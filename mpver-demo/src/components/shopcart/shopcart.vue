<template>
    <div class="shopcart">
        <div class="content">
            <div class="content-left">
                <div class="logo-wrapper">
                    <div class="logo" :class="{'highlight': totalCount>0}">
                       <i class="iconfont icon-gouwuche icon" :class="{'highlight': totalCount>0}"></i>
                    </div>
                    <div class="num" v-show="totalCount>0">{{totalCount}}</div>
                </div>
                <div class="price" :class="{'highlight': totalCount>0}">￥{{totalPrice}}</div>
                <div class="desc">另需配送费{{deliveryPrice}}元</div>
            </div>
            <div class="content-right">
                <div class="pay" :class="{'enough':totalPrice>=minPrice}">
                    {{payDesc}}
                </div>
            </div>
        </div>
     
        
        <div class="shopcart-list" v-show="listShow">
            <div class="list-header">
                <h1 class="title">购物车</h1>
                <span class="empty">清空</span>
            </div>
            <!-- <div class="list-content">
                <ul>
                    <li class="food" v-for="(food,index) in selectFoods" :key="index"></li>
                    <span class="name">{{food.name}}</span>
                    <div class="price">
                        <span>￥{{food.price*food.count}}</span>
                    </div>
                    <div class="cartcontrol-wrapper">
                        <cartcontrol :food="food"></cartcontrol>
                    </div>
                </ul>
            </div> -->
        </div>
    </div>
</template>

<script>
    import cartcontrol  from "../cartcontrol/cartcontrol"

export default {
    data() {
        return {
             flod:true,
             balls: [
                {
                 show: false
                },
                {
                 show: false
                },
                {
                 show: false
                },
                {
                 show: false
                },{
                 show: false
                }
             ]
        }
    },
     props: {
         selectFoods: {
             type: Array,
             default() {
                 return [
                     {  
                        price: 0,
                        count: 0
                     }
                 ];
             }
         },
         deliveryPrice: {
             type: Number,
             default: 0
         },
         minPrice: {
             type:  Number,
             default: 0
         },
        
    },
     components: {
       
        cartcontrol
    },
    computed: {
        totalPrice() {
            let total = 0;
            this.selectFoods.forEach((food) => {
                total += food.price * food.count;
            });
            return total
        },
        totalCount() {
            let count = 0;
            this.selectFoods.forEach((food) => {
                count += food.count
            });
            return count
        },
        payDesc() {
            if(this.totalPrice === 0) {
                return `￥${this.minPrice}元起送`
            }else if(this.totalPrice<this.minPrice){
                let diff = this.minPrice-this.totalPrice
                return  `还差￥${diff}元起送`
            }else{
                return '去结算'
            }
        },
        payClass() {
            if(this.totalPrice<this.minPrice) {
                return 'not-enough'
            }else{
                return 'enough'
            }
        },
        listShow(){
            if(!this.totalCount) {
                this.flod = true;
                return false;
            }
            let show = !this.flod;
        }
    }
}
</script>

<style lang="stylus" scoped>
 @import "../../common/fonts/iconfont.css";
    .shopcart
        position fixed
        z-z-index 99
        left 0
        bottom 0
        width 100%
        height 96rpx
        .content
            display flex
            background #141d27
            font-size 0
            .content-left
                flex 1
                .logo-wrapper
                    display inline-block
                    position relative
                    top -20rpx
                    margin 0 24rpx
                    padding 12rpx
                    height 112rpx
                    width 112rpx
                    box-sizing border-box
                    vertical-align top
                    border-radius 50%
                    background #141d27
                    .logo
                        width 100%
                        height 100%
                        border-radius 50%
                        background #2b343c
                        text-align center
                        &.highlight
                            background rgb(0,160,220)
                        .icon
                            line-height 88rpx
                            font-size 48rpx
                            color #80858a
                            &.highlight
                                color #ffffff
                    .num
                        position absolute
                        top 0
                        right 0
                        width 48rpx
                        height 32rpx
                        line-height 32rpx
                        text-align center
                        border-radius 32rpx
                        font-size 18rpx
                        font-weight 700
                        color #ffffff
                        background rgb(240,20,20)
                        box-shadow 0 8rpx 16rpx 0 rgba(0,0,0,.4)
                .price
                    display inline-block
                    font-size 32rpx
                    vertical-align top
                    line-height 48rpx
                    margin-top 24rpx
                    box-sizing border-box
                    padding-right 24rpx
                    border-right  1px solid rgba(255,255,255,.1)
                    font-size 32rpx
                    font-weight 700
                    color rgba(255,255,255,.4)
                    &.highlight
                        color #ffffff
                .desc
                    display inline-block
                    vertical-align top
                    line-height 48rpx
                    margin 24rpx 0 0 24rpx
                    line-height 48rpx
                    color rgba(255,255,255,.4)
                    font-size 20rpx
            .content-right
                flex 0 0 210rpx
                width 210rpx
                .pay
                    text-align center
                    height 96rpx
                    line-height 96rpx
                    font-size 24rpx
                    color rgba(255,255,255,.4)
                    font-weight 700
                    background #2b333b
                    &.enough
                        background #00b43c
                        color #ffffff
        

</style>
