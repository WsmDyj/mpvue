<template>
   <div class="home">
    <div class="mask" v-show="isHidden" @click="mask1Cancel">
        <sortList></sortList>
        <div class="overall-sort-list">
            <div v-for="(item,index) in sortList" :key="index">
                <div class="overall-sort" @click="sortSelected">{{item.sort}}</div>
            </div> 
        </div>
    </div>
     <sprinner v-if="isShow"></sprinner>
    <search></search>
    <h-swiper></h-swiper>
        <div class="title">
            <div class="line"></div>
            <div class="text">附近商家</div>
            <div class="line"></div>
        </div>
        <div class="select">
            <div class="sort-list">
                <div class="sort" @click="onOverallTag">综合排序{{sortSelected}}
                <image src="/static/images/down.png" style="width:20rpx;height:20rpx;"/></div>
                <div :data-index="0" @click="onTapTag" class="sort " :class="{'sort-active': selected == 0}">销量最高</div>
                <div :data-index="1" @click="onTapTag" class="sort" :class="{'sort-active': selected == 1}">距离最近</div>
                <div class="sort" @click="onFilter">筛选
                    <image src="/static/images/screen.png" style="width:22rpx;height:22rpx;"/>
                </div>
            </div>
        </div>
        <scroll-view>
            <div class="restaurantsList">
                    <div class="restaurants-list" v-for="(item,index) in restaurant" :key="index" @click="toIndex">
                        <div class="restaurants-info-image"><image :src="item.src" class="restaurants-image"/></div>
                        <div class="restaurants-info">
                        <div class="restaurants-info-name">{{item.name}}</div>
                        <div class="restaurants-info-rating">
                             <star :size="24" :score="item.score"></star>
                            <div 
                            class="restaurants-info-rating-sales">月售 {{item.sales}}</div>
                        </div>
                        <div class="restaurants-info-price">
                            起送 {{item.initial_price}}￥ | 配送 {{item.distribution_price}}
                        </div>
                    </div>
                    <div class="restaurants-distribution">
                        <span class="restaurants-distribution-time">{{item.time}} 分钟</span>
                        <span class="restaurants-distribution-distance"> {{item.distance}}</span> 
                      
                    </div>
                    </div>
            </div>
        </scroll-view>
   
   </div>
    
</template>

<script>
    import swiper from "@/components/swiper/swiper";
    import star from "@/components/star/star";
    import sortList from "@/components/sortList/sortList";
    import search from "@/components/search/search";
    import sprinner from "@/components/sprinner/sprinner";
    import fly from '@/utils/fly'
export default {
    data() {
        return {
            restaurant:[],
            page: 1,
            isShow: false,
            isHidden: false,
            sortList:[{
                    sort: "综合排序",
                    image:"",
                }, {
                    sort: "速度最快",
                    image: "",
                }, {
                    sort: "评分最高",
                    image: "",
                }, {
                    sort: "起送价最低",
                    image: "",
                }, {
                    sort: "配送费最低",
                    image: "",
                }], 
                selected: null  
        }
    },
     onLoad() {
        this.getList();
    },
    created(){
        },
    components: {
        "h-swiper": swiper,
        star:star,
        search,
        sprinner,
        sortList
     },
      methods: {
          toIndex() {
               wx.navigateTo({
                    url: '/pages/index/main',
                    success: function(res){
                        console.log("success")
                    },
                })
          },
          onOverallTag() {
              this.isHidden = !this.isHidden;
          },
          sortSelected() {
                this.isHidden = false;
                this.$http.get('sell#!method=get').then((res)=>{
                    this.restaurant =  res.data.data.select;
                })
          },
          onTapTag(e) {
             this.selected = e.currentTarget.dataset.index
          },
          onFilter() {
                wx.showToast({
            title: '代完善',
            icon: 'success',
            duration: 2000
            })
          }
            
          
        
         
      },
       onReachBottom() {
                let nextPage = this.page +1;
                this.page = nextPage
                            wx.showLoading({
                    title: '加载中',
                })
                this.$http.get('sell#!method=get').then((res)=>{
                this.restaurant =[...res.data.data.restaurant,...this.restaurant]
                wx.hideLoading();
                }).catch((e)=>{
                console.log(e)
                })
            },
        onPullDownRefreash(){
          this.isShow = !this.isShow
        }
        
        
        
   
}
</script>

<style lang="stylus" scoped>
.home
    width 100%
    height 100%
    .mask
        overflow hidden
        position fixed
        z-index 999
        width 100%
        height 100%
        background-color rgba(15, 15, 26, 0.7)
        .overall-sort-list,.filterList,.filterList-footer
            background: white
        .overall-sort-list
            flex-direction column
            border-top 1px solid rgba(0,0,0,0)
            display flex
            .overall-sort
                font-size 25rpx
                height 70rpx
                line-height 70rpx
                margin-left 30rpx
                
    .title
        display flex
        align-items center
        width 50%
        margin 20rpx auto 30rpx auto
        .line
            flex 1
            top -12rpx
            border-bottom 1rpx solid #404040
        .text
            padding 24rpx
            font-weight 500
            font-size 35rpx
            color #333
    .select
        margin-bottom 30rpx
        .sort-list
            justify-content space-around
            display flex
            background white
            width 100%
            height 80rpx
            font-size 27rpx
            color #6A6A6A
            align-content center
            border 1rpx solid #ECECEC
            .sort
                text-align center
                margin auto 0
                height 30rpx
                line-height 30rpx
                border-right 1rpx solid #ECECEC;
                flex 1
                .overall-sort
                    font-size 25rpx
                    height 70rpx
                    line-height 70rpx
                    margin-left 30rpx
                    
                .sort-active
                    color black
                    font-weight: 800
        
    .restaurants-list
        font-size 25rpx
        display flex
        width 100%
        padding 10rpx 0   
        border-bottom 1rpx solid #ECECEC
        color: #6D6D6D
        justify-content space-between
        .restaurants-info-image
            margin 20rpx
            image
                width 200rpx
                height 125rpx
        .restaurants-info
            margin: 15rpx;
            flex: 1;
        .restaurants-info-name
            color #333
            font-size 36rpx
            font-weight 700
            margin-bottom 10rpx
        .restaurants-info-rating
            display flex
            width 300rpx
            height 50rpx
            line-height 50rpx
            .restaurants-info-rating-stars
                color #FFD161
                width 130rpx
                height 50rpx
            .restaurants-info-rating-sales
                width 150rpx
                height 50rpx
                padding-left 20rpx
    .restaurants-distribution
        width 180rpx
        margin-right 20rpx 
        margin-top 72rpx
        height 27rpx
        line-height 27rpx
        .restaurants-distribution-time
            padding-right 5rpx
            border-right 1px solid #e4e4e4
            
        
            
</style>
