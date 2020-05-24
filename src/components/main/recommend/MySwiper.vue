<template>
    <div class="my-swiper">
  <swiper  :options="swiperOption">
    <swiper-slide v-for="(item, index) of swiperList" :key="index">
        <img :src="item.img" class="w100">
    </swiper-slide>
    <div class="swiper-pagination" slot="pagination"></div>
  </swiper>
    </div>
</template>
<script>
import { Swiper, SwiperSlide } from 'vue-awesome-swiper'
import 'swiper/css/swiper.css'
export default {
    props:{
        swiperList:{
            type:Array,
            required:true
        },
        swiperOption:{
        type:Object,
        required:true

       }
    },
    
   components: {
    Swiper,
    SwiperSlide
  },
}
</script>