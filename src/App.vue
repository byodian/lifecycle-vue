<template>
  <div id="app">
    <AComponent :adata="options"/>
    <BComponent :bdata="adata.age" />
    <CComponent :cdata="cdata" v-if="isShow" />
  </div>
</template>

<script>
import CComponent from './components/CComponent.vue'
import AComponent from './components/AComponent.vue'
import BComponent from './components/BComponent.vue'

export default {
  name: 'App',
  components: {
    CComponent,
    AComponent,
    BComponent
  },
  data() {
    return {
      adata: {},
      options: {},
      bdata: 'B',
      cdata: 'C',
      isShow: false
    }
  },
  watch: {
    adata: {
      handler (newData) {
        this.options = {
          name: newData.name || '暂无',
          age: '12'
        }

        // console.log(this.options)
      },
      deep: true,
      immediate: true
    }
  },
  created() {
    console.log('%cparent created', 'color: pink')
    // const promise = new Promise((resolve) => {
    //   setTimeout(() => {
    //     resolve('123') 
    //   }, 0);
    // })

    // promise.then(data => {
    //   this.adata = {
    //     name: `byodian${data}`,
    //     age: '21'
    //   }
    // })
  },
  mounted() {
    console.log('parent mounted')
    const promise = new Promise((resolve) => {
      setTimeout(() => {
        resolve('123') 
      }, 0);
    })

    promise.then(data => {
      this.adata = {
        name: `byodian${data}`,
        age: '21'
      }
    })
  },
  beforeUpdate() {
    console.log('parent beforeUpdate')
  },
  updated() {
    console.log('parent updated')
  },
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
