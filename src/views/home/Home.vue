<template>
  <!-- <div id="home"> -->
    <!-- <nav-bar class="home-nav"><div slot="center">买衣服</div></nav-bar>
    <span>
      <home-swiper :banners="banners"></home-swiper>
    </span>
    <recommend-view :recommends="recommends"></recommend-view>
    <feature-view></feature-view>
    <tab-control :titles="['流行','新款','精选']" @tabsClick="tabsClick" class="tab-control"></tab-control>
    <goods-list :goods="showGoods"></goods-list> -->
    <!-- </div> -->
  <div id="home" class="wrapper">
    <nav-bar class="home-nav"><div slot="center">购物街</div></nav-bar>
    <scroll class="content"
            ref="scroll"
            :probe-type="3"
            @scroll="contentScroll"
            :pull-up-load="true"
            @pullingUp="loadMore">
      <home-swiper :banners="banners"/>
      <recommend-view :recommends="recommends"/>
      <feature-view/>
      <tab-control class="tab-control"
                   :titles="['流行', '新款', '精选']"
                   @tabClick="tabClick"
                   ref="tabControl"/>
      <goods-list :goods="showGoods"/>
    </scroll>
    <back-top @click.native="backClick" v-show="isShowBackTop"></back-top>
  </div>
</template>

<script>
import HomeSwiper from "./childComps/HomeSwiper"
import RecommendView from "./childComps/RecommendView"
import FeatureView from "./childComps/FeatureView"

import NavBar from "components/common/navbar/NavBar"
import TabControl from "components/content/tabControl/TabControl"
import GoodsList from "components/content/goodsList/GoodsList"
import Scroll from 'components/common/scroll/Scroll'
import BackTop from "components/content/backTop/BackTop"

import {getHomeMultidata} from "network/home"
import {getHomeGoods} from "network/home"


  export default {
    name: "Home",
    components: {
      NavBar,
      HomeSwiper,
      RecommendView,
      FeatureView,
      TabControl,
      getHomeGoods,
      GoodsList,
      BackTop,
      Scroll,
    },
    data() {
      return {
        banners:[],
        recommends:[],
        goods:{
          'pop':{
            page:0,
            list:[]
          },
          'new':{
            page:0,
            list:[]
          },
          'sell':{
            page:0,
            list:[]
          },
        },
        currentType: 'pop',
        isShowBackTop: false,
        tabOffsetTop: 0
      }
    },
    created() {
      // 1.请求多个数据
      this.getHomeMultidata()
      // 2.请求商品数据
      this.getHomeGoods("pop")
      this.getHomeGoods("new")
      this.getHomeGoods("sell")
      // 3.赋值
      this.tabOffsetTop = this.$refs.tabControl
    },

    computed:{
      showGoods(){
        return this.goods[this.currentType].list
      }
    },

    mounted(){
    // 所有的组件都有一个属性$el,用于获取组件的元素
      setTimeout(() =>{
        // console.log(this.$refs.tabControl.$el.offsetTop);
      },100)
    },

    methods:{
      // 网络请求
      getHomeMultidata(){
        getHomeMultidata().then(res =>{
          this.banners = res.data.banner.list
          this.recommends = res.data.recommend.list
        })
      },
      getHomeGoods(type){
        const page=this.goods[type].page+1
        getHomeGoods(type,page).then(res =>{
        // console.log(res.data);
          this.goods[type].list.push(...res.data.list)
          this.goods[type].page+=1
          this.$refs.scroll.finishPullUp()
        })
      },
      // 事件监听
      tabClick(index){
        // console.log(index);
        switch(index){
          case 0:
            this.currentType='pop'
            break
          case 1:
            this.currentType='new'
            break
          case 2:
            this.currentType='sell'
            break
        }
      },
      backClick(){
        this.$refs.scroll.scrollTo(0,0)
      },
      contentScroll(position) {
        this.isShowBackTop = (-position.y) > 1000
      },
      loadMore() {
        this.getHomeGoods(this.currentType)
      },
    }
  }
</script>

<style >

  /* .home-nav{
    background-color: #ff5777;
    color:white;
    position: sticky;
    top: 0;
    z-index: 10;
  }
  .tab-control{
    position: sticky;
    top: 44px;
    z-index: 10;
  } */
   #home {
    /*padding-top: 44px;*/
    height: 100vh;
    position: relative;
  }

  .home-nav {
    background-color: var(--color-tint);
    color: #fff;

    position: fixed;
    left: 0;
    right: 0;
    top: 0;
    z-index: 9;
  }
/* sticky属性仅在以下几个条件都满足时有效：
    父元素不能overflow:hidden或者overflow:auto属性，或者body height:100%
    必须指定top、bottom、left、right4个值之一，否则只会处于相对定位
    父元素的高度不能低于sticky元素的高度
*/
  .tab-control {
    position: sticky;
    top: 44px;
    z-index: 9;
  }
/* 之前是content  现在改成wrapper,但老师的代码可以用,因为有overflow，所以tab-control的sticky不能用
  https://blog.csdn.net/qiqi_77_/article/details/79361413
*/
  .wrapper {
    overflow: hidden;
    position: absolute;
    top: 20px;
    bottom: 49px;
    left: 0;
    right: 0;
  }
</style>
