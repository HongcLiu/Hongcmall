<template>
  <div class="goods-item">
    <a :href="goodlistitem.link">
      <img :src="goodlistitem.show.img" alt="">
      <div class="goods-info">
        <p>{{goodlistitem.title}}</p>
        <span class="price">{{goodlistitem.price}}</span>
        <span class="collects">{{goodlistitem.cfav}}</span>
      </div>
    </a>
  </div>
</template>

<script>
export default {
  name: "GoodListItem",
  props: {
    goodlistitem: {
      type: Object,
      default() {
        return {}
      }
    }
  }
}
</script>

<style scoped>
.goods-item {
  padding-bottom: 40px;
  position: relative;
  width: 48%;
}
.goods-item img {
  width: 100%;
  border-radius: 5px;
  border:3px solid var(--color-tint);
}
.goods-info {
  font-size: 12px;
  position: absolute;
  bottom: 5px;
  left: 0;
  right: 0;
  overflow: hidden;
  text-align: center;
}
.goods-info p {
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
  margin-bottom: 3px;
}
.goods-info .price {
  color: var(--color-high-text);
  margin-right: 20px;
}
.goods-info .collects {
  position: relative;
}
.goods-info .collects::before {
  content: '';
  position: absolute;
  left: -15px;
  top: -1px;
  width: 14px;
  height: 14px;
  background: url("~assets/img/common/collect.svg") 0 0/14px 14px;
}
</style>
