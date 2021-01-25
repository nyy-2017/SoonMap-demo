<template>
  <div id="map">
    <div class="map-header">
      <MapHeader/>
    </div>
    <div class="map-body">
      <div class="map_left">
        <MapLeft/>
      </div>
      <div class="map_center">
        <MapSoonspace/>
      </div>
      <div class="map_right">
        <MapRight/>
      </div>
    </div>
    <div class="map-footer">
      <MapFooter/>
    </div>
  </div>
</template>

<script>
import MapHeader from './components/MapHeader.vue'
import MapSoonspace from './components/MapSoonspace.vue'
import MapLeft from './components/MapLeft.vue'
import MapRight from './components/MapRight.vue'
import MapFooter from './components/MapFooter.vue'
export default {
  name: 'app',
  components: {MapHeader, MapSoonspace, MapLeft, MapRight, MapFooter},
  data(){
    return{

    }
  },
  methods: {}
}
</script>

<style>
*{
  padding: 0;
  margin: 0;
}
#map {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
.map-header{
  display: flex;
  align-items: center;
  width: 100%;
  height: 5.83333333vh;
  min-height: 63px;
  background: #030d1e;
}
.map-body{
  position: relative;
  flex: 1 1;
}
.map_left{
  position: absolute;
  top: 0;
  left: 0;
  height: calc(100vh - 98px);
  width: 366px;
  background: #030d1e;
  padding: 0 20px;
  z-index: 80;
}
.map_right{
  position: absolute;
  top: 0;
  right: 0;
  height: calc(100vh - 98px);
  width: 366px;
  background: #030d1e;
  padding: 0 20px;
  z-index: 80;
}
.map-footer{
  position: fixed;
  display: flex;
  align-items: center;
  justify-content: space-between;
  bottom: 0;
  width: 100%;
  padding: 0 10px;
  height: 3.24074074vh;
  min-height: 35px;
  background: #030d1e;
  z-index: 999;
}
</style>
