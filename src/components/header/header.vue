<template>
    <div class="header">
        <div class="content-wrapper">
            <div class="avatar">
                <image :src="seller.avatar" />
            </div>
           <div class="content">
               <div class="title">
                   <span class="brand"></span>
                   <span class="name">{{seller.name}}</span>
               </div>
                <div class="description">{{seller.description}}/{{seller.deliveryTime}}分钟送达
                </div>
                <div v-if="seller.supports" class="support">
                    <span class="icon decrease" :class="classMap[seller.supports[0].type]"></span>
                    <span class="text">{{seller.supports[0].description}}</span>
                </div>
           </div>
           <div v-if="seller.supports" class="support-count" @click="showDetail">
               <span class="count">{{seller.supports.length}}个</span>
               <i class="iconfont icon-icon icon"></i>
           </div>
        </div>
        <div class="bulletin-wrapper" @click="showDetail">
            <span class="bulletin-title"></span><span class="bulletin-text">{{seller.bulletin}}</span>
            
        </div>
        <div class="background">
            <image :src="seller.avatar" width="100%" height="100%"/>
        </div>
        <div v-show="detailShow" class="detail" >
            <div class="detail-wrapper clearfix">
                <div class="detail-main">
                   <h1 class="name">{{seller.name}}</h1>
                   <div class="star-wrapper">
                       <star :size="48" :score="seller.score"></star>
                   </div>
                   <div class="title">
                       <div class="line"></div>
                       <div class="text">优惠信息</div>
                       <div class="line"></div>
                   </div>
                   <ul v-if="seller.supports" class="supports">
                       <li class="support-item" v-for="(item,index) in seller.supports" :key="index">
                           <span class="icon decrease" :class="classMap[seller.supports[index].type]"></span>
                            <span class="text">{{seller.supports[index].description}}</span>
                       </li>
                   </ul>
                   <div class="title">
                       <div class="line"></div>
                       <div class="text">商家公告</div>
                       <div class="line"></div>
                   </div>
                   <div class="bulletin">
                       <p class="content">{{seller.bulletin}}</p>
                   </div>
                </div>
            </div>
            <div class="detail-close" @click="hideDetail">x</div>
        </div>
    </div>
</template>

<script>
 import star from '../star/star.vue';
export default {
    data() {
        return{
            detailShow: false,
        }
    },
    props: {
       seller: {
            type: Object
        }
    },
    methods: {
        showDetail() {
            this.detailShow = true
        },
        hideDetail() {
            this.detailShow = false
        }
    },
    created() {
        this.classMap = ['decrease','discount','special','invoice','guarantee'];
    },
    computed: {

    },
     components: {
        star
    }
};
</script>

<style lang="stylus" scoped>
    @import "../../common/stylus/mixin";
    @import "../../common/stylus/base";
    .header
        color: #ffffff
        position relative
        background: rgba(7,17,27,0.5)
        overflow hidden
        .content-wrapper
            position relative
            padding 48rpx 24rpx 48rpx 48rpx
            font-size 0
            .avatar
                display inline-block
                vertical-align top
                image 
                    border-radius 4rpx
                    width 128rpx
                    height 128rpx
            .content
                display inline-block
                margin-left 32rpx
                .title
                    margin 4rpx 0 16rpx 0
                    .brand
                        display inline-block
                        vertical-align top
                        width 60rpx
                        height 32rpx
                        bg-image('brand')
                        background-size 60rpx 36rpx
                        background-repeat no-repeat
                    .name
                        margin-left 12rpx
                        font-size 32rpx
                        line-height 36rpx
                        font-weight bold
                .description
                    margin-bottom 20rpx
                    line-height 24rpx
                    font-size 24rpx
                .support
                    .icon
                        display inline-block
                        vertical-align top
                        width 24rpx
                        height 24rpx
                        margin-right 8rpx
                        background-size 24rpx
                        background-repeat no-repeat
                        &.decrease
                            bg-image('decrease_1')
                        &.discount
                            bg-image('discount_1')
                        &.guarantee
                            bg-image('guarantee_1')
                        &.invoice
                            bg-image('invoice_1')
                        &.special
                            bg-image('special_1')
                    .text
                        line-height 24rpx
                        font-size 20rpx
            .support-count
                display flex
                text-align center
                justify-content space-around
                position absolute
                right 24rpx
                bottom 36rpx
                padding 0 16rpx
                height 48rpx
                line-height 48rpx
                border-radius 28rpx
                background rgba(0,0,0,0.2)
                .count
                    font-size 20rpx
                .icon
                    font-size 25rpx
                    padding-left 5rpx

                    
        .bulletin-wrapper
            height 56rpx
            line-height 56rpx
            padding 0 44rpx 0 24rpx
            overflow hidden
            white-space nowrap
            text-overflow ellipsis
            background rgba(7,17,27,.2)
            .bulletin-title
                display inline-block
                width 44rpx
                height 24rpx
                bg-image('bulletin')
                background-size 44rpx
                background-repeat no-repeat
                vertical-align top
                margin-top 16rpx
            .bulletin-text
                vertical-align top
                font-size 20rpx
                margin 0 8rpx
        .background
            position absolute
            top 0
            left 0
            width 100%
            height 100%
            z-index -1 
            filter blur(20rpx)
        .detail
            position fixed
            z-index 99999
            top 0
            left 0
            width 100%
            height 100%
            overflow auto
            background rgba(7,17,27,.8)
            .detail-wrapper
                min-height 100%
                width 100%
                .detail-main  
                    margin-top 120rpx
                    padding-bottom 128rpx
                    .name
                        line-height 32rpx
                        text-align center
                        font-size 32rpx
                        font-weight 700
                    .star-wrapper
                        margin-top 36rpx
                        padding 4rpx 0 
                        text-align center
                    .title
                        display flex
                        align-items center
                        width 80%
                        margin 56rpx auto 48rpx auto
                        .line
                            flex 1
                            top -12rpx
                            border-bottom 1rpx solid rgba(255,255,255,.2)
                        .text
                            padding 24rpx
                            font-weight 700
                            font-size 28rpx
                    .supports
                        width 80%
                        margin 0 auto 
                        .support-item
                            padding 0 24rpx
                            margin-bottom 24rpx
                            font-size 0
                            $:last-child
                                margin-bottom 0
                            .icon
                                display inline-block
                                width 32rpx
                                height 32rpx
                                margin-top -12rpx
                                vertical-align top
                                margin-right 24rpx
                                background-size 32rpx 32rpx
                                background-repeat no-repeat
                                &.decrease
                                    bg-image('decrease_2')
                                &.discount
                                    bg-image('discount_2')
                                &.guarantee
                                    bg-image('guarantee_2')
                                &.invoice
                                    bg-image('invoice_2')
                                &.special
                                    bg-image('special_2')
                            .text
                                line-height 2rpx
                                font-size 24rpx
                    .bulletin
                        width 80%
                        margin 0 auto 
                        .content
                            padding 0 24rpx
                            line-height 48rpx
                            font-size 24rpx

            .detail-close
                position relative
                width 64rpx
                height 64rpx
                margin -48rpx auto 0 auto
                clear both
                font-size 64rpx
</style>

   