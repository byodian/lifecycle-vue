<template>
  <div :id="id" :class="className" :style="{ height: height, width: width }" :alt="options.series[0].name" />
</template>

<script>
export default {
  name: 'Echart',
  props: {
    className: {
      type: String,
      default: 'chart'
    },
    id: {
      type: String,
      default: 'chart'
    },
    width: {
      type: String,
      default: '100%'
    },
    height: {
      type: String,
      default: '2.5rem'
    },
    options: {
      type: Object,
      default: () => ({})
    }
  },
  data () {
    return {
      chart: null
    }
  },
  watch: {
    options: {
      handler (options) {
        // 设置true清空echart缓存
        this.chart.setOption(options, true)
      },
      deep: true
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
  beforeUpdate() {
    console.log('%cbeforeUpdate B 组件', 'color: red')
  },
  updated() {
    console.log('%cupdated B 组件', 'color: red')
  },
  mounted () {
    console.log('%cmounted B 组件', 'color: red')
    this.initChart()
  },
  methods: {
    initChart () {
      // 初始化echart
      this.chart = this.$echarts.init(this.$el)
      this.chart.setOption(this.options, true)
    }
  }
}
</script>