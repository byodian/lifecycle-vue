<template>
    <p class="a-com">{{ adata.name }}</p>
</template>

<script>
export default {
  name: 'A',
  props: {
    adata: Object,
    default: () => ({})
  },
  beforeCreate() {
    console.log('%cbeforeCreate A 组件', 'color: green')
  },
  created() {
    console.log('%ccreated A 组件', 'color: green')
  },
  beforeMount() {
    console.log('%cbeforeMounte A 组件', 'color: green')
  },
  mounted() {
    console.log('%cmounted A 组件', 'color: green')
  },
  beforeUpdate() {
    console.log('%cbeforeUpdate A 组件', 'color: green')
  },
  updated() {
    console.log('%cupdated A 组件', 'color: green')
  },

}
</script>

<style  scoped>
.a-com {
  outline: 1px dashed blueviolet;
}
</style>