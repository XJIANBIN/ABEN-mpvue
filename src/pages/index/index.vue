<template>
  <div class="container">
    <img class="bg-img" src="/static/img/bg.jpg" alt="">
    <div class="content">
      <div class="userinfo" @click="bindViewTap">
        <img class="userinfo-avatar" v-if="userInfo.avatarUrl" :src="userInfo.avatarUrl" background-size="cover" />
        <div class="userinfo-nickname">
          <card :text="userInfo.nickName"></card>
        </div>
      </div>
      <div class="usermotto">
        <div class="user-motto">
          <card :text="motto"></card>
        </div>
      </div>
      <div class="jump-in" @click="clickHandle('test click', $event)">
        <div class="scroll-block">
          <span class="icon-left">>></span>
        </div>
        <span>向右滑动进入</span>
      </div>
    </div>
  </div>
</template>

<script>
import card from '@/components/card'

export default {
  data () {
    return {
      motto: '阿本私厨',
      userInfo: {}
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
    }
  },

  created () {
    // 调用应用实例的方法获取全局数据
    this.getUserInfo()
  }
}
</script>

<style scoped>
@import "./index.css";
</style>
