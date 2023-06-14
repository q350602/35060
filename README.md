//app.js
const defaultTime = {
  defaultWorkTime: 25,
  defaultRestTime: 5
}

App({
  globalData: {
    userInfo: null,
    defaultWorkTime: 25,
    defaultRestTime: 5
  },
  onLaunch: function() {
    let workTime = wx.getStorageSync('workTime')
    let restTime = wx.getStorageSync('restTime')
    if(!workTime) {
    if (!workTime) {
      wx.setStorage({
        key: 'workTime',
        data: this.globalData.defaultWorkTime
        data: defaultTime.defaultWorkTime
      })
    }
    if(!restTime) {
    if (!restTime) {
      wx.setStorage({
        key: 'restTime',
        data: this.globalData.defaultRestTime
        data: defaultTime.defaultRestTime
      })
    }
  },
  getUserInfo: function(cb) {
    var that = this;
    if (this.globalData.userInfo) {
      typeof cb == "function" && cb(this.globalData.userInfo)
    } else {
      //调用登录接口
      wx.login({
        success: function() {
          wx.getUserInfo({
            success: function(res) {
              that.globalData.userInfo = res.userInfo;
              typeof cb == "function" && cb(that.globalData.userInfo)
            }
          })
        }
      });
    }
  },
  setTime: function() {

  }
})
