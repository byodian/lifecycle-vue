<script>
export default {
  name: 'SlotComponent',
  beforeCreate () {
    console.log('%cbeforeCreate Slot 父组件', 'color: #f9c30f')
  },
  created () {
    console.log('%ccreated Slot 父组件', 'color: #f9c30f')
  },
  beforeMount () {
    console.log('%cbeforeMount Slot 父组件', 'color: #f9c30f')
  },
  mounted () {
    console.log('%cmounted Slot 父组件', 'color: #f9c30f')
  },
  beforeUpdate () {
    console.log('%cbeforeUpdate Slot 父组件', 'color: #f9c30f')
  },
  updated () {
    console.log('%cupdated Slot 父组件', 'color: #f9c30f')
  }
}
</script>

<template>
  <div class="slot-com-wrapper">
    <div class="slot-header">
      <slot name="header"></slot>
    </div>
    <div class="slot-main">
      <slot name="main"></slot>
    </div>
  </div>
</template>

<style lang="scss" scoped>
.slot-com-wrapper {
  display: flex;
  flex-direction: column;
  height: 300px;

  outline: 1px dashed #333;

  .slot-main {
    flex-basis: 100%;
    background-color: #f7fce5;
  }
}
</style>