<template>
     <div class="search">
      <div class="search_input">
        <input type="text">
        <div class="word">
          <icon type="search" size="20"></icon>
          <span>搜索</span>
        </div>
      </div>
    </div>
</template>

<script>
export default {

}
</script>

<style lang="less">
.search{
    background-color: #eb4450;
    padding: 20rpx 16rpx;
    .search_input{
        height: 60rpx;
        background-color: #fff;
        width: 100%;
        position: relative;
        border-radius: 8rpx;
       
        .word{
             display: flex;
             align-items: center;
            position: absolute;
            left: 50%;
            top: 50%;
            transform: translate(-50%,-50%);
            color: #c1c1c1;
            text-align: center;
            icon{
             margin-right: 10rpx;
            }
            span{
                margin-bottom: 10rpx;
            }

        }
    }
}
</style>
