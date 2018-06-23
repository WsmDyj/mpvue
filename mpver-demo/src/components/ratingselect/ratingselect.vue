<template>
    <div class="ratingselect">
        <div class="rating-type border-1px">
            <span class="block positive" :class="{'active': selectType===2}">{{desc.all}}<span class="count">
                </span>(47)</span>
            <span class="block positive" :class="{'active': selectType===0}">{{desc.positive}}<span class="count">
                </span>(40)</span>
            <span class="block negative" :class="{'active': selectType===1}">{{desc.negative}}<span class="count">
                </span>(7)</span>
        </div>
        <div class="switch">
            <div class="iconfont icon-rentongguli icon"></div>
            <span class="text">只看好评</span>
        </div>
    </div>
</template>

<script>
const POSITIVE = 0;
const HEGATIVE = 1;
const ALL = 2;
export default {
   
    props: {
        ratings: {
            type: Array,
            default() {
                return [];
            }
        },
        selectType: {
            type: Number,
            default: ALL
        },
        onlyContent: {
            default: false
        },
        desc: {
            type: Object,
            default() {
                return {
                    all: '全部',
                    positive: '好评',
                    negative: '差评'
                }
            }
        }
    },
   
}
</script>

<style lang="stylus" scoped>
  @import "../../common/stylus/mixin";
    .ratingselect
        .rating-type
            padding 36rpx 0
            margin 0 36rpx
            border-1px(rgba(7,17,27,.1))
            font-size 0
            .block
                display inline-block
                padding 16rpx 24rpx
                margin-right 16rpx
                border 1rpx solid #cccccc
                border-radius 5rpx
                font-size 24rpx
                line-height 32rpx
                color rgb(77,85,93)
                &.active
                    color #ffd161
                .count
                    margin-left 4rpx
                    font-size 16rpx
                &.positive
                    background #ffffff
                    &.active
                        background #fff8e9
                &.negative
                    background #fff
                    &.active
                        background rgb(77,85,93)
        .switch
            display flex
            padding 24rpx 36rpx
            line-height 48rpx
            border-bottom 1px solid rgba(7,17,27,.1)
            color rgb(147,153,159)
            font-size 0
            .icon
                color #ffd161
            .text
                font-size 24rpx
                padding-left 10rpx
</style>
