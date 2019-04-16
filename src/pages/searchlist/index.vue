<template>
  <div>
    <div class="mytop">
    <!-- 头部 -->
   <div class="search">
      <div class="search-input">
        <input type="text" v-model="query">
        <div class="word">
           <icon type="search" size="20"></icon>
        </div>
      </div>
   </div>

   <!-- 顶部tab -->
   <div class="tab">
     <div @click="seachindex = index" :class="{active:seachindex==index}" v-for="(item,index) in tabList" :key="index">{{item}}</div>
   
   </div>
   </div>
   <!-- 中间商品列表内容 -->
   <div class="goodsList">
     <div class="item" v-for="(item,index) in  goodsList" :key="index">
        <div class="box">
     <div class="left">
       <image :src="item.goods_small_logo"></image>
     </div>
     <div class="right">
       <div class="word">
        {{item.goods_name}}
       </div>
       <div class="price">
            <span>￥</span>
            <span>{{item.goods_price}}</span>
       </div>
      
     </div>
   </div>
     </div>
     
   </div>
   
  </div>
</template>

<script>
// 导入request
import request from '../../utils/request.js'
export default {
  data(){
    return{
      seachindex:0,
     tabList:['综合','销量','价格'],
     goodsList:[],
     query:'',
     pagenum:1,
     pagesize:10
     
    }
  },
  methods: {
    async getDataList(){
      //根据关键字查询
      var url = 'https://itjustfun.cn/api/public/v1/goods/search'
       let res = await request.get(url,{
         query:this.query,
         pagenum:this.pagenum,
         pagesize:this.pagesize
       })
       console.log(res);
       if(this.goodsList.length == 0){
         this.goodsList = res.data.data.goods
       }else{
         this.goodsList = this.goodsList.concat(res.data.data.goods)
       }
       
    }
  },
  mounted() {
    //接受参数
    this.query = this.$root.$mp.query.query
    // 重新渲染页面
    this.getDataList()
  },

  // 上拉事件
  onReachBottom(){
    this.pagenum = this.pagenum + 1
    this.getDataList()
  }
}
</script>

<style lang="less">
@import './index.less';
</style>
