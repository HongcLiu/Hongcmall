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
  props: {
    probeType: {
      type: Number,
      default() {
        return 0
      }
    },
    pullUpLoad: {
      type: Boolean,
      default() {
        return false;
      }
    }
  },
  // ref对于元素标签来说拿到的是元素对象
  // ref对于组件来说拿到的是组件对象
  mounted() {
    this.bscroll = new BScroll(this.$refs.wrapper, {
      click: true,
      probeType: this.probeType,
      pullUpLoad: this.pullUpLoad
    })
    this.bscroll.on('scroll', position => {
      this.$emit('scroll',position)
    })
    this.bscroll.on('pullingUp', () => {
      this.$emit('pulling')
    })
  },
  methods: {
    scrollTo(x, y, time=500) {
      this.bscroll && this.bscroll.scrollTo(x, y, time)
    },
    finishPullUp() {
      this.bscroll.finishPullUp()
    },
    refresh() {
      this.bscroll && this.bscroll.refresh()
    },
    getScrollY() {
      return this.bscroll ? this.bscroll.y : 0
    }
  }
}
</script>

<style scoped>
</style>
