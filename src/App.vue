<template>
  <div id="app">
    <div class="center">
      <vue-soonspace
        customId="vue-soonspace-customId"
        customClass="vue-soonspace-customClass"
        :customStyle="{
          margin: '0 auto',
          width: '600px',
          height: '300px'
        }"
        :option="{
          showInfo: true,
          showGrid: true,
          backgroundColor: 0x333300
        }"
        :globalSdk="false"
        @sceneReady="sceneReady"
        @modelClick="modelClick"
        @selectPosition="selectPosition"
      ></vue-soonspace>
    </div>
    <HelloWorld />
  </div>
</template>

<script>
import HelloWorld from './components/HelloWorld.vue'

export default {
  name: 'app',
  components: {
    HelloWorld
  },
  methods: {
    sceneReady(ssp) {
      console.log("soonspace: ", ssp);
    },
    modelClick(param) {
      console.log("soonspace modelClick", param);
    },
    selectPosition(position) {
      console.log("soonspace selectPosition", position);
    }
  }
}
</script>

<style>
#app {
  font-family: 'Avenir', Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
