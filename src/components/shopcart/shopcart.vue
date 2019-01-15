<template>
    <div>
     <div class="shopcart">
        <div class="content" @click="toggleList">
            <div class="content-left">
                <div class="logo-wrapper" :class="{'highlight': totalCount>0}">
                    <div class="logo" :class="{'highlight': totalCount>0}">
                       <i class="iconfont icon-gouwuche icon"  :class="{'highlight': totalCount>0}"></i>
                    </div>
                    <div class="num" v-show="totalCount>0">{{totalCount}}</div>
                </div>
                <div class="price" :class="{'highlight': totalCount>0}">￥{{totalPrice}}</div>
                <div class="desc">另需配送费{{deliveryPrice}}元</div>
            </div>
            <div class="content-right">
                <div class="pay" :class="{'enough':totalPrice>=minPrice}" @click.stop="toPay">
                    {{payDesc}}
                </div>
            </div>
        </div>
        
        <div class="shopcart-list" v-show="listShow">
             <notice></notice>
            <div class="list-header">
                <div class="delete">
                <span class="image"></span>
                <span class="empty" @click="empty">清空购物车</span>
                </div>
            </div>
             <scroll-view :scroll-y="true" class="list-content">
                <ul>
                    <li class="food" v-for="(food,index) in selectFoods" :key="index">
                        <span class="name">{{food.name}}</span>
                        <div class="price">
                            <span>￥{{food.price*food.count}}</span>
                        </div>
                        <div class="cartcontrol-wrapper">
                            <cartcontrol :food="food"></cartcontrol>
                        </div>
                    </li>
                </ul>
             </scroll-view>
        </div>
     </div>
     <div class="list-mask" v-show="listShow" @click="toggleList"></div>
    </div>   
</template>

<script>
    import cartcontrol  from "../cartcontrol/cartcontrol"
    import notice  from "../notice/notice"
     
export default {
   
    data() {
        return {
             flod:true,
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
    methods: {
        toggleList() {
            if(!this.totalCount) {
                return;
            }
            this.flod =!this.flod;
        },
        empty() {
            this.selectFoods.forEach((food)=>{
                food.count=0;
            })
        },
        toPay() {

            try {
                wx.setStorageSync('selectFoods', this.selectFoods)
            } catch (e) {   
                console.log(e) 
            }
            wx.switchTab({
            url: '/pages/order/main',
        })
        }
     
    },
     components: {
        cartcontrol,
        notice
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
        listShow() {
            if (!this.totalCount) {
                this.flod = true;
                return false
            }
            let show = !this.flod;
            return show;
        }
    }
}
</script>

<style lang="stylus" scoped>
 @import "../../common/fonts/iconfont.css";
   @import "../../common/stylus/mixin";
    .shopcart
        position fixed
        z-index 999
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
                            background #ffd161
                            transform scale(1.2)
                        .icon
                            line-height 88rpx
                            font-size 48rpx
                            color #80858a
                            &.highlight
                                color #000
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
                        background  #ffd161
                        color #000
        .shopcart-list
            position absolute
            top  0
            left 0
            z-index -1
            width 100%
            background #ffffff
            transform translate3d(0,-100%,0)
            .list-header
                height 80rpx
                line-height 80rpx
                padding 0 36rpx
                background #f4f4f4
                .delete
                    float right
                    display flex
                    align-items center
                    justify-content center
                    .image
                        display inline-block
                        width 35rpx
                        height 35rpx
                        background url(./delete.png)
                        background-repeat no-repeat
                        background-size 100% 100%  
                    .empty
                        font-size 30rpx
                        padding-left 10rpx
                        color #666
            .list-content
                padding 0 36rpx
                max-height 434rpx
                overflow hidden
                background #ffffff
                .food
                    position relative
                    padding 46rpx 0
                    box-size border-box
                    border-1px(rgba(rgba(7,17,27,.1)))
                    .name
                        line-height 48rpx
                        font-size 28rpx
                        color #333
                    .price
                        position absolute
                        right 300rpx
                        bottom 46rpx
                        line-height 48rpx
                        font-size 28rpx
                        color #333
                        font-weight 700
                    .cartcontrol-wrapper
                        position absolute
                        right 40rpx
                        bottom 35rpx
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
