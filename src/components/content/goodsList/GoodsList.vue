<template>
  <div class="goods">
    <goods-list-item v-for="(item,index) in goods" :key="index" :goodsItem="item">{{goods}}</goods-list-item>
  </div>
</template>

<script>
import GoodsListItem from "./GoodsListItem.vue"
export default {
  name: 'GoodsList',
  components:{
    GoodsListItem
  },
  props:{
    goods:{
      type:Array,
      default(){
        return []
      }
    }
  },
  data() {
    return {
      
    };
  },

  mounted() {
    
  },

  methods: {
    
  },
};
</script>

<style lang="scss" scoped>
  .goods {
    display: flex;
    // 根据宽度自动决定一行显示几个
    flex-wrap: wrap;
    // 均等分
    justify-content: space-around;
    padding: 2px;
  }
</style>