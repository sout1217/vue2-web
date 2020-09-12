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
                <div class="carousel-item active">
                    <img :src="banners[0].download_url" alt="Los Angeles">
                </div>
                <div class="carousel-item">
                    <img :src="banners[1].download_url" alt="Chicago">
                </div>
                <div class="carousel-item">
                    <img :src="banners[2].download_url" alt="New York">
                </div>
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
    import banners from "../api/banners";

    export default {
        name: "SlideBanner",
        data() {
            return {
                banners: []
            }
        },
        created() {
            banners.getMainSlideBanners()
                .then(res => {
                    this.banners = [].concat(res.data) // 깊은 복사 (deep copy)
                    // this.banners = res.data 는 얕은 복사 (shallow copy) 이다
                    // 때문에, res.data.push('add new data') 이와 같이 추가 하는 경우 this.banners 까지 영향을 미친다
                    // 반면 깊은 복사인 [].concat(res.data) 는 push 를 하여도 영향을 미치지 않는다
                })
        }
    }
</script>

<style scoped>
    .carousel-item img {
        width: 100%;
        max-height: 40vw;
    }
</style>