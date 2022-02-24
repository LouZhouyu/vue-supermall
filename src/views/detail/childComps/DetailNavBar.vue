<template>
  <div>
    <nav-bar>
      <div slot="left" class="back" @click="backClick">
        <img src="~assets/img/common/back.svg" alt="">
      </div>
      <div slot="center" class="title">
        <div @click="titleClick(index)" v-for="(item,index) in titles" :key="index" :class="{active:index=== currentIndex}" class="title-item">{{item}}</div>
      </div>
    </nav-bar>
  </div>
</template>

<script>
import NavBar from 'components/common/navbar/NavBar'
export default {
  name: 'DetailNavBar',
  components:{
    NavBar
  },
  data() {
    return {
      titles:['商品','参数','评论','推荐'],
      currentIndex:0
    };
  },

  mounted() {
    
  },

  methods: {
    titleClick(index){
      this.currentIndex=index
    },
    backClick(){
      this.$router.back()
    }
  },
};
</script>

<style lang="scss" scoped>
  .title{
    display: flex;
    font-size: 13px;
  }
  .title-item{
    flex:1
  }
  .active{
    color: #ff5777;
  }
  .back img{
    margin-top: 10px;
  }
</style>