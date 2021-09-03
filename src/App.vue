<script>
import AComponent from './components/AComponent.vue'
import BComponent from './components/BComponent.vue'

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
    BComponent
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
              type: 'line'
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
      this.adata = {
        name: `byodian${data}`,
        age: '21',
        items: [150, 230, 224, 218, 135, 147, 260]
      }
    })
  },
  mounted () {
    console.log('%cmounted 父组件', 'color: pink')
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
  }
}
</script>

<template>
  <div id="app">
    <AComponent :adata="adata" />
    <div v-if="isShow" class="b-com-wrapper">
      <BComponent
        :key="uid"
        :options="options"
        width="100%"
        height="100%" />
    </div>
  </div>
</template>

<style>
p {
  margin: 0;
}

#app {
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
  display: flex;
  flex-direction: column;
  height: 300px;

  outline: 1px dashed #000;
}

.b-com-wrapper {
  width: 100%;
  flex-basis: 100%;
  outline: 1px dashed pink;
}
</style>
