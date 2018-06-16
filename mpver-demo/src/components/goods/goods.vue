<template>
<div class="goods">
   <div class="menu-wrapp">
       <ul>
           <li v-for="(item ,index) in goods" :key="index" class="menu-item">
               <span class="text border-1px">
                   <span v-show="item.type>0" class="icon" :class="classMap[item.type]"></span>
                    {{item.name}}
                </span>
           </li>
       </ul>
   </div>
   <div class="foods-wrapper">
       <ul>
           <li v-for="(item,index) in goods" :key="index" class="food-list">
               <h1 class="title">{{item.name}}</h1>
               <ul>
                   <li v-for="(food, index) in item.foods" :key="index" class="food-item  border-1px">
                       <div class="icon">
                           <img :src="food.icon" width="57" height="57"/>
                       </div>
                       <div class="content">
                           <h2 class="name">{{food.name}}</h2>
                           <p class="desc">{{food.description}}</p>
                           <div class="extra">
                               <span class="count">月售{{food.sellerCount}}份</span>
                               <span>好评率{{food.rating}}%</span>
                           </div>
                           <div class="price">
                               <span class="now">￥{{food.price}}</span>
                               <span v-show="food.oldPrice" class="old">￥{{food.oldPrice}}</span>
                           </div>
                       </div>
                   </li>
               </ul>
           </li>
       </ul>
   </div>
</div>
</template>

<script>
export default {
    props: {
        seller: {
            type: Object
        }
    },
    data() {
        return {
            goods: []
        }
    },
    created() {
    this.classMap = ['decrease','discount','special','invoice','guarantee'];

        this.$http.get('https://www.easy-mock.com/mock/5aded45053796b38dd26e970/sell#!method=get')
        .then((response)=>{
        response = response.body;
        this.goods = response.data.goods;
        // console.log(this.goods)
    })
    }
}
</script>

<style lang="stylus" scoped>
  @import "../../common/stylus/mixin";
    .goods
        display flex
        position absoult 
        top 174px
        width 100%
        bottom 46px
        overflow hidden
        .menu-wrapp
            flex 0 0 80px
            width 80px
            background #f3f5f7
            .menu-item
                display table
                height 54px
                width 56px
                line-height 14px
                padding 0 12px
                .icon
                    display inline-block
                    width 16px
                    height 16px
                    vertical-align top
                    margin-right 2px
                    background-size 16px 16px
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
                    font-size 12px
                    width 56px
                    border-1px(rgba(7,17,27,.1))
                    vertical-align middle
        .foods-wrapper
            flex 1
            .title
                padding-left 14px
                height 26px
                line-height 26px
                border-left 2px solid #d9dde1
                font-size 12px
                color rgb(147,153,159)
                background #f3f5f7
            .food-item
                display flex
                margin 18px
                padding-bottom 18px
                border-1px(rgba(7,17,27,.1))
                &:last-child
                    border-none()
                    margin-bottom 0
                .icon 
                    flex 0 0 57px
                    margin-right 10px
                .content
                    flex 1
                    .name
                        margin 2px 0 8px 0
                        font-size 14px
                        line-height 14px
                        color rgb(7,17,27)
                    .desc, .extra
                        line-height 10px
                        font-size 10px
                        color rgb(147,153,159)
                    .desc
                        margin-bottom 8px
                    .extra
                        &.count
                            margin-right 12px
                    .price
                        font-weight 700
                        line-height 24px
                        .now
                            margin-right 8px
                            font-size 14px
                            color rgb(240,20,20)
                        .old
                            text-decoration line-through
                            font-size 10px
                            color rgb(147,153,159)
                        
</style>
