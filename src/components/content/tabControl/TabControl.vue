<template>
  <div class="tab-control">
    <div @click="tabClick(index)"  v-for="(item,index) in titles" :key="index" class="tab-control-item" :class="{active:index==currentIndex}" >
      <span >{{item}}</span>
    </div>
  </div>
</template>

<script>
export default {
  name: 'TabControl',
  props:{
    titles:{
      type:Array,
      default(){
        return []
      }
    }
  },
  data() {
    return {
      currentIndex:0
    };
  },

  mounted() {
    
  },

  methods: {
    tabClick(index){
      this.currentIndex=index
      this.$emit("tabClick",index)
    }
  },
};
</script>

<style lang="scss" scoped>
  .tab-control{
    display: flex;
    text-align: center;
    background-color: #fff;
    height: 40px;
    line-height: 40px;
    font-size: 15px;
  }
  .tab-control-item{
    flex:1;
  }
  .active{
    color:#ff5777
  }
  .active span{
    border-bottom:3px solid #ff5777;
  }
</style>