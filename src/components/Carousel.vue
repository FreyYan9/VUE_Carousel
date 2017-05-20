<template>
    <div class="Carousel" @mouseenter.stop.prevent="clearTimer" @mouseleave.stop.prevent="runTimer">
        <div class="carousel-wrapper">
            <a :href="carouselList[nowIndex].target">
                <transition name='banner-in'>
                    <img v-if="isShow" :src="carouselList[nowIndex].src" alt="">
                </transition>
                <transition name='banner-out'>
                    <img v-if="!isShow" :src="carouselList[nowIndex].src" alt="">
                </transition>
            </a>
        </div>
        <div class="carousel-pages">
            <ul>
                <li v-for="(item, index) in carouselList" :class="{on : index === nowIndex}" @click='goto(index)'></li>
            </ul>
        </div>
        <div class="carousel-around">
            <transition name="fade-left">
                <div class="left" v-show="isShowAround" href="javascript:void(0)"><img @click="goto(prevIndex)" src="../assets/left.png" alt=""></div>
                <!-- <a class="left" v-show="isShowAround" href="javascript:void(0)"><img @click="goto(prevIndex)" src="../assets/left.png" alt=""></a> -->
                <!-- <img class="left" v-show="isShowAround" @click="goto(prevIndex)" src="../assets/left.png" alt=""> -->
            </transition>
            <transition name="fade-right">
                <div class="right" v-show="isShowAround" href="javascript:void(0)"><img @click="goto(nextIndex)" src="../assets/right.png" alt=""></div>
                <!-- <a class="right" v-show="isShowAround" href="javascript:void(0)"><img @click="goto(nextIndex)" src="../assets/right.png" alt=""></a> -->
                <!-- <img class="right" v-show="isShowAround" @click="goto(prevIndex)" src="../assets/right.png" alt=""> -->
            </transition>
        </div>
    </div>
</template>
<script>
export default {
    name: 'Carousel',
    props: {
        carouselList: {
            type: Array,
            default () {
                return []
            }
        }
    },
    data() {
        return {
            nowIndex: 0,
            isShowAround: false,
            isShow: true
        };
    },
    mounted() {
        this.runTimer();
    },
    methods: {
        goto(idx) {
            this.isShow = false;
            setTimeout(() => {
                this.isShow = true;
                this.nowIndex = idx;
            }, 1)
        },
        runTimer() {
            this.isShowAround = false;
            this.timerId = setInterval(() => {
                this.goto(this.nextIndex);
            }, 2000);
        },
        clearTimer() {
            this.isShowAround = true;
            clearInterval(this.timerId);
        }
    },
    computed: {
        prevIndex() {
            if (this.nowIndex === 0) {
                return this.carouselList.length - 1;
            } else {

                return this.nowIndex - 1;
            }
        },
        nextIndex() {
            if (this.nowIndex === this.carouselList.length - 1) {
                return 0;
            } else {

                return this.nowIndex + 1;
            }
        }
    }
}
</script>
<style lang="less" scoped>
.fade-left-enter-active,
.fade-left-leave-active {
    transition: all .5s;
}

.fade-left-enter,
.fade-left-leave-active {
    transform: translateX(-100px);
}

.fade-right-enter-active,
.fade-right-leave-active {
    transition: all .5s;
}

.fade-right-enter,
.fade-right-leave-active {
    transform: translateX(100px);
}

.banner-in-enter-active {
    transition: all .6s;
}

.banner-in-enter {
    transform: translateX(100%);
}

.banner-out-leave-active {
    transition: all .6s;
    transform: translateX(-100%);
}

.Carousel {
    width: 100%;
    min-height: 100%;
    overflow: hidden;
    position: relative;
    .carousel-wrapper {
        width: 100%;
        img {
            width: 100%;
            position: absolute;
            top: 0;
            left: 0;
        }
    }
    .carousel-pages {
        position: absolute;
        bottom: 10px;
        width: 100%;
        text-align: center;
        ul {
            width: auto;
            margin: 0;
            padding: 0;
            li {
                width: 10px;
                height: 10px;
                cursor: pointer;
                border-radius: 50%;
                border: 1px solid #FFF;
                background-color: transparent;
                &.on {
                    background-color: #FFF;
                }
            }
        }
    }
    .carousel-around {
        position: absolute;
        width: 100%;
        top: calc(560 / 2 - 30px);
        left: 0;
        // display: flex;
        // justify-content: space-between;
        .left {
            float: left;
        }
        .right {
            float: right;
        }
        img {
            width: 30px;
            height: 60px;
            padding: 0 30px;
            cursor: pointer;
            // opacity: 1;
        }
    }
}
</style>
