<template>
  <div class="home-wrapper">
    <div id="container"></div>
    <div class="controller-wrapper">
      <button @click="changeMapStyle()">改变地图风格</button>
      <button @click="setMarkers()">撒点</button>
      <button @click="clearMarkers()">清除撒点</button>
      <button @click="hideInfo()">关闭信息窗口</button>
    </div>
  </div>
</template>

<script>
import AMap from "AMap";
export default {
  name: "Home",
  data() {
    return {
      map: null,
      mapStyle: [
        "normal",
        "macaron",
        "graffiti",
        "whitesmoke",
        "dark",
        "fresh",
        "darkblue",
        "blue",
        "light",
        "grey"
      ],
      // mapStyleNum: 0,
      infoWindow: null,
      markers: [
        {
          lng: "121.347",
          lat: "31.06632",
          title: "邦普园",
          info: "邦普园信息"
        },
        {
          lng: "121.349",
          lat: "31.06332",
          title: "昱章电气",
          info: "昱章电气信息"
        }
      ]
    };
  },
  methods: {
    // 初始化地图
    initMap(style) {
      this.map = new AMap.Map("container", {
        zoom: 14,
        center: [121.347, 31.06632],
        // 地图风格：
        mapStyle: "amap://styles/" + style
      });
    },
    // 改变地图风格
    changeMapStyle() {
      let n = Math.floor(Math.random() * 10);
      this.map.setMapStyle("amap://styles/" + this.mapStyle[n]);
    },
    // 地图撒点
    setMarkers() {
      let markersList = this.markers.map(item => {
        let marker = new AMap.Marker({
          position: new AMap.LngLat(item.lng, item.lat),
          title: item.title
        });
        marker.on("click", () => {
          this.showInfo(item);
        });
        return marker;
      });
      this.map.add(markersList);
    },
    // 清除撒点
    clearMarkers() {
      this.map.remove(this.markers);
    },
    // 点击撒点显示信息
    showInfo(item) {
      this.infoWindow = new AMap.InfoWindow({
        anchor: "bottom-center",
        content: item.info
      });
      this.infoWindow.open(this.map, [item.lng, item.lat]);
    },
    // 关闭信息窗口
    hideInfo() {
      this.infoWindow.close();
    }
  },
  mounted() {
    this.initMap(this.mapStyle[3]);
  }
};
</script>

<style lang="stylus" scoped>
.home-wrapper
  width: 100vw
  height: 100vh
  position: relative
  #container
    position: absolute
    top: 0
    left: 0
    width: 100%
    height: 100%
  .controller-wrapper
    position: absolute
    top: 15px
    left: 15px
</style>
