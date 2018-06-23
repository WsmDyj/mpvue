<template>
    <div class="cartcontrol">
         <div class="cart-decrease iconfont  icon-jianhao"  v-if="food.count>0" @click.stop="decreaseCart" transition="move"></div>
        <div class="cart-count" v-if="food.count>0">{{food.count}}</div>
        <div class="cart-add iconfont icon-jiahao-copy" @click.stop="addCart"></div>
    </div>
</template>

<script>
import Vue from 'vue' 
export default {
     data() {
        return{
            detailShow: false,
        }
    },
    props: {
        food: {
            type: Object,
        }
    },
    methods: {
        addCart(event) {
            if(!this.food.count){
                this.$set(this.food, 'count', 1)
                this.food.count = 1;
            }else{
                this.food.count++
            }
        },
        decreaseCart(){
            if(this.food.count){
                this.food.count--;
            }
        }
    },
    created() {
       
    }   
}
</script>

<style lang="stylus" scoped>
    .cartcontrol
        font-size 0
        .cart-decrease, .cart-add
            display inline-block
            font-size 48rpx
            line-height 48rpx
            padding 12rpx
            color rgb(0,160,220)
        .cart-decrease
            display inline-block
            color #c4c4c4
        .cart-count
            display inline-block
            vertical-align top
            width 24rpx
            padding-top 12rpx
            line-height 48rpx
            text-align center
            font-size 30rpx
            color rgb(147,153,159)
        .cart-add
            display inline-block
            color #ffd161
        
</style>
