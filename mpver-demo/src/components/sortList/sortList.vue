<template>

  <div class="sort-list">
    <div class="sort" @click="onOverallTag">综合排序{{sortSelected}}
      <image src="/static/images/down.png" style="width:20rpx;height:20rpx;"/></div>
      <div data-index="0" @click="onTapTag" class="sort " :class="{'sort-active': selected == 0}">销量最高</div>
      <div data-index="1" @click="onTapTag" class="sort" :class="{'sort-active': selected == 1}">距离最近</div>
      <div class="sort" @click="onFilter">筛选
        <image src="/static/images/screen.png" style="width:22rpx;height:22rpx;"/>
      </div>
    </div>

  

</template>

<script>

export default {
}
</script>

<style lang="stylus" scoped>
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
        .sort-active
            color black
            font-weight: 800


  

        

</style>
