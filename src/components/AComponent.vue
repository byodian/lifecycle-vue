<template>
  <p class="a-com">{{ adata.name }}</p>
</template>

<script>
export default {
  name: 'A',
  props: {
    adata: {
      type: Object,
      default: () => ({})
    }
  },
  beforeCreate () {
    console.log(`%cbeforeCreate A 组件 - ${this.$attrs.name}`, 'color: #f9c30f')
  },
  created () {
    console.log(`%ccreated A 组件 - ${this.$attrs.name}`, 'color: #f9c30f')
  },
  beforeMount () {
    console.log(`%cbeforeMount A 组件 - ${this.$attrs.name}`, 'color: #f9c30f')
  },
  mounted () {
    console.log(`%cmounted A 组件 - ${this.$attrs.name}`, 'color: #f9c30f')
  },
  beforeUpdate () {
    console.log(`%cbeforeUpdate A 组件 - ${this.$attrs.name}`, 'color: #f9c30f')
  },
  updated () {
    console.log(`%cupdated A 组件 - ${this.$attrs.name}`, 'color: #f9c30f')
  }
}
</script>

<style  scoped>
.a-com {
  outline: 1px dashed blueviolet;
}
</style>
