<template>
  <div id="container"></div>
</template>

<script>
import AMap from "AMap";
export default {
  name: "Map",
  data() {
    return {
      map: null,
      marker: []
    };
  },
  methods: {
    // 初始化地图
    initMap() {
      this.map = new AMap.Map("container", {
        zoom: 14,
        center: [121.347, 31.06632],
        mapStyle: "amap://styles/macaron"
      });
    }
    // 地图撒点
    // 清除撒点
    // 点击撒点显示信息
  },
  mounted() {
    this.initMap();
  }
};
</script>

<style lang="stylus" scoped>
#container
  width: 100%
  height: 100%
  position: absolute
  top: 0
  left: 0
</style>
