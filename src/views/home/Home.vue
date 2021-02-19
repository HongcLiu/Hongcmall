<template>
  <div id="home">
    <nav-bar class="home-nav">
      <div slot="center">购物车</div>
    </nav-bar>
    <tab-control :titles="['流行','新款','精选']"
                 class="tab-control"
                 @tabClick="tabClick"
                 ref="tabControl1" v-show="topTabControlShow"></tab-control>
    <better-scroll ref="scroll"
                   class="content"
                   :probe-type="3"
                   @scroll="scrollClick"
                   :pull-up-load="true"
                    @pulling="pullingClick">
      <home-swiper :banners="banners" @homeSwiperImgLoad="swiperImgLoad"></home-swiper>
      <recommend-view :recommends="recommends"></recommend-view>
      <feature-view/>
      <tab-control :titles="['流行','新款','精选']"
                   @tabClick="tabClick" ref="tabControl2"></tab-control>
      <good-list :goodlist="showGoods" />
    </better-scroll>

    <back-top @click.native="backClick" v-show="isShowBackTop"></back-top>
  </div>
</template>

<script>
import NavBar from "components/common/navbar/NavBar";
import BetterScroll from "components/common/bscroll/BetterScroll";
import TabControl from "components/content/tabControl/TabControl";
import GoodList from "components/content/goods/GoodList";
import BackTop from "components/content/backtop/BackTop";

import HomeSwiper from "views/home/childComps/HomeSwiper";
import RecommendView from "views/home/childComps/RecommendView";
import FeatureView from "views/home/childComps/FeatureView";

import {getHomeMultidata, getHomeGoods} from "network/home";

export default {
  name: "Home",
  components: {
    NavBar,
    BetterScroll,
    TabControl,
    GoodList,
    BackTop,
    HomeSwiper,
    RecommendView,
    FeatureView
  },
  data() {
    return {
      banners: [],
      recommends: [],
      goods: {
        'pop': {page: 0, list: []},
        'new': {page: 0, list: []},
        'sell': {page: 0, list: []},
      },
      currentType: 'pop',
      isShowBackTop: false,
      tabOffsetTop: 0,
      topTabControlShow: false,
      saveY: 0
    }
  },
  computed: {
    showGoods() {
      return this.goods[this.currentType].list
    }
  },
  created() {
    // 1请求多个数据
    this.getHomeMultidata()

    // 2请求商品数据
    this.getHomeGoods('pop')
    this.getHomeGoods('new')
    this.getHomeGoods('sell')

  },
  mounted() {
    // 3监听item中图片加载完成
    this.$bus.$on('itemImgLoad', () => {
      this.$refs.scroll.refresh()
    })

  },
  activated() {
    this.$refs.scroll.scrollTo(0, this.saveY, 0)
    this.$refs.scroll.refresh()
  },
  deactivated() {
    this.saveY = this.$refs.scroll.getScrollY()
  },
  methods: {
    /**
     * 事件监听相关代码
     */

    tabClick(index) {
      switch (index) {
        case 0:
          this.currentType = 'pop'
          break
        case 1:
          this.currentType = 'new'
          break
        case 2:
          this.currentType = 'sell'
          break
      }
      this.$refs.tabControl1.currentIndex = index
      this.$refs.tabControl2.currentIndex = index
    },

    backClick() {
      this.$refs.scroll.scrollTo(0, 0);
    },

    scrollClick(position) {
      this.isShowBackTop = -position.y > 1000
      if(-position.y > this.tabOffsetTop) {
        this.topTabControlShow = true
      }else {
        this.topTabControlShow = false
      }
    },

    pullingClick() {
      this.getHomeGoods(this.currentType)
      this.$refs.scroll.finishPullUp()
    },

    swiperImgLoad() {
      // 获取tabControl的offSetTop

      this.tabOffsetTop = this.$refs.tabControl2.$el.offsetTop
    },


    /**
     * 网络请求相关代码
     */
    getHomeMultidata() {
      getHomeMultidata().then(res => {
        this.banners = res.data.banner.list
        this.recommends = res.data.recommend.list
      })
    },
    getHomeGoods(type) {
      const page = this.goods[type].page + 1
      getHomeGoods(type, page).then(res => {
        this.goods[type].list.push(...res.data.list)
        this.goods[type].page += 1
      })
    }
  }
}


</script>

<style scoped>
  #home {
    /*padding-top: 44px;*/
    height: 100vh;
    position: relative;
  }

  .home-nav {
    background: var(--color-tint);
    color: #ffffff;

    /*position: fixed;*/
    /*left: 0;*/
    /*right: 0;*/
    /*top: 0;*/
    /*z-index: 7;*/
  }

  .tab-control {
    position: relative;
  }

  .content {
    overflow: hidden;

    position: absolute;
    top: 44px;
    bottom: 49px;
    right: 0px;
    left: 0px;
  }

  /*.content {*/
  /*  height: calc(100% - 93px + 51px);*/
  /*  overflow: hidden;*/
  /*}*/
</style>
