<template>
  <swiper>
    <swiper-item class="swiper-item" v-for="(item,index) in topImages" :key="index">
      <img :src="item" alt="">
    </swiper-item>
  </swiper>
</template>

<script>
import {Swiper,SwiperItem} from 'components/common/swiper'

export default {
  name: 'DetailSwiper',
  data() {
    return {
      
    };
  },
  props:{
    topImages:{
      type:Array,
      default(){
        return []
      }
    }
  },
  mounted() {
    
  },
  components:{
    Swiper,
    SwiperItem
  },
  methods: {
    
  },
};
</script>

<style lang="scss" scoped>
  .swiper-item{
    height: 300px;
    overflow: hidden;
  }
</style>