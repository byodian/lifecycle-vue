<template>
  <div class="hello">
    <p>{{ cdata }}</p>
  </div>
</template>

<script>
export default {
  name: 'C',
  props: {
    cdata: String
  },
  beforeCreate () {
    console.log('%cbeforeCreate C 组件', 'color: pink')
  },
  created () {
    console.log('%ccreated C 组件', 'color: pink')
  },
  beforeMount () {
    console.log('%cbeforeMounte C 组件', 'color: pink')
  },
  mounted () {
    console.log('%cmounted C 组件', 'color: pink')
  },
  beforeUpdate () {
    console.log('%cbeforeUpdate C 组件', 'color: pink')
  },
  updated () {
    console.log('%cupdated C 组件', 'color: pink')
  }

}
</script>
