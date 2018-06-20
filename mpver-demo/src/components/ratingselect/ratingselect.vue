<template>
    <div class="ratingselect">
        <div class="rating-type border-1px">
            <span class="block positive" :class="{'active': selectType===2}">{{desc.all}}<span class="count">
                </span>47</span>
            <span class="block positive" :class="{'active': selectType===0}">{{desc.positive}}<span class="count">
                </span>50</span>
            <span class="block negative" :class="{'active': selectType===1}">{{desc.negative}}<span class="count">
                </span>7</span>
        </div>
        <div class="switch">
            <div class="icon"></div>
            <span class="text">只看有内容的评价</span>
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
                    positive: '满意',
                    negative: '不满意'
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
                border-radius 1rpx
                font-size 24rpx
                line-height 32rpx
                color rgb(77,85,93)
                &.active
                    color #fff
                .count
                    margin-left 4rpx
                    font-size 16rpx
                &.positive
                    background rgba(0,160,220,.2)
                    &.active
                        background rgb(0,160,220)
                &.negative
                    background rgba(77,85,93,.2)
                    &.active
                        background rgb(77,85,93)
        .switch
            padding 24rpx 36rpx
            line-height 48rpx
            border-bottom 1px solid rgba(7,17,27,.1)
            color rgb(147,153,159)
            font-size 0
            .icon
                height 24rpx
                width 24rpx
                border 1px solid rgba(7,17,27,.1)
                border-radius 50%
                line-height 24rpx
                display inline-block
                margin-right 8rpx
                font-size 48rpx
                background-color rgb(0,160,220)
            .text
                font-size 36rpx
</style>
