<script>
import AComponent from './components/AComponent.vue'
import BComponent from './components/BComponent.vue'
import SlotComponent from './components/SlotComponent.vue'

const debounce = function (callback, delay) {
  let timer
  return function () {
    clearTimeout(timer)
    const args = arguments
    timer = setTimeout(() => {
      callback.apply(callback, args)
    }, delay)
  }
}

export default {
  name: 'App',
  components: {
    AComponent,
    BComponent,
    SlotComponent
  },
  data () {
    return {
      adata: {},
      options: {},
      isShow: false,
      uid: 1
    }
  },
  watch: {
    adata: {
      handler (newData) {
        if (Object.keys(newData).length > 0) {
          this.isShow = true
        }
        this.options = {
          xAxis: {
            type: 'category',
            data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
          },
          yAxis: {
            type: 'value'
          },
          series: [
            {
              name: 'a',
              data: newData.items,
              type: 'line',
            }
          ]
        }
      },
      deep: true,
      immediate: true
    }
  },
  beforeCreate () {
    console.log('%cbeforeCreate 父组件', 'color: pink')
  },
  created () {
    console.log('%ccreated 父组件', 'color: pink')
    const promise = new Promise((resolve) => {
      setTimeout(() => {
        resolve('123')
      }, 0)
    })

    promise.then((data) => {
      // 为已有对象赋值多个新 property
      const interObject = {
        name: `byodian${data}`,
        age: '21',
        items: [150, 230, 224, 218, 135, 147, 260]
      }

      // 1. 对象字面量赋值替换
      // this.adata = interObject

      // 2. 使用 Vue.set(object, propertyName, value)
      // this.$set(this.adata, 'name', `byodian${data}`)
      // this.$set(this.adata, 'items', [150, 230, 224, 218, 135, 147, 260])

      // 3. 使用 Object.assign() 赋值替换 
      // this.adata = Object.assign({}, this.adata, interObject)

      // 4. 使用结构赋值
      this.adata = { ...this.adata, ...interObject }
    })
  },
  mounted () {
    // 窗口尺寸变化后，强制刷新图表组件宽高
      window.addEventListener('resize', debounce(() => {
        this.uid += 1
      }, 300))

    this.$nextTick(() => {
      console.log('%c$nextTick mounted', 'color: pink')
    })
  },
  beforeUpdate () {
    console.log('%cbeforeUpdate 父组件', 'color: pink')
  },
  updated () {
    console.log('%cupdated 父组件', 'color: pink')
  },
}
</script>

<template>
  <div id="app">
    <div class="box1">
      <a-component v-if="isShow" :adata="adata" name="box1" />
      <div v-if="isShow" class="b-com-wrapper">
        <b-component
          :key="uid"
          name="box1"
          :options="options"
          width="100%"
          height="100%" />
      </div>
    </div>
    <slot-component>
      <template v-slot:header>
        <a-component :adata="adata" name="slotComponent" />
      </template>
      <template v-slot:main>
        <b-component
          :key="uid"
          name="slotComponent"
          :options="options"
          width="100%"
          height="100%" />
      </template>
    </slot-component>
    <div class="box2">
      <dv-border-box-1>
        <b-component
          :key="uid"
          name="dv-border-box"
          :options="options"
          width="100%"
          height="100%" />
      </dv-border-box-1>
    </div>
  </div>
</template>

<style>
p {
  margin: 0;
}

body {
  margin: 0;
  padding: 0;
}

#app {
  text-align: center;
  color: #2c3e50;
  margin: 20px;
  display: flex;
  flex-direction: column;
  gap: 30px;
}

.box1 {
  display: flex;
  flex-direction: column;
  height: 300px;

  outline: 1px dashed #000;
}

.box2 {
  height: 300px;
}

.b-com-wrapper {
  width: 100%;
  flex-basis: 100%;
  background-color: #f7fce5;
}
</style>
