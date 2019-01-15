<template>
    <swiper class="categoryList" :autoplay="true" :circular="true" :indicator-dots="true" indicator-color="rgba(228,228,228,1)" indicator-active-color="#FECA49">
        <swiper-item v-for="(items,i) in categoryList" :key="i">
            <div v-for="(item,index) in items" class="category-info" :key="index" @click="choose">
                <image :src="item.src"  classs="category-image"/>
                <div class="category-text">{{item.name}}</div>
            </div>
        </swiper-item>
  </swiper>
</template>

<script>
export default {
    data() {
        return {
              categoryList:{
                    pageone:[{
                        name: "美食",
                        src: "/static/images/1.png"
                    }, {
                        name: "甜点饮品",
                        src: "/static/images/2.png"
                    }, {
                        name: "美团超市",
                        src: "/static/images/3.png"
                    }, {
                        name: "正餐精选",
                        src: "/static/images/4.png"
                    }, {
                        name: "生鲜果蔬",
                        src: "/static/images/5.png"
                    }, {
                        name: "全部商家",
                        src: "/static/images/6.png"
                    }, {
                        name: "免配送费",
                        src: "/static/images/7.png"
                    }, {
                        name: "新商家",
                        src: "/static/images/8.png"
                    }],
                    pagetwo: [{
                        name: "美食",
                        src: "/static/images/1.png"
                    }, {
                        name: "甜点饮品",
                        src: "/static/images/2.png"
                    }, {
                        name: "美团超市",
                        src: "/static/images/3.png"
                    }, {
                        name: "正餐精选",
                        src: "/static/images/4.png"
                    }, {
                        name: "生鲜果蔬",
                        src: "/static/images/5.png"
                    }, {
                        name: "全部商家",
                        src: "/static/images/6.png"
                    }, {
                        name: "免配送费",
                        src: "/static/images/7.png"
                    }, {
                        name: "新商家",
                        src: "/static/images/8.png"
                    }]
              }
        }
    },
   methods: {
        choose() {
         wx.showToast({
            title: '代完善',
            icon: 'success',
            duration: 2000
            })
        }
   }
}
</script>

<style lang="stylus" scoped>
    .categoryList
        width 100%
        height 350rpx
        border-bottom:20rpx solid #f4f4f4; 
        .category-info
            display inline-block
            text-align center
            position relative
            margin-top 10rpx
            width 25%
            height 150rpx
            image 
                width 95rpx
                height 95rpx
            .category-text
                font-size 25rpx
                width 100%
                line-height 30rpx



</style>
