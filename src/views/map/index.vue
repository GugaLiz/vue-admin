<template>
  <baidu-map class="map" :center="center" :zoom="4" :scroll-wheel-zoom="true" shape="BMAP_POINT_SHAPE_STAR" color="green">
    <bm-point-collection :points="points" shape="BMAP_POINT_SHAPE_CIRCLE" color="green" size="BMAP_POINT_SIZE_SMALL" @click="clickHandler"></bm-point-collection>
  </baidu-map>
</template>

<script>
export default {
  data() {
    return {
      center: { lng: 116.404, lat: 39.915 },
      points: []
    }
  },
  mounted() {
      this.addPoints()
  },
  methods: {
    clickHandler(e) {
      alert(`单击点的坐标为：${e.point.lng}, ${e.point.lat}`)
    },
    addPoints() {
      const points = []
      for (var i = 1; i < 46; i++) {
        const position = { lng: 116.404 + (i * 0.001), lat: 39.915 - (i * 0.001) }
        points.push(position)
      }
      this.points = points
      console.log(this.points)
    }
  }
}
</script>
<style>
/* The container of BaiduMap must be set width & height. */
.map {
  width: 100%;
  height: 600px;
}
</style>