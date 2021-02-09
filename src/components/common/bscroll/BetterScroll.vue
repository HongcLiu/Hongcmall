<template>
  <div class="wrapper" ref="wrapper">
    <div class="content">
      <slot></slot>
    </div>
  </div>
</template>

<script>
import BScroll from 'better-scroll'

export default {
  name: "BetterScroll",
  data() {
    return {
      bscroll: null
    }
  },
  // ref对于元素标签来说拿到的是元素对象
  // ref对于组件来说拿到的是组件对象
  mounted() {
    this.bscroll = new BScroll(this.$refs.wrapper, {
      click: true
    })
  },
  methods: {
    scrollTo(x, y, time=500) {
      this.bscroll.scrollTo(x, y, time)
    }
  }
}
</script>

<style scoped>
</style>
