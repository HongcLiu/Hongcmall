<template>
  <div id="detail-navbar">
    <nav-bar>
      <div slot="left" class="back-logo" @click="backClick">
        <img src="~assets/img/common/back.svg" alt="">
      </div>
      <div slot="center" class="center">
        <div v-for="(item,index) in titles"
             class="title"
             :class="{active: currentIndex === index}"
             @click="itemClick(index)">{{item}}</div>
      </div>
    </nav-bar>
  </div>
</template>

<script>
import NavBar from "components/common/navbar/NavBar";

export default {
  name: "DetailNavBar",
  components: {
    NavBar
  },
  data() {
    return {
      titles: ['商品','参数','评论','推荐'],
      currentIndex: 0
    }
  },
  methods: {
    itemClick(index) {
      this.currentIndex = index
    },
    backClick() {
      this.$router.back()
    }
  }
}
</script>

<style scoped>
  .center {
    display: flex;
  }

  .title {
    flex: 1;
    font-size: 14px;
  }

  .active {
    color: #ff8198;
  }

  .back-logo {
    margin-top: 6px;
  }
</style>
