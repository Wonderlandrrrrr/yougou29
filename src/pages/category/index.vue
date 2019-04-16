<template>
<div>
<!-- 头部区域 -->
<div class="mytop">
 <myheader></myheader>
</div>
  
   <!-- 内容区域 -->
   <div class="content">
     <!-- 左侧区域 -->
     <div class="nav">
       <div class="nav-item" @click="setRightData(index)" :class="{active:selectedIndex == index}" v-for="(item,index) in dataList" :key="index" >{{item.cat_name}}</div>
       
     </div>
     <!-- 右测区域 -->
     <div class="goods">
       <!-- 右侧顶部图片 -->
       <image class="topimg" src="https://img.alicdn.com/simba/img/TB1AhMzMAvoK1RjSZFNSuwxMVXa.jpg" mode="aspectFill"></image>
       <!-- 右侧下部内容 -->
       <div class="list" v-for="(item,index) in rightList" :key="index">
         <div class="title">
           <span>/</span>{{item.cat_name}}<span>/</span>
         </div>
         <div class="list-item">
           <a :href="'/pages/searchlist/main?query='+subitem.cat_name" class="item" v-for="(subitem,subindex) in item.children" :key="subindex">
              <image :src="'https://itjustfun.cn/' + subitem.cat_icon" mode="aspectFill"></image>
           <span>{{subitem.cat_name}}</span>
           </a>
         
         </div>
       </div>
       
     </div>
   </div>
</div>
  
</template>

<script>
// 引入request
import request from '../../utils/request.js'
// 引入头部公共区域
import myheader from "../../components/myheader.vue"


export default {
data(){
  return{
       dataList:[],
      selectedIndex: 0,
      rightList:[]
  }
},
methods: {
  setRightData(index){
    this.selectedIndex=index
    // 根据index得到当前点击的左侧菜单
    this.rightList = this.dataList[index].children;
    conse.log( this.rightList)
    
  }
},
//获取左侧菜单
 async mounted() {
   var url ='https://itjustfun.cn/api/public/v1/categories'
   let res = await request(url)
   console.log(res);
   this.dataList = res.data.data
  //  打开页面给右侧赋值
  this.rightList = this.dataList[this.selectedIndex].children
  
},
components:{
   myheader
  }

}
</script>

<style lang="less">
@import "./index.less";

</style>
