<template>
    <div class="order">
        <div class="empty" v-if="isShow">
          <div class="image">
            <image src="/static/images/orderImg.png"/>
          </div>
          <div class="order" @click="toIndex">
             <span class="text">立即下单</span>
          </div>
         
        </div>
      <scroll-view class="container" :scroll-y="true">
        <div class="orderList" v-for="(item,index) in orderList" :key="index">
          <div class="order-title">
            <div class="order-title-restaurantName">
              <span class="name">{{item.name}}</span>
             <span class="iconfont icon-icon icon"></span>
            </div>
            <div class="order-title-state">商家已接单</div>
          </div>
          <div class="order-content">
            <image class="order-content-restaurantImg" :src="item.icon"/>
            <div class="order-content-info">
              <div class="order-content-info-price">￥ {{item.price}}</div>
              <div class="order-content-info-howToDistribute">美团小助手提供服务</div>
            </div>
          </div>
            <div class="order-desc">共{{item.count}}件商品，实付<span style="font-weight:700;">￥ {{item.count*item.price}}</span></div>
          <div class="order-footer">
            <div class="order-footer-orderAgain">再来一单</div>
            <div class="order-footer-goToComment">去评论</div>
          </div>
        </div>
      </scroll-view>
    </div>
</template>

<script>
   import util from '@/utils/util'
export default {
    data() {
        return {
             orderList:[],
             isShow: true
        }
    },
    onShow(){
       
         try {
            var value = wx.getStorageSync('selectFoods')
            if (value) {
              this.isShow = false;
              this.orderList=value;
            }
          } catch (e) {
            console.log(e)
          };

         
    },
    methods: {
      toIndex() {
          wx.switchTab({
            url: '/pages/home/main',
          })
        
      }

    }
}
</script>

<style lang="stylus" scoped>
  .empty
    display flex
    flex-direction column
    justify-content center
    align-items center
    margin-top 25%
    .order
      height 68rpx
      width 240rpx
      background-color #ffd300
      text-align center
      margin-top 40rpx
      line-height 68rpx
      border-radius 5rpx

  .container
    height: 100%
    .orderList
      width 100%
      padding 15rpx
      border 100rpx 0
      border-style solid
      border-color #ECECEC
      .order-title
        width 100%
        height 70rpx
        line-height 70rpx
        border-bottom 1rpx solid #ECECEC
        .order-title-restaurantName
          width 200rpx
          float left
          height 100%
          font-size 30rpx
          .name 
            padding-right 10rpx
          .icon
            color #b4b4b4
        .order-title-state
          width 200rpx
          float right
          color #ffc648
          margin-right -15rpx
          font-size 28rpx
      .order-content
        height 250rpx
        display flex
        align-items center
        .order-content-restaurantImg
          width 125rpx
          height 125rpx
        .order-content-info
          font-size 25rpx
          flex 1
          display flex
          flex-direction column
          .order-content-info-price,.order-content-info-howToDistribute
            height 42rpx
            line-height 42rpx
            margin-left 30rpx
          .order-content-info-price
            color: red
            font-size: 30rpx
      .order-desc
        float right 
        font-size 30rpx
        width 335rpx
        margin-bottom 40rpx
        line-height 30rpx
        margin-right 10rpx
      .order-footer
        width 100%
        height 90rpx
        display flex
        justify-content flex-end
        font-size 28rpx
        .order-footer-goToComment,.order-footer-orderAgain
          margin-top 15rpx
          margin-right: 40rpx
          height 70rpx
          line-height 70rpx
          width 200rpx
          text-align center
          border 1rpx solid #ECECEC
        .order-footer-orderAgain
          margin-right 20rpx
        .order-footer-goToComment
          background #FFD161
        
</style>
