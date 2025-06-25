<template>
  <view class="register">
    <view class="con">
      <!-- Logo区域 -->
      <view class="logo-section">
        <image src="@/static/logo.png" />
        <text class="welcome-title">创建新账户</text>
        <text class="welcome-subtitle">开启您的专属体验</text>
      </view>

      <!-- 登录表单 -->
      <view class="login-form">
        <view :class="['item', errorTips==1 ? 'error' : '']">
          <view class="account">
            <view class="input-icon">👤</view>
            <view class="input-content">
              <text class="input-item">账号</text>
              <input
                type="text"
                data-type="account"
                placeholder-class="inp-palcehoder"
                placeholder="请输入账号名称"
                @input="getInputVal"
              >
            </view>
          </view>
          <view
            v-if="errorTips==1"
            class="error-text"
          >
            <text class="warning-icon">!</text>
            请输入账号！
          </view>
        </view>

        <view :class="['item', errorTips==2 ? 'error' : '']">
          <view class="account">
            <view class="input-icon">🔒</view>
            <view class="input-content">
              <text class="input-item">密码</text>
              <input
                type="password"
                data-type="password"
                placeholder-class="inp-palcehoder"
                placeholder="请输入密码"
                @input="getInputVal"
              >
            </view>
          </view>
          <view
            v-if="errorTips==2"
            class="error-text"
          >
            <text class="warning-icon">!</text>
            请输入密码！
          </view>
        </view>

        <view class="operate">
          <view
            class="to-register"
            @tap="toLogin"
          >
            已有账号？
            <text class="login-text">立即登录 →</text>
          </view>
        </view>
      </view>

      <view class="button-group">
        <button
          class="authorized-btn"
          @tap="toRegister"
        >
          注册账户
        </button>
        <button
          class="to-idx-btn"
          @tap="toIndex"
        >
          回到首页
        </button>
      </view>
    </view>
  </view>
</template>

<script setup>
import { encrypt } from '@/utils/crypto.js'

/**
 * 生命周期函数--监听页面显示
 */
onShow(() => {
  // 头部导航标题
  uni.setNavigationBarTitle({
    title: '用户注册'
  })
})

const principal = ref('') // 账号
const credentials = ref('') // 密码

/**
 * 输入框的值
 */
const getInputVal = (e) => {
  const type = e.currentTarget.dataset.type
  if (type == 'account') {
    principal.value = e.detail.value
  } else if (type == 'password') {
    credentials.value = e.detail.value
  }
}

const errorTips = ref(0) // 输入错误提示:  1账号输入  2密码输入

/**
 * 注册
 */
const toRegister = () => {
  if (principal.value.length == 0) {
    errorTips.value = 1
  } else if (credentials.value.length == 0) {
    errorTips.value = 2
  } else {
    errorTips.value = 0

    uni.showLoading({
      title: '注册中...'
    })
    http.request({
      url: '/user/register',
      method: 'post',
      data: {
        userName: principal.value,
        passWord: encrypt(credentials.value)
      }
    })
      .then(() => {
        uni.hideLoading()
        uni.showToast({
          title: '注册成功，请登录',
          icon: 'success',
          duration: 1500
        })
        setTimeout(() => {
          uni.navigateTo({
            url: '/pages/accountLogin/accountLogin'
          })
        }, 1800)
      })
      .catch(() => {
        uni.hideLoading()
      })
  }
}

/**
 * 去登陆
 */
const toLogin = () => {
  uni.navigateTo({
    url: '/pages/accountLogin/accountLogin'
  })
}

/**
 * 回到首页
 */
const toIndex = () => {
  uni.switchTab({
    url: '/pages/index/index'
  })
}
</script>

<style lang="scss" scoped>
.register {
  min-height: 100vh;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  padding: 40rpx 0;
}

.con {
  background: #fff;
  margin: 40rpx 30rpx;
  border-radius: 24rpx;
  box-shadow: 0 20rpx 40rpx rgba(0, 0, 0, 0.1);
  overflow: hidden;
  padding: 60rpx 0;
}

// Logo区域
.logo-section {
  text-align: center;
  margin-bottom: 80rpx;

  image {
    display: block;
    width: 250rpx;
    height: 250rpx;
    margin: 0 auto 30rpx;
    border-radius: 50%;
    border: 6rpx solid #f0f2ff;
    box-shadow: 0 10rpx 30rpx rgba(102, 126, 234, 0.2);
  }

  .welcome-title {
    display: block;
    font-size: 40rpx;
    font-weight: 700;
    color: #333;
    margin-bottom: 12rpx;
  }

  .welcome-subtitle {
    display: block;
    font-size: 26rpx;
    color: #999;
    font-weight: 300;
  }
}

.login-form {
  width: 90%;
  margin: 0 auto;
  margin-bottom: 60rpx;
}

.item {
  display: block;
  margin-bottom: 40rpx;

  &.error {
    .account {
      border-color: #ff4757;
      background: rgba(255, 71, 87, 0.05);
    }
  }
}

.account {
  display: flex;
  background: #f8f9ff;
  border: 2rpx solid #e8ebf7;
  border-radius: 16rpx;
  padding: 25rpx 20rpx;
  align-items: center;
  transition: all 0.3s ease;

  &:focus-within {
    border-color: #667eea;
    background: #f0f2ff;
    box-shadow: 0 0 0 6rpx rgba(102, 126, 234, 0.1);
  }

  .input-icon {
    font-size: 32rpx;
    margin-right: 20rpx;
    opacity: 0.7;
  }

  .input-content {
    flex: 1;

    .input-item {
      display: block;
      font-size: 24rpx;
      color: #667eea;
      font-weight: 600;
      margin-bottom: 8rpx;
    }

    input {
      width: 100%;
      font-size: 30rpx;
      color: #333;
      border: none;
      outline: none;
      background: transparent;

      &::placeholder {
        font-size: 28rpx;
        color: #bbb;
      }
    }
  }
}

.operate {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-top: 40rpx;
}

.to-register {
  font-size: 28rpx;
  color: #666;

  .login-text {
    color: #667eea;
    font-weight: 600;
    margin-left: 8rpx;
  }
}

.button-group {
  width: 90%;
  margin: 0 auto;
}

.authorized-btn {
  width: 100%;
  height: 88rpx;
  margin: 0 auto;
  text-align: center;
  background: linear-gradient(135deg, #667eea 0%, #764ba2 100%);
  border: none;
  color: #fff;
  border-radius: 44rpx;
  font-size: 32rpx;
  font-weight: 600;
  margin-bottom: 24rpx;
  box-shadow: 0 16rpx 32rpx rgba(102, 126, 234, 0.3);
  transition: all 0.3s ease;

  &:active {
    transform: translateY(2rpx);
    box-shadow: 0 12rpx 24rpx rgba(102, 126, 234, 0.2);
  }
}

.to-idx-btn {
  width: 100%;
  height: 88rpx;
  margin: 0 auto;
  text-align: center;
  background: #f5f6fa;
  border: 2rpx solid #e8ebf7;
  color: #666;
  border-radius: 44rpx;
  font-size: 30rpx;
  font-weight: 500;
  transition: all 0.3s ease;

  &:active {
    background: #eef0f6;
    transform: translateY(2rpx);
  }
}

button {
  &::after {
    border: 0 !important;
  }
}

.error {
  .error-text {
    display: flex;
    align-items: center;
    width: 100%;
    font-size: 26rpx;
    color: #ff4757;
    text-align: left;
    margin-top: 16rpx;
    padding-left: 20rpx;
    animation: shake 0.5s ease-in-out;

    .warning-icon {
      display: inline-flex;
      align-items: center;
      justify-content: center;
      color: #fff;
      width: 32rpx;
      height: 32rpx;
      background: #ff4757;
      border-radius: 50%;
      margin-right: 12rpx;
      font-size: 20rpx;
      font-weight: bold;
      flex-shrink: 0;
    }
  }
}

@keyframes shake {
  0%, 100% { transform: translateX(0); }
  25% { transform: translateX(-5rpx); }
  75% { transform: translateX(5rpx); }
}

// 输入框聚焦动画
.inp-palcehoder {
  color: #bbb !important;
  font-size: 28rpx !important;
}

// 响应式适配
@media screen and (max-width: 400px) {
  .con {
    margin: 20rpx 15rpx;
    padding: 40rpx 0;
  }

  .logo-section {
    margin-bottom: 60rpx;

    .welcome-title {
      font-size: 36rpx;
    }
  }

  .authorized-btn, .to-idx-btn {
    height: 80rpx;
    font-size: 28rpx;
  }
}
</style>
