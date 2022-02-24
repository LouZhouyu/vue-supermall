<template>
  <div>
    <detail-nav-bar></detail-nav-bar>
    <detail-swiper :top-images="topImages"></detail-swiper>
    <detail-base-info :goods="goods"></detail-base-info>
    <detail-shop :shop="shop"></detail-shop>
    <detail-goods-param :paramInfo="paramInfo"></detail-goods-param>
  </div>
</template>

<script>
import DetailNavBar from './childComps/DetailNavBar'
import DetailSwiper from './childComps/DetailSwiper'
import DetailBaseInfo from './childComps/DetailBaseInfo'
import DetailShop from './childComps/DetailShop'
import DetailGoodsParam from './childComps/DetailGoodsParam'
import {getDetail,GoodsInfo,Shop,GoodsParam} from 'network/detail'

export default {
  name: 'Detail',
  data() {
    return {
      iid:null,
      topImages:[],
      goods: {},
      shop: {}
    }
  },
  created(){
    this.iid = this.$route.params.id
    getDetail(this.iid).then(res =>{
      const data = res.result;
      console.log(data);
      this.topImages = data.itemInfo.topImages,
      this.goods = new GoodsInfo(data.itemInfo,data.columns,data.shopInfo.services)
      console.log(this.goods);
      this.shop = new Shop(data.shopInfo)
      this.paramInfo = new GoodsParam(data.itemParams.info,data.itemParams.rule)
    })
  },
  mounted() {
    
  },
  components:{
    DetailNavBar,
    getDetail,
    DetailSwiper,
    GoodsInfo,
    DetailBaseInfo,
    GoodsParam,
    Shop,
    DetailShop,
    DetailGoodsParam
  },
  methods: {
    
  },
};
</script>

<style lang="scss" scoped>
  #detail{
    position: relative;
    z-index: 9;
    background-color: #fff;
  }
</style>