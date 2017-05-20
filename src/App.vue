<template>
    <div id="app">
        <div class="carousel-container">
            <Carousel :carouselList="carouselList"></Carousel>
        </div>
        <div class="carousel-container">
            <Carousel1 :carouselList="carouselList"></Carousel1>
        </div>
    </div>
</template>
<script>
import Carousel from 'com/Carousel.vue';
import Carousel1 from 'com/Carousel1.vue';

export default {
    name: 'app',
    data() {
        return {
            msg: 'Welcome to Your Vue.js App',
            carouselList: [{
                target: '',
                src: 'http://p0.so.qhimgs1.com/t01bf0af1a4064e7eac.jpg'
            }, {
                target: '',
                src: 'http://p2.so.qhimgs1.com/t019f302477e4ec891e.jpg'
            }, {
                target: '',
                src: 'http://p0.so.qhmsg.com/t0131fb27eb87dd0c45.jpg'
            }, {
                target: '',
                src: 'http://p0.so.qhimgs1.com/t01da86d5638222b66c.jpg'
            }, {
                target: '',
                src: 'http://p2.so.qhmsg.com/t0117e1a4b20cb09017.jpg'
            }]
        }
    },
    components: {
        Carousel,
        Carousel1
    }


}
</script>
<style lang="less">
#app {
    font-family: 'Avenir', Helvetica, Arial, sans-serif;
    -webkit-font-smoothing: antialiased;
    -moz-osx-font-smoothing: grayscale;
    text-align: center;
    color: #2c3e50;
    margin-top: 60px;
    margin-bottom: 60px;
    .carousel-container {
        width: 1200px;
        height: 560px;
        margin: 80px auto;
    }
}

h1,
h2 {
    font-weight: normal;
}

ul {
    list-style-type: none;
    padding: 0;
}

li {
    display: inline-block;
    margin: 0 10px;
}

a {
    color: #42b983;
}
</style>
