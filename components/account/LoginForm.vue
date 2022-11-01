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
import SessionUtils from '~/utils/SessionUtils.vue'
import HttpUtils from '~/utils/HttpUtils.vue'
export default {
  name: 'LoginForm',
  mixins: [SessionUtils, HttpUtils],
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
      const dataObj = {}
      dataObj.username = usernameData
      dataObj.password = saltPasswordMD5
      this.sendPostToApi('/account/login', dataObj, this.reqDataCallback, false)
    },
    reqDataCallback (requestDataReturn) {
      if (requestDataReturn.code === 1000) {
        const sessionIdReturn = requestDataReturn.data.sessionId
        if (sessionIdReturn !== null) {
          this.editCookieValue('sessionId', sessionIdReturn)
        }
        this.$data.isSubmitted = true
        setTimeout(() => {
          this.$data.transitionPlayed = true
        }, 500)
        this.$emit('submitSucceed')
      } else if (requestDataReturn.data !== undefined && requestDataReturn.data.code !== undefined) {
        if (requestDataReturn.data.code === 1001 && requestDataReturn.code === 404) {
          this.showResult(undefined, undefined, true, false, '用户名/邮箱不存在')
        } else if (requestDataReturn.data.code === 1002 && requestDataReturn.code === 403) {
          this.showResult(undefined, undefined, false, true, '密码不正确')
        }
      } else if (requestDataReturn.code === 500) {
        this.showResult('error', '服务器内部错误, 请重试', true, true, '服务器内部错误, 请重试')
      } else if (requestDataReturn.code === -1) {
        this.showResult('error', '网络错误, 请重试', true, true, '网络错误, 请重试')
      } else if (requestDataReturn.code === 0) {
        this.showResult('error', '发生未知错误, 请重试', true, true, '发生未知错误, 请重试')
      } else {
        this.showResult('error', '发生未知错误, 请重试', true, true, '发生未知错误, 请重试')
      }
    },
    clearBtnStyle () {
      this.$refs.submitBtn.$el.style = ''
    },
    showResult (snackBarType, snackBarMsg, usrErr, pwdErr, errMsg) {
      if (snackBarType !== undefined) {
        this.$parent.$parent.$parent.$emit('showSnackBar', snackBarType, snackBarMsg, '5000', true)
      }
      this.$data.usernameErr = usrErr
      this.$data.passwordErr = pwdErr
      if (usrErr && pwdErr) {
        this.$data.pwdErrMsg = errMsg
        this.$data.usrErrCount = 1
        this.$data.pwdErrCount = 1
      } else if (usrErr && !pwdErr) {
        this.$data.usrErrMsg = errMsg
        this.$data.usrErrCount = 1
        this.$data.pwdErrCount = 0
      } else if (!usrErr && pwdErr) {
        this.$data.pwdErrMsg = errMsg
        this.$data.usrErrCount = 0
        this.$data.pwdErrCount = 1
      }
      this.$data.isSubmitting = false
      this.$refs.submitBtn.$el.style = 'background-color: #EE6363 !important; border-color: #EE6363 !important;'
      setTimeout(this.clearBtnStyle, 1500)
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
