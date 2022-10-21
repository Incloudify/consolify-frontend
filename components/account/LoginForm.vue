<template>
  <div>
    <v-scroll-x-transition>
      <v-form
        v-if="!isSubmitted"
        ref="infoForm"
        elevation="0"
        lazy-validation
      >
        <v-text-field
          ref="usrField"
          v-model="usernameData"
          label="用户名或邮箱"
          hint="大小写A-z, 数字0-9, 下划线_, @, ."
          :rules="userNameRule"
          :error="usernameErr"
          :error-count="usrErrCount"
          :error-messages="usrErrMsg"
          maxlength="35"
          outlined
        />
        <v-text-field
          ref="pwdField"
          v-model="originPassword"
          label="密码"
          hint="注册时设置的密码"
          :type="passwdShow ? 'text' : 'password'"
          :append-icon="passwdShow ? 'mdi-eye' : 'mdi-eye-off'"
          :rules="passwordRule"
          :error="passwordErr"
          :error-count="pwdErrCount"
          :error-messages="pwdErrMsg"
          maxlength="128"
          outlined
          @click:append="passwdShow = !passwdShow"
        />
        <v-btn
          id="submitBtn"
          ref="submitBtn"
          rounded
          block
          elevation="1"
          color="primary"
          :loading="isSubmitting"
          :disabled="isSubmitting"
          @click="submit"
        >
          登录
        </v-btn>
      </v-form>
    </v-scroll-x-transition>
    <v-scroll-x-transition>
      <v-form
        v-if="isSubmitted && transitionPlayed"
        ref="succeedForm"
        class="succeed-form"
        elevation="0"
      >
        <v-icon
          size="120"
          color="grey darken-2"
        >
          mdi-check
        </v-icon>
        <p>登录成功</p>
        <v-btn
          ref="backHomeBtn"
          rounded
          block
          elevation="1"
          color="primary"
          to="/table"
        >
          返回首页
        </v-btn>
      </v-form>
    </v-scroll-x-transition>
  </div>
</template>

<script>
import sessionUtils from '~/utils/SessionUtils.vue'
import httpUtils from '~/utils/HttpUtils.vue'
export default {
  name: 'LoginForm',
  mixins: [sessionUtils, httpUtils],
  data: () => ({
    isSubmitting: false,
    isSubmitted: false,
    passwdShow: false,
    usernameData: '',
    originPassword: '',
    usernameErr: false,
    passwordErr: false,
    transitionPlayed: false,
    usrErrCount: 1,
    pwdErrCount: 1,
    usrErrMsg: '',
    pwdErrMsg: '',
    userNameRule: [
      value => !!value || '不可以空着',
      (value) => {
        const emailPattern = /\w[-\w.+]*@([A-Za-z0-9][-A-Za-z0-9]+\.)+[A-Za-z]/
        const userNamePattern = /\w([A-Za-z0-9][-A-Za-z0-9]*)/
        if (emailPattern.test(value)) {
          return true
        } else if (userNamePattern.test(value)) {
          return true
        } else {
          return false || '好好填啊喂!'
        }
      }
    ],
    passwordRule: [
      value => !!value || '这个更不可以空着了'
    ]
  }),
  mounted () {
    this.reverseValidateSession('/account/settings')
  },
  methods: {
    submit () {
      const cryptoInstance = require('crypto')
      const validateResult = this.$refs.infoForm.validate()
      this.$refs.submitBtn.$el.style = ''
      if (validateResult === true) {
        this.isSubmitting = !this.isSubmitting
      } else {
        this.$refs.submitBtn.$el.style = 'background-color: #EE6363 !important; border-color: #EE6363 !important;'
        setTimeout(this.clearBtnStyle, 1500)
        return false
      }
      const usernameData = this.$data.usernameData
      const originPassword = this.$data.originPassword
      const saltPassword = 'MiHoMo114514' + originPassword + 'Incloudify1919810HengHengAAA'
      const md5 = cryptoInstance.createHash('md5')
      const saltPasswordMD5 = md5.update(saltPassword).digest('hex')
      this.sendPostToApi('/account/login', '{"username": "' + usernameData + '", "password": "' + saltPasswordMD5 + '"}', this.reqDataCallback)
    },
    reqDataCallback (requestDataReturn) {
      const cookie = document.cookie.split(';')
      if (requestDataReturn.code === 1000) {
        const sessionIdReturn = requestDataReturn.data.sessionId
        if (sessionIdReturn !== null) {
          this.editCookieValue(cookie, 'sessionId', sessionIdReturn)
        }
        this.$data.isSubmitted = true
        setTimeout(() => {
          this.$data.transitionPlayed = true
        }, 500)
        this.$emit('submitSucceed')
      } else if (requestDataReturn.code === 1001) {
        this.$data.usernameErr = true
        this.$data.usrErrMsg = '用户名/邮箱不存在'
        this.$data.usrErrCount = 1
        this.$data.isSubmitting = false
        this.$refs.submitBtn.$el.style = 'background-color: #EE6363 !important; border-color: #EE6363 !important;'
        setTimeout(this.clearBtnStyle, 1500)
      } else if (requestDataReturn.code === 1002) {
        this.$data.passwordErr = true
        this.$data.pwdErrMsg = '密码不正确'
        this.$data.pwdErrCount = 1
        this.$data.isSubmitting = false
        this.$refs.submitBtn.$el.style = 'background-color: #EE6363 !important; border-color: #EE6363 !important;'
        setTimeout(this.clearBtnStyle, 1500)
      } else {
        this.$data.usernameErr = true
        this.$data.passwordErr = true
        this.$data.pwdErrMsg = '发生未知错误, 请重试'
        this.$data.pwdErrCount = 1
        this.$data.isSubmitting = false
        this.$refs.submitBtn.$el.style = 'background-color: #EE6363 !important; border-color: #EE6363 !important;'
        setTimeout(this.clearBtnStyle, 1500)
      }
    },
    clearBtnStyle () {
      this.$refs.submitBtn.$el.style = ''
    }
  }
}
</script>

<style>
.v-form{
  margin: 5px auto;
  max-width: 35%;
  min-width: 300px;
}
.v-btn{
  margin: 0;
  transition: all 0.5s;
}
.v-input{
  margin-top: 5px;
}
.succeed-form{
  text-align: center;
}
.succeed-form p{
  font-size: 22px;
  opacity: .5;
}
</style>
