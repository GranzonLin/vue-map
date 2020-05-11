<template>
    <div class="home">
        <div id="mapContainer" class="map-container" ref="mapContainer"></div>
    </div>
</template>

<script>
    export default {
        name: 'Home',
        data(){
            return{
                zoom:'15',
                T:{},
                map:''
            }
        },
        mounted(){
            this.drawMap()
        },
        methods:{
            // 确保地图加载完毕
            init(){
                return new Promise((resolve,reject) => {
                    if(typeof window.T !== 'undefined'){
                        resolve(window.T);
                        return true
                    }
                    window.onload = () => {
                        resolve(window.T)
                    }
                })
            },
            drawMap(){
                this.init().then(T => {
                    this.T = T;
                    this.map = new T.Map(this.$refs.mapContainer);
                    this.map.centerAndZoom(new T.LngLat(116.112230,24.304730), this.zoom);
                })
            },
            getLngLat(lnglat) {
                console.log(lnglat.lng.toFixed(6) + "," + lnglat.lat.toFixed(6));
            }
        }
    }
</script>

<style lang="less" scoped>
    .map-container{
        width: 900px;
        height: 700px;
        margin: 0 auto;
    }
</style>
