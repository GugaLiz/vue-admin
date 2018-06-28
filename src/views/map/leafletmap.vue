<template>
    <div id="leaflet-map">

    </div>
</template>

<script>
import Leaflet from 'leaflet'
import MiniMap from 'leaflet-minimap'
import "../../../node_modules/leaflet/dist/leaflet.css"

delete Leaflet.Icon.Default.prototype._getIconUrl
Leaflet.Icon.Default.imagePath = ''
Leaflet.Icon.Default.mergeOptions({
  iconRetinaUrl: require('../../assets/markers/marker-icon-2x.png'),
  iconUrl: require('../../assets/markers/marker-icon.png'),
  shadowUrl: require('../../assets/markers/marker-shadow.png')
})

export default {
    data() {
        return {
            map:null,
            map_config:{
                url:'https://{s}.tile.openstreetmap.org/{z}/{x}/{y}.png',
                center:[37.5,106],
                zoom:4,
                minZoom:2,
                maxZoom:18,
                zoomControl:false,
                attribution: 'Map data &copy; <a href="http://openstreetmap.org">OpenStreetMap</a> contributors, <a href="http://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery © <a href="http://mapbox.com">Mapbox</a>',
            }
        }
    },
    mounted:function() {
        this.initMap();
        this.initTool();
    },
    methods: {
        initMap:function(){
            this.map = new Leaflet.map('leaflet-map',{
                center:this.map_config.center,
                zoom:this.map_config.zoom,
                minZoom:this.map_config.minZoom,
                maxZoom:this.map_config.maxZoom,
                zoomControl:this.map_config.zoomControl
            });
            Leaflet.tileLayer(this.map_config.url,{
                attribution:this.map_config.attribution
            }).addTo(this.map);
        },
        initTool:function(){
            var osm2 = new Leaflet.TileLayer(this.map_config.url, {minZoom: 0, maxZoom: 13, attribution: this.map_config.attribution });

            this.map = new Leaflet.Control.MiniMap(osm2,{ toggleDisplay: true }).addTo(this.map);
        }
    }
}
</script>
<style>
@import url(../../../node_modules/leaflet/dist/leaflet.css);
#leaflet-map{
    float:left;
    width:100%;
    height:500px;
    margin-left:5px
}
</style>


