<template>
<div>
<div class="goods">
   <scroll-view :scroll-y="true" class="menu-wrapp">
       <ul>
           <li  class="menu-item" :class="{'active':changeGoods === item.id}" v-for="(item,index) in goods" :key="index" :data-id="item.id"
            @click="switchGoods">
               <span class="text border-1px">
                    {{item.name}}
                </span>
           </li>
       </ul>
   </scroll-view>
      <scroll-view :scroll-y="true" class="foods-wrapper"  @scroll="goodsScrollAct" :scroll-into-view="whereFood">
       <ul>
           <li v-for="(item,id) in goods" :key="id" :data-id="id" :id="item.id"  class="food-list " >
               <h1 class="title">{{item.name}}</h1>
               <ul>
                   <li v-for="(food, index) in item.foods" :key="index" :data-id="index"  @click="selectFood(food,event)" class="food-item  border-1px">
                      
                       <div class="icon">
                           <image :src="food.icon" style="width:114rpx;height:114rpx" />
                       </div>
                       <div class="content">
                           <h2 class="name">{{food.name}}</h2>
                           <p class="desc">{{food.description}}</p>
                           <div class="extra">
                               <span class="count">月售{{food.sellCount}}</span>
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
<div class="food border-1px" v-show="foodFlg">
    <div class="icon">
        <image :src="selectedFood.image" style="width:670rpx;height:500rpx" />
    </div>
    <div class="content">
        <div class="extra">
            <h2 class="name">{{selectedFood.name}}</h2>
            <div class="desc">
                <span class="count">月售{{selectedFood.sellCount}}</span>
                <span class="rating">好评率{{selectedFood.rating}}%</span>
            </div>
        </div>
        <div class="price">
            <span class="now">￥{{selectedFood.price}}</span>
            <div class="cartcontrol-wrapper">
                <cartcontrol :food="selectedFood"></cartcontrol>
            </div>
        </div>
       
    </div>
    <div class="close" @click="close">
        <span class="text">x</span>
    </div>
</div>
<div class="list-mask" v-show="foodFlg" @click="selectFood"></div>
</div>
</template>
<script>
    import shopcart from "../shopcart/shopcart"
    import cartcontrol  from "../cartcontrol/cartcontrol"
    import fly from '@/utils/fly'
export default {
    data() {
        return {
            goods: [],
            seller: {},
            changeGoods: 'hot',
            whereFood: 'hot',
            foodFlg: false,
            selectedFood: {}
        }
    },
    onLoad() {
        this.getList();
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
        },
       selectFood(food,event) {
           this.selectedFood = food;
           this.foodFlg=true;
        },
        close() {
            this.foodFlg = false
        },
        goodsScrollAct(e) {
         
            
            var height =  e.mp.detail.scrollHeight;
            
            const scrollTop = e.mp.detail.scrollTop
         
            console.log(scrollTop)
        }
        
    },
   computed: {
        selectFoods() {
            let foods = [];
            if(!this.goods.length){
                return;
            }
            this.goods.forEach((good) => {
                good.foods.forEach((food)=>{
                    if(food.count){
                         foods.push(food);
                    }
                })
            });
            return foods
        },
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
            background #f7f8f9
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
    .food
        position fixed
        z-index 99999
        margin  auto
        left 0
        right 0
        top 0
        bottom 0
        width 670rpx
        height 840rpx 
        .content
            height 210rpx
            width 100%
            box-sizing border-box
            .extra
                display flex
                flex-direction column
                justify-content center
                padding-left 16rpx
                height 120rpx
                background #fff
                .name 
                    display block
                    font-size 30rpx
                    line-height 30rpx
                    color #333333
                .desc
                    padding-top 18rpx
                    .count, .rating
                        font-size 23rpx
                        line-height 23rpx
                        color #8c8c8c
                    .rating
                       
                        padding-left 30rpx 
            .price
                height 90rpx
                background #fafafa
                box-sizing border-box
                line-height 90rpx
                .now
                    padding-left 30rpx
                    font-size 40rpx
                    color red
                .cartcontrol-wrapper
                    float right
        .close
            margin-top 40rpx
            margin-left auto
            margin-right auto 
            width 80rpx
            height 80rpx
            line-height 80rpx
            text-align center
            background #3d3d3d
            border-radius 50%
            .text
                font-size 50rpx
                line-height 30rpx
                color #ffffff

    .list-mask
        position fixed
        top 0
        left 0
        width 100%
        height 100%
        z-index  100
        background #666666
        opacity .7







                        
</style>
