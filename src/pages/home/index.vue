<template>
  <div>
    <!-- 头部区域 -->
  
     <myheader></myheader>
     <!-- 轮播图 -->
  <swiper class="loop" circular indicator-dots autoplay>
      <block v-for="(item, index) in imgList" :key="index">
        <swiper-item>
          <image :src="item.image_src" mode="aspectFill" />
        </swiper-item>
      </block>
    </swiper>

    <!-- 导航 -->
    <div class="nav">
      <div class="navphp" v-for="(item,index) in cateList" :key="index">
         <image :src="item.image_src" mode="aspectFit"></image>
      </div>
      
    </div>
    <!-- 楼层区 -->
    <div class="floor" v-for="(item,index) in floorList" :key="index">
      <div class="title">
        <image :src="item.floor_title.image_src" mode="aspectFit"></image>
      </div>
      <div class="cont">
        <div class="left">
          <image :src="item.product_list[0].image_src" mode="aspectFit"></image>
        </div>
        <div class="right">
          <!-- 遍历出来有5张图片   用v-if如果下标=0不显示,下标不等于0显示 -->
          <image v-if="subindex !=0" v-for="(subitem,subindex) in item.product_list" :key="subindex" :src="subitem.image_src" mode="aspectFit"></image>
          
        </div>
      </div>
    </div>

</div>
</template>
 
 

<script>
// 引入头部公共区域
import myheader from "../../components/myheader.vue"
// 导入封装的request
import request from "../../utils/request.js";
export default {
  data() {
    return {
      //轮播图
      imgList: [],
      //导航
      cateList:[],
      // 楼层区左边图片
      floorList:[]
     



    };
  },
  // 请求页面中的数据
  async mounted() {
    // 发送请求
    var url1 = "https://itjustfun.cn/api/public/v1/home/swiperdata";
    var reslunbo = await request(url1);
    // 解构赋值
    var { data } = reslunbo.data;
    this.imgList = data;
    //console.log(this.imgList);


    // 导航请求的数据
     var url2 = "https://itjustfun.cn/api/public/v1/home/catitems";
     var resCate = await request(url2);
     this.cateList = resCate.data.data
     //console.log(res);


    //  发送请求楼层区域
     var url3 = "https://itjustfun.cn/api/public/v1/home/floordata";
     var rel = await request(url3);
     //console.log(rel);
     this.floorList = rel.data.data
     console.log(this.floorList);
     
  },

  components:{
   myheader
  }

};
</script>


<style lang="less">
// 引用index: less;
@import "./index.less";
</style>
