<template>
  <div id="app">
   <v-header :seller="seller"></v-header>
    <div class="tab">
      <div class="tab-item">
        <a href="/goods" class="router">商品</a>
      </div>
      <div class="tab-item">
        <a href="/ratings" class="router">商品</a>
       </div>
      <div class="tab-item">
         <a href="/seller" class="router">商家</a>
       </div>
    </div>
    <router-view></router-view>
  </div>
</template>

<script>
  import header from "@/components/header/header";

export default {
  data() {
    return {
      seller: {}
    }
  },
  created() {
     wx.request({
        url:'https://www.easy-mock.com/mock/5aded45053796b38dd26e970/sell#!method=get',
        success: (res) => {
          this.seller = res.data.data.seller
          console.log(res.data.data.seller)
        },
      })
         
    },
 
  components: {
    "v-header":header
  }
}
</script>

<style >

  .tab {
    display: flex;
    width: 100%;
    height: 40px;
    line-height: 40px;
    text-align: center;
    /* border-bottom: 1px solid rgba(7, 17, 27, 0.1); */
    position: relative;
  }
  .tab::after {
    display: block;
    position: absolute;
    left: 0;
    bottom: 0;
    width: 100%;
    border-top: 1px solid rgba(7, 17, 27, 0.1);
    content: '';
  }
  .tab-item {
    flex: 1
  }
  .tab-item .router {
    display: block;
    font-size: 14px;
    color: rgb(77, 85, 93);
  }
  .tab-item .router-link-active  {
    color: rgb(240, 20, 20)
  }
</style>
