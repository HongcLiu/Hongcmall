<template>
  <div class="good-list">
    <good-list-item v-for="item in goodlist" :goodlistitem="item"></good-list-item>
  </div>

</template>

<script>
import GoodListItem from "./GoodListItem";

export default {
  name: "GoodList",
  props: {
    goodlist: {
      type: Array,
      default() {
        return []
      }
    }
  },
  components: {
    GoodListItem
  }
}
</script>

<style scoped>
.good-list {
  display: flex;
  flex-wrap: wrap;
  justify-content: space-around;
  background-color: var(--color-background);
  padding: 2px;
  z-index: 0;
}
</style>
