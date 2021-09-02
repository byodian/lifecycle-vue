<template>
  <div>
    {{bdata}}
  </div> 
</template>

<script>
export default {
  name: 'B',
  props: {
    bdata: {
      type: String,
      default: ''
    }
  },
  beforeCreate() {
    console.log('%cbeforeCreate B 组件', 'color: red')
  },
  created() {
    console.log('%ccreated B 组件', 'color: red')
  },
  beforeMount() {
    console.log('%cbeforeMounte B 组件', 'color: red')
  },
  mounted() {
    console.log('%cmounted B 组件', 'color: red')
  },
  beforeUpdate() {
    console.log('%cbeforeUpdate B 组件', 'color: red')
  },
  updated() {
    console.log('%cupdated B 组件', 'color: red')
  },
}
</script>

<style>

</style>>