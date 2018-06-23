<template>
    <div class="seller">
        <div class="seller-content">
            <div class="overview">
                <h1 class="title">{{seller.name}}</h1>
                <div class="desc bordex-1px">
                    <div class="star"><star :size="36" :score="seller.score"></star></div>
                    <span class="text">({{seller.ratingCount}})</span>
                    <span class="text">月销{{seller.sellCount}}单</span>
                </div>
                <ul class="remaek">
                    <li class="block">
                        <h2>起送价</h2>
                        <div class="content">
                            <span class="stress">{{seller.minPrice}}</span>元
                        </div>
                    </li> 
                    <li class="block">
                        <h2>商家配送</h2>
                        <div class="content">
                            <span class="stress">{{seller.deliveryPrice}}</span>元
                        </div>
                    </li>
                    <li class="block">
                        <h2>评价配送时间</h2>
                        <div class="content">
                            <span class="stress">{{seller.deliveryTime}}</span>分钟
                        </div>
                    </li>
                </ul>
            </div>
           <split></split>
           <div class="bulletin ">
               <h1 class="title">公告与活动</h1>
               <div class="content-wrapper border-1px">
                   <p class="contern">{{seller.bulletin}}</p>
               </div>
                 <ul v-if="seller.supports" class="supports">
                       <li class="support-item border-1px" v-for="(item,index) in seller.supports" :key="index">
                           <span class="icon" :class="classMap[seller.supports[index].type]"></span>
                            <span class="text">{{seller.supports[index].description}}</span>
                       </li>
                   </ul>
           </div>
            <split></split>
            <div class="pics">
                <h1 class="title">商家实景</h1>
               <scroll-view scroll-x="true" style="height: 180rpx;">
                   <div class="item" v-for="(item,index) in seller.pics" :key="index">
                       <image :src="item" style="width:240rpx;height:180rpx;display:inline-block"/>
                   </div>
               </scroll-view>
            </div>
             <split></split>
             <div class="info">
                 <h1 class="title  border-1px">商家信息</h1>
                 <ul>
                     <li class="info-item" v-for="(info,index) in seller.infos" :key="index">
                         <span class="text">{{info}}</span>
                     </li>
                 </ul>
             </div>
        </div>
    </div>
</template>

<script>
 import star from '../star/star.vue';
 import split from "../split/split.vue"
export default {
    data() {
        return {
            favorite: false
        }
    },
    created() {
        this.classMap = ['decrease','discount','special','invoice','guarantee'];
    },
    props: {
        seller: {
                type: Object
            }
        },
        components: {
            star,
            split
        },
}

</script>

<style  lang="stylus" scoped>
 @import "../../common/stylus/mixin";
    .seller
        position absolute
        top 348rpx
        bottom 0
        left 0
        width 100%
        .seller-content
            .overview
                padding 36rpx 
                .title
                    margin-top 36rpx
                    line-height 28rpx
                    margin-bottom 16rpx
                    font-size 28rpx
                    color rgb(7,17,27)
                .desc
                    padding-bottom 36rpx
                    border-1px(rgba(7,17,27,.1))
                    font-size 0
                    .star
                        display inline-block
                        margin-right 16rpx
                        line-height 36rpx
                        vertical-align top
                    .text
                        display inline-block
                        vertical-align top
                        margin-right 32rpx
                        line-height 36rpx
                        font-size 20rpx
                        color  rgb(77,85,93)
                .remaek
                    display flex
                    padding-top 36rpx
                    width 100%
                    .block
                        flex 1
                        text-align center
                        border-right 1px solid rgba(7,17,27,.1)
                        &:last-child
                            border-right none 
                        h2
                            margin-bottom 8rpx
                            line-height 20rpx
                            font-size 20rpx
                        .content
                            line-height 48rpx
                            font-size 20rpx
                            color rgb(7,17,27)
                            .stress
                                font-size 48rpx
            .bulletin
                padding 36rpx 36rpx 0 36rpx
                .title
                    margin-bottom 16rpx
                    line-height 28rpx
                    color rgb(7,17,27)
                .content-wrapper
                    padding 0 24rpx 32rpx 24rpx
                    border-1px(rgba(7,17,27,.1))
                    .contern
                        line-height 48rpx
                        font-size 24rpx
                        color rgb(240,20,20)
                        font-weight 200
                .supports
                    .support-item
                        display block
                        padding 32rpx 24rpx 
                        border-1px(rgba(7,17,27,.1))
                        font-size 0
                        .icon
                            width 32rpx
                            height 32rpx
                        .text
                            padding 12rpx
                            font-size 24rpx
                            font-weight 200
                            line-height 32rpx
                            color rgb(7,17,27)
            .pics
                padding 36rpx 0rpx 36rpx 36rpx
                .title
                    margin-bottom 24rpx
                .item
                    margin-right 12rpx
                    display inline-block
                    white-space nowrap
                    &:last-child
                        margin-right none 
            .info
                padding  36rpx 36rpx 0 36rpx
                color rgb(7,17,27)
                .title
                    padding-bottom 24rpx
                    border-1px(rgba(7,17,27,0.1))
                .info-item
                    padding 32rpx 24rpx
                    font-size 20rpx
                    border-1px(rgba(7,17,27,0.1))
                    .text
                        padding 12rpx
                        font-size 24rpx
                        font-weight 200
                        line-height 32rpx
                        color rgb(7,17,27)
                        

                   




                    



                    


</style>
