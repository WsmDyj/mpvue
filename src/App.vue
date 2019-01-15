<script>
export default {
  created () {
    // 调用API从本地缓存中获取数据
    const logs = wx.getStorageSync('logs') || []
    logs.unshift(Date.now())
    wx.setStorageSync('logs', logs)
  }
}
</script>

<style>
  @import './common/fonts/iconfont.css';
  @import './common/fonts/iconfont2.css';
  @import './common/fonts/iconfont3.css';
 
  
</style>
