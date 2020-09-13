<template>
    <div class="slide-banner">
        <div id="demo" class="carousel slide" data-ride="carousel">

            <!-- Indicators -->
            <ul class="carousel-indicators">
                <li data-target="#demo" data-slide-to="0" class="active"></li>
                <li data-target="#demo" data-slide-to="1"></li>
                <li data-target="#demo" data-slide-to="2"></li>
            </ul>

            <!-- The slideshow -->
            <div class="carousel-inner">
                <template v-for="(banner, index) in banners" >
                    <div :class="['carousel-item', index===0?'active':'']" v-bind:key="banner.id">
                        <img :src="banner.download_url" alt="Los Angeles">
                    </div>
                </template>
            </div>

            <!-- Left and right controls -->
            <a class="carousel-control-prev" href="#demo" data-slide="prev">
                <span class="carousel-control-prev-icon"></span>
            </a>
            <a class="carousel-control-next" href="#demo" data-slide="next">
                <span class="carousel-control-next-icon"></span>
            </a>

        </div>
    </div>
</template>

<script>
    import {mapState} from "vuex";

    export default {
        name: "SlideBanner",
        data() {
            return {}
        },
        computed: {
            /* namespaced: true 이용한 방법 */
            ...mapState('bannersModule', {
                banners(state) {
                    return state.mainBanners.splice(0,3)
                }
            })

            /* namespaced: false 이용한 방법 */
            // ...mapState({
            //     banners(state) {
            //         return state.bannersModule.mainBanners
            //     }
            // })
        },
        created() {
            console.log(this.$store)
            /* namespaced: true 이용한 방법 */
            this.$store.dispatch("bannersModule/setMainBanners")
            /* namespaced: false 이용한 방법 */
            // this.$store.dispatch("setMainBanners")
        }
    }
</script>

<style scoped>
    .carousel-item img {
        width: 100%;
        max-height: 40vw;
    }
</style>