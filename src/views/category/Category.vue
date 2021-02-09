<template>
  <div class="wrapper" ref="aaa">
    <div class="content">
      <button @click="btnclick">按钮</button>
      <ul>
        <li>1100</li>
        <li>2100</li>
        <li>3100</li>
        <li>4100</li>
        <li>5100</li>
        <li>6100</li>
        <li>7100</li>
        <li>8100</li>
        <li>9100</li>
        <li>10100</li>
        <li>11100</li>
        <li>12100</li>
        <li>13100</li>
        <li>14100</li>
        <li>15100</li>
        <li>16100</li>
        <li>17100</li>
        <li>18100</li>
        <li>19100</li>
        <li>20100</li>
        <li>21100</li>
        <li>22100</li>
        <li>23100</li>
        <li>24100</li>
        <li>25100</li>
        <li>26100</li>
        <li>27100</li>
        <li>28100</li>
        <li>29100</li>
        <li>30100</li>
        <li>31100</li>
        <li>32100</li>
        <li>33100</li>
        <li>34100</li>
        <li>35100</li>
        <li>36100</li>
        <li>37100</li>
        <li>38100</li>
        <li>39100</li>
        <li>40100</li>
        <li>41100</li>
        <li>42100</li>
        <li>43100</li>
        <li>44100</li>
        <li>45100</li>
        <li>46100</li>
        <li>47100</li>
        <li>48100</li>
        <li>49100</li>
        <li>50100</li>
        <li>51100</li>
        <li>52100</li>
        <li>53100</li>
        <li>54100</li>
        <li>55100</li>
        <li>56100</li>
        <li>57100</li>
        <li>58100</li>
        <li>59100</li>
        <li>60100</li>
        <li>61100</li>
        <li>62100</li>
        <li>63100</li>
        <li>64100</li>
        <li>65100</li>
        <li>66100</li>
        <li>67100</li>
        <li>68100</li>
        <li>69100</li>
        <li>70100</li>
        <li>71100</li>
        <li>72100</li>
        <li>73100</li>
        <li>74100</li>
        <li>75100</li>
        <li>76100</li>
        <li>77100</li>
        <li>78100</li>
        <li>79100</li>
        <li>80100</li>
        <li>81100</li>
        <li>82100</li>
        <li>83100</li>
        <li>84100</li>
        <li>85100</li>
        <li>86100</li>
        <li>87100</li>
        <li>88100</li>
        <li>89100</li>
        <li>90100</li>
        <li>91100</li>
        <li>92100</li>
        <li>93100</li>
        <li>94100</li>
        <li>95100</li>
        <li>96100</li>
        <li>97100</li>
        <li>98100</li>
        <li>99100</li>
        <li>100100</li>
      </ul>
    </div>
  </div>
</template>

<script>
import BScroll from 'better-scroll'

export default {
  name: "Category",
  data() {
    return {
      bscroll: null
    }
  },
  methods: {
    btnclick() {
      console.log('btnclick');
    }
  },
  mounted() {
    this.bscroll = new BScroll(document.querySelector('.wrapper'),{
      probeType: 3,
      pullUpLoad: true,
      click:true
    })

    this.bscroll.on('scroll', position => {
      console.log(position);
    })

    this.bscroll.on('pullingUp', () => {
      console.log('上拉加载更多');
    })
  }
}
</script>

<style scoped>
  .wrapper {
    height: 150px;
    background: red;
  }
</style>
