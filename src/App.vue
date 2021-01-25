<template>
  <div id="map">
  </div>
</template>

<script>
// import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'App',
  // components: {
  //   HelloWorld
  // },
  data(){
    return{

    }
  },
  methods:{

  },
  created(){
    let smp = new window.SoonMap({
      id:'map', 
      center:[116.4, 39.9], 
      zoom:9,
    });
    smp.drawCircle({
      center:[116.4, 39.9], 
      radiusInKm:1, 
      fillColor:"red", 
      fillOpacity:0.2,
      centerRadius:10
    })
  }
}
</script>

<style>
#map {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}
</style>
<style>
  #map{
    width: 100%;
    height: 100vh;
    display: flex;
  }
  body {
    margin: 0px;
  }
</style>
