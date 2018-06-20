<template>
<div class="goods">
   <scroll-view :scroll-y="frue" class="menu-wrapp">
       <ul>
           <li  class="menu-item" :class="{'active':changeGoods === item.id}" v-for="(item,index) in goods" :key="index" :data-id="item.id" @click="switchGoods">
               <span class="text border-1px">
                    {{item.name}}
                </span>
           </li>
       </ul>
   </scroll-view>
      <scroll-view :scroll-y="true" class="foods-wrapper" scroll-top="0" :scroll-into-view="whereFood">
       <ul>
           <li v-for="(item,curr) in goods" :key="curr" :data-id="curr" :id="item.id"   @click="selectFood" class="food-list " >
               <h1 class="title">{{item.name}}</h1>
               <ul>
                   <li v-for="(food, index) in item.foods" :key="index" class="food-item  border-1px">
                       <div class="icon">
                           <image :src="food.icon" style="width:114rpx;height:114rpx" />
                       </div>
                       <div class="content">
                           <h2 class="name">{{food.name}}</h2>
                           <p class="desc">{{food.description}}</p>
                           <div class="extra">
                               <span class="count">月售{{food.sellCount}}份</span>
                               <span class="rating">好评率{{food.rating}}%</span>
                           </div>
                           <div class="price">
                               <span class="now">￥{{food.price}}</span>
                               <span v-show="food.oldPrice" class="old">￥{{food.oldPrice}}</span>
                           </div>
                           <div class="cartcontrol-wrapper">
                               <cartcontrol :food="food"></cartcontrol>
                           </div>
                       </div>
                   </li>
               </ul>
           </li>
       </ul>
   </scroll-view>
    <shopcart :select-foods="selectFoods" :delivery-price="seller.deliveryPrice" :min-price="seller.minPrice"></shopcart>
</div>
</template>
<script>
    import shopcart from "../shopcart/shopcart"
    import cartcontrol  from "../cartcontrol/cartcontrol"
export default {
    data() {
        return {
            goods: {},
            seller: {},
            changeGoods: 'hot',
            whereFood: 'hot'
        }
    },
    onLoad() {
    this.classMap = ['decrease','discount','special','invoice','guarantee'];
     wx.request({
        url:'https://www.easy-mock.com/mock/5aded45053796b38dd26e970/sell#!method=get',
        success: (res) => {
          this.goods = res.data.data.goods
          this.seller = res.data.data.seller
        },
        
      })
 
    },
    components: {
        shopcart,
        cartcontrol
    },
    methods: {
        switchGoods(e) {
            const current = e.currentTarget.dataset.id;
            this.changeGoods = current;
            this.whereFood = current;
            console.log(this.changeGoods);
        },
       selectFood(e) {
            console.log(e)
        },
        
    },
    computed: {
        selectFoods() {
            let foods = [];
            this.goods.forEach((good) => {
                good.foods.forEach((food)=>{
                    if(food.count){
                         foods.push(food);
                    }
                })
            });
            return foods
        }
    }

}
</script>

<style lang="stylus" scoped>
  @import "../../common/stylus/mixin";
    .goods
        display flex
        position absoult 
        top 348rpx
        bottom 92rpx
        height 100vh
        overflow hidden
        .menu-wrapp
            flex 0 0 160rpx
            width 160rpx
            background #f3f5f7
            .active
                position relative
                background #ffffff
                z-index 10
                margin-top -2rpx
                font-weight 700
                .text
                    border-none()
            .menu-item
                display table
                height 108rpx
                width 112rpx
                line-height 28rpx
                padding 0 24rpx
                .icon
                    width 32rpx
                    height 32rpx
                    vertical-align top
                    margin-right 4rpx
                    background-size 32rpx 32rpx
                    background-repeat no-repeat
                    &.decrease
                        bg-image('decrease_3')
                    &.discount
                        bg-image('discount_3')
                    &.guarantee
                        bg-image('guarantee_3')
                    &.invoice
                        bg-image('invoice_3')
                    &.special
                        bg-image('special_3')
                .text
                    display table-cell
                    font-size 24rpx
                    width 112rpx
                    border-1px(rgba(7,17,27,.1))
                    vertical-align middle
        .foods-wrapper
            flex 1
            .title
                padding-left 28rpx
                height 52rpx
                line-height 52rpx
                border-left 4rpx solid #d9dde1
                font-size 24rpx
                color rgb(147,153,159)
                background #f3f5f7
            .food-item
                display flex
                margin 36rpx
                padding-bottom 36rpx
                border-1px(rgba(7,17,27,.1))
                &:last-child
                    border-none()
                    margin-bottom 0
                .icon 
                    flex 0 0 114rpx
                    margin-right 20rpx
                .content
                    flex 1
                    .name
                        margin 4rpx 0 16rpx 0
                        font-size 28rpx
                        line-height 28rpx
                        color rgb(7,17,27)
                    .desc, .extra
                        line-height 20rpx
                        font-size 20rpx
                        color rgb(147,153,159)
                    .desc
                        margin-bottom 16rpx
                    .extra
                        .count
                            margin-right 24rpx
                          
                    .price
                        font-weight 700
                        line-height 48rpx
                        vertical-align top
                        .now
                            margin-right 16rpx
                            font-size 28rpx
                            color rgb(240,20,20)
                        .old
                            text-decoration line-through
                            font-size 20rpx
                            color rgb(147,153,159)
                    .cartcontrol-wrapper
                        position absolute 
                        right 0
                        top 0
                        bottom 30rpx
                        margin-top 70rpx

                        
</style>
