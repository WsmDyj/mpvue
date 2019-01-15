<template>
    <div class="star" :class="starType">
       <span v-for="(itemClass,index) in itemClasses" :class="itemClass" class="star-item" :key="index"></span>

    </div>
</template>

<script>
    const LENGTH = 5;
    const CLS_ON = 'on';
    const CLS_HALF = 'half';
    const CLS_OFF = 'off';

export default {
    props: {
        size: {
            type: Number
        },
        score: {
            type: Number
        }
    },
    computed: {
        starType() {
            return 'star-' + this.size;
        },
        itemClasses() {
            let result = [];
            let score = Math.floor(this.score*2)/2;
            let hasDecimal = score % 1 !=0;
            let integer = Math.floor(score);
            for(let i=0;i<integer;i++) {
                result.push(CLS_ON);
            }
            if (hasDecimal) {
                result.push(CLS_HALF)
            }
            while (result.length < LENGTH) {
                result.push(CLS_OFF);
            }
             return result ;
        }
    }
}
</script>

<style lang="stylus" >
    @import "../../common/stylus/mixin";
    .star
        .star-item
            font-size 0
            display inline-block
            background-repeat no-repeat
        &.star-48
            .star-item
                width 40rpx
                height 40rpx
                margin-right 44rpx
                background-size 40rpx 40rpx
                &:last-child
                    margin-right 0
                &.on
                    bg-image('star48_on')
                &.half
                    bg-image('star48_half')
                &.off
                    bg-image('star48_off')
        &.star-36
            .star-item
                width 30rpx
                height 30rpx
                margin-right 16rpx
                background-size 30rpx 30rpx
                &:last-child
                    margin-right 0
                &.on
                    bg-image('star36_on')
                &.half
                    bg-image('star36_half')
                &.off
                    bg-image('star36_off')
        &.star-24
             .star-item
                width 10px
                height 10px
                margin-right 3px
                background-size 10px 10px
                &:last-child
                    margin-right 0
                &.on
                    bg-image('star24_on')
                &.half
                    bg-image('star24_half')
                &.off
                    bg-image('star24_off')
        
</style>
