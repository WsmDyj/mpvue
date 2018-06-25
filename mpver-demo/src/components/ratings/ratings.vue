<template>
    <div class="ratings">
        <div class="rating-content">
            <div class="overview">
                <div class="overview-left">
                    <h1 class="score">{{seller.score}}</h1>
                    <div class="title">综合评分</div>
                    <div class="rank">高于周边商家{{seller.rankRate}}%</div>
                </div>
                <div class="overview-right">
                    <div class="scroe-wrapper">
                        <span class="title">服务态度</span>
                        <div class="star"><star :size="36" :score="seller.serviceScore"></star></div>
                        <span class="scroe">{{seller.serviceScore}}</span>
                    </div>
                    <div class="scroe-wrapper">
                        <span class="title">商品评分</span>
                        <div class="star"> <star :size="36" :score="seller.serviceScore"></star></div>
                        <span class="scroe">{{seller.foodScore}}</span>
                    </div>
                     <div class="delivery-wrapper">
                        <span class="title">送达时间</span>
                        <span class="deliver">{{seller.deliveryTime}}分钟</span>
                    </div>
                </div>
            </div>
            <split></split>
            <ratingselect :select-type="selectType" :desc="desc"></ratingselect>
        </div>
        <div class="ratings-wrapper">
                <ul>
                    <li v-for="(rating,index) in ratings" :key="index" class="rating-wrapper">
                        <div class="avater">
                            <image :src="rating.avatar" style="width:56rpx;height:56rpx"/>
                        </div>
                        <div class="content">
                            <h1 class="name">{{rating.username}}</h1>
                            <div class="star-wrapper">
                                <div class="star"> <star :size="24" :score="rating.score"></star></div>
                               
                                <span class="delivery" v-show="rating.deliveryTime">{{rating.deliveryTime}}分钟送达</span>
                            </div>
                            <p class="text">{{rating.text}}</p>
                            <!-- <div class="recommend" v-show="rating.recommend"></div> -->
                            <div class="time">{{rating.rateTime}}</div>
                        </div>
                    </li>
                </ul>
            </div>
    </div>
</template>

<script>
 import star from '../star/star.vue';
 import ratingselect from '../ratingselect/ratingselect.vue';
 import split from "../split/split.vue"
export default {
     data() {
        return {
           ratings: {},
        }
    },
    created() {
        this.getList();
    },
    components: {
        star,
        split,
        ratingselect
    },
    props: {
      seller: {
            type: Object
        }
    }
}
</script>

<style lang="stylus" scoped>
 @import "../../common/stylus/mixin";
    .ratings
        position absolute
        top 348rpx
        bottom 0
        left 0
        width 100%
        .rating-content
            .overview
                display flex
                padding 36rpx 0
                .overview-left
                    flex 0 0 274rpx
                    padding 12rpx 0
                    width 274rpx
                    border-right  1px solid rgba(7,17,27,.2)
                    text-align center
                    .score
                        margin-bottom 12rpx
                        line-height 56rpx
                        font-size 48rpx
                        color rgb(255,153,0)
                    .title
                        margin-bottom 16rpx
                        line-height 24rpx
                        font-size 24rpx
                        color rgb(7,17,27)
                    .rank
                        line-height 20rpx
                        font-size 20rpx
                        color rgb(147,153,159)
                .overview-right
                    flex 1
                    padding 12rpx 0 12rpx 48rpx
                    .scroe-wrapper
                        margin-bottom 16rpx
                        font-size 0
                        .title
                            display inline-block
                            line-height 36rpx
                            font-size 24rpx
                            color rgb(7,17,27)
                        .star
                            display inline-block
                            margin 0 24rpx
                            vertical-align top
                        .scroe
                            display inline-block
                            vertical-align top
                            line-height 36rpx
                            font-size 24rpx
                            color rgb(250,153,0)
                    .delivery-wrapper
                        font-size 0
                        .title
                            line-height 36rpx
                            font-size 24rpx
                            color rgb(7,17,27)
                        .deliver
                            margin-left  24rpx
                            font-size 24rpx
                            color rgb(147,153,159)
        .ratings-wrapper
            padding 0 36rpx
            margin-top 36rpx
            margin-bottom 36rpx
            .rating-wrapper
                display flex
                border-1px(rgba(7,17,27,.1))
                margin-top 36rpx
                .avater
                    flex  0  0 56rpx 
                    width 56rpx
                    margin-right 24rpx
                    image 
                        border-radius 50%
                .content
                    display flex
                    flex-direction column
                    .name
                        line-height 24rpx
                        font-size 20rpx
                        color rgb(7,17,27)
                    .star-wrapper
                        .star
                            display inline-block
                        .delivery
                            padding-left 12rpx
                            font-size 20rpx
                            font-weight 200
                            color rgb(147,153,159)
                            line-height 24rpx
                    .text
                        font-size 24rpx
                        line-height 36rpx
                        color rgb(7,17,27)
                        padding-bottom 36rpx
                    .time
                        position absolute
                        right 36rpx
                        font-size 20rpx
                        font-weight 200
                        color rgb(147,153,159)
                        line-height 24rpx


                



       
                




                
                  
</style>
