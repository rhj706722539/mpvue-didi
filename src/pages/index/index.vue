<template>
  <div class="home-page">
    <div class="nav-tab">
      <div class="nav-person">
        <!-- <svg class="icon" aria-hidden="true">
            <use xlink:href="#icon-xiao"></use>
        </svg> -->
      </div>
      <scroll-view class="nav-scroll"
      scroll-x  
      style="width: 100%"
      scroll-with-animation="true" 
      :scroll-left="scrollLeft">
        <div class="nav-item" v-for="(item,index) in navData" :key="index">
          {{item}}
        </div>
      </scroll-view>
    </div>
  </div>
</template>

<script type="text/ecmascript-6">
import card from '@/components/card'
import QQMapWX from '../../common/lib/qqmap-wx-jssdk.js'

const qqmapsdk = new QQMapWX({
    key: 'NQABZ-QVUK4-OS7U7-XG3MU-YTVS2-MQFPN'
});

export default {
  data () {
    return {
      motto: 'Hello weChat!',
      userInfo: {},
      scrollLeft:0,
      // toView: '出租车',
      navData:['出租车','快车','专车','豪华车','顺风车','代驾']
    }
  },
  components: {
    card
  },

  methods: {
    bindViewTap () {
      const url = '../logs/main'
      wx.navigateTo({ url })
    },
    getUserInfo () {
      // 调用登录接口
      wx.login({
        success: () => {
          wx.getUserInfo({
            success: (res) => {
              this.userInfo = res.userInfo
            }
          })
        }
      })
    },
    clickHandle (msg, ev) {
      console.log('clickHandle:', msg, ev)
    },
  },

  created () {
    // 调用应用实例的方法获取全局数据
    this.getUserInfo()
  }
}
</script>

<style scoped lang="scss">
.icon {
    width: 1em; height: 1em;
    vertical-align: -0.15em;
    fill: currentColor;
    overflow: hidden;
}
.nav-tab {
  width: 100%;
  background: #F8F8F8;
  .nav-person {
    width: 100%;
  }
  .nav-scroll {
    flex: 1;
    margin: 0 5px;
    height: 54px;
    line-height: 54px;
    overflow: hidden;
    white-space: nowrap;
    font-size: 0;
    .nav-item {
      width: 50px;
      text-align: center;
      margin: 0 10px;
      display: inline-block;
      font-size: 16px;
    }
  }
}
</style>
