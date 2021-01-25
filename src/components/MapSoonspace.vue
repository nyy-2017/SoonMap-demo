<template>
  <div id="map">
      <!-- <vue-soonspace
        customId="vue-soonspace-customId"
        customClass="vue-soonspace-customClass"
        :customStyle="{
          margin: '0 auto',
          width: '1920px',
          height: '874px'
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
      ></vue-soonspace> -->
  </div>
</template>

<script>
    var smp = new window.SoonMap({
        id:'map', 
        center:[116.4, 39.9], 
        zoom:9,
        // hasBaseMap:false
    });
export default {
    data(){
        return{
          
        }
    },
    methods:{
        // sceneReady(ssp) {
        //     console.log("soonspace: ", ssp);
        // },
        // modelClick(param) {
        //     console.log("soonspace modelClick", param);
        // },
        // selectPosition(position) {
        //     console.log("soonspace selectPosition", position);
        // },

        loadSubwayGeoJson() {

            // var smp = new window.SoonMap({
            //     id:'map', 
            //     center:[116.4, 39.9], 
            //     zoom:9,
            //     // hasBaseMap:false
            // });
            // smp.drawCircle({
            //     center:[116.4, 39.9], 
            //     radiusInKm:1, 
            //     fillColor:"red", 
            //     fillOpacity:0.2,
            //     centerRadius:10
            // })
            smp.getOauthToken({
                accessKey   : 'xw1cq3quhbau1r23',
                sign        : 'aac6475ff309f848ca199ee53ad34128',
                nonce       : 'ab5537dd-9ea3-4b86-902c-0da8c2b5024b',
                timestamp   :  1608865823063,
                host        : 'http://test.gis.xwbuilders.com',
                port        :  '8888'
                // host        : 'http://192.168.2.163',
                // port        :  '8082'
            })
            smp.addScalControl()
            smp.addNavigationControl()
            smp.addGeolocateControl()


            //线路编号一定是一个字符串
            const lines = smp.loadSubwayGeoJson({lineIds:['01','02','03','04','05','06','07','08','09','10']});

            const subwayScene = smp.getSubwayScene();
            subwayScene.addEventLisnter('click', (features)=> {
                console.log('click', features)
            })
            subwayScene.addEventLisnter('hover', (features)=> {
                console.log('hover', features)
            })

            // 设置所有线路的不透明度
            for (const i in lines) {
                const id = lines[i]._lineLayerId
                console.log(lines[i]);
                smp.map.setPaintProperty(id, 'line-opacity', 0.5)
            }
            subwayScene.addEventLisnter('click', (features) => {
                console.log('click', features)
                const selectLayerId = features[0].layer.id
                let source = smp.map.getSource(features[0].source)
                console.log(source._data);
                smp.flyToFeature(source._data.features[0].geometry, 13)
                smp.map.setPaintProperty(selectLayerId, 'line-opacity', 0.5)
                // subwayScene.removeLineLayer()
                // smp.shrinkFeature(features[0])
            })
            let layers = subwayScene._subwayLayers
            for(let i in layers) {
                layers[i].zoomThreshold = 1
            }
            subwayScene.getLines(lines=>{
                console.log(lines);

            })
            this.addLine(); 
        },

        addLine() {
            let layer = smp.addLayer({
                id: 'my-line',
                type: 'point',
                url: 'http://test.gis.xwbuilders.com:8888/files/upload/3dpoi/1kgelb1vgv9t/station.png',
                data: [{
                    "type": "Feature",
                    "geometry": {
                        "type": "Point",
                        "coordinates": 
                        [116.31726184631289, 39.90611941596121],
                    },
                    "properties":{
                        "iconSize":1.25
                    }
                }]
            })
            layer.setIconAllowOverlap(false)
            console.log(layer);
        }
    },
    created(){
        this.loadSubwayGeoJson();
    }
}
</script>
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