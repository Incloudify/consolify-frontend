<template>
  <div>
    <v-scroll-x-transition>
      <v-form
        v-if="stepNum === 1"
        ref="infoForm"
        elevation="0"
        lazy-validation
      >
        <v-text-field
          ref="mailField"
          v-model="mailData"
          label="邮箱"
          hint="大小写A-z, 数字0-9, 下划线_, @, ."
          :rules="mailRule"
          :error="mailErr"
          :error-count="mailErrCount"
          :error-messages="mailErrMsg"
          maxlength="35"
          outlined
        />
        <v-col style="display: flex; padding: 0;">
          <v-spacer />
          <v-btn
            ref="nextStepBtn"
            rounded
            elevation="1"
            color="primary"
            @click="setPassword"
          >
            下一步
          </v-btn>
        </v-col>
      </v-form>
    </v-scroll-x-transition>
    <v-scroll-x-transition>
      <v-form
        v-if="stepNum === 2"
        ref="passwdForm"
        class="passwd-form"
        elevation="0"
      >
        <v-text-field
          ref="pwdField"
          v-model="originPassword"
          label="密码"
          hint="6-16个字符, 至少包含大写英文字母、小写英文字母、特殊符号、数字中的三种"
          :type="passwdShow ? 'text' : 'password'"
          :append-icon="passwdShow ? 'mdi-eye' : 'mdi-eye-off'"
          :rules="passwordRule"
          :error="passwordErr"
          :error-count="pwdErrCount"
          :error-messages="pwdErrMsg"
          maxlength="16"
          outlined
          @click:append="passwdShow = !passwdShow"
        />
        <v-col style="display: flex; padding: 0;">
          <v-btn
            id="backwardBtn"
            ref="backwardBtn"
            rounded
            elevation="1"
            color="primary"
            :disabled="isSubmitting"
            @click="backwardToEmail"
          >
            上一步
          </v-btn>
          <v-spacer />
          <v-btn
            id="submitBtn"
            ref="submitBtn"
            rounded
            right
            elevation="1"
            color="primary"
            :loading="isSubmitting"
            :disabled="isSubmitting"
            @click="submit"
          >
            注册
          </v-btn>
        </v-col>
      </v-form>
    </v-scroll-x-transition>
    <v-scroll-x-transition>
      <v-form
        v-if="stepNum === 3"
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
        <p>注册成功</p>
        <v-btn
          rounded
          block
          elevation="1"
          color="primary"
          to="/account/login"
        >
          返回登录
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
    stepNum: 1,
    passwdShow: false,
    mailData: '',
    originPassword: '',
    mailErr: false,
    passwordErr: false,
    mailErrCount: 1,
    pwdErrCount: 1,
    mailErrMsg: '',
    pwdErrMsg: '',
    isSubmitting: false,
    mailRule: [
      value => !!value || '不可以空着',
      (value) => {
        const emailPattern = /\w[-\w.+]*@([A-Za-z0-9][-A-Za-z0-9]+\.)+[A-Za-z]/
        if (emailPattern.test(value)) {
          return true
        } else {
          return false || '这真的是邮箱嘛...'
        }
      }
    ],
    passwordRule: [
      value => !!value || '你的账户安全至极'
    ]
  }),
  methods: {
    setPassword () {
      if (this.$refs.infoForm.validate()) {
        this.$data.stepNum = 0
        this.$emit('processStarted')
        setTimeout(() => {
          this.$data.stepNum = 2
        }, 500)
      } else {
        this.$refs.nextStepBtn.$el.style = 'background-color: #EE6363 !important; border-color: #EE6363 !important;'
        setTimeout(() => {
          this.$refs.nextStepBtn.$el.style = ''
        }, 1500)
        return false
      }
    },
    backwardToEmail () {
      this.$data.stepNum = 0
      this.$emit('processBackward')
      setTimeout(() => {
        this.$data.stepNum = 1
      }, 500)
    },
    submit () {
      const cryptoInstance = require('crypto')
      const validateResult = this.$refs.passwdForm.validate()
      this.$refs.submitBtn.$el.style = ''
      if (validateResult === true) {
        this.isSubmitting = !this.isSubmitting
      } else {
        this.$refs.submitBtn.$el.style = 'background-color: #EE6363 !important; border-color: #EE6363 !important;'
        setTimeout(() => {
          this.$refs.submitBtn.$el.style = ''
        }, 1500)
        return false
      }
      const mailData = this.$data.mailData
      const originPassword = this.$data.originPassword
      const saltPassword = 'MiHoMo114514' + originPassword + 'Incloudify1919810HengHengAAA'
      const md5 = cryptoInstance.createHash('md5')
      const saltPasswordMD5 = md5.update(saltPassword).digest('hex')
      const dataObj = {}
      dataObj.email = mailData
      dataObj.password = saltPasswordMD5
      this.sendPostToApi('/account/register', dataObj, this.reqDataCallback)
    },
    reqDataCallback (requestDataReturn) {
      if (requestDataReturn.code === 1010) {
        this.$data.stepNum = 0
        setTimeout(() => {
          this.$data.stepNum = 3
        }, 500)
        this.$emit('submitSucceed')
      } else if (requestDataReturn.code === 1011) {
        this.$parent.$parent.$parent.$emit('showSnackBar', 'error', '服务器内部错误, 请重试', '5000', true)
        this.$data.usernameErr = true
        this.$data.passwordErr = true
        this.$data.pwdErrMsg = '服务器内部错误, 请重试'
        this.$data.pwdErrCount = 1
        this.$data.isSubmitting = false
        this.$refs.submitBtn.$el.style = 'background-color: #EE6363 !important; border-color: #EE6363 !important;'
        setTimeout(() => {
          this.$refs.submitBtn.$el.style = ''
        }, 1500)
      } else if (requestDataReturn.code === 1012) {
        this.$parent.$parent.$parent.$emit('showSnackBar', 'error', '邮箱已被注册', '5000', true)
        this.$data.isSubmitting = false
        this.$refs.submitBtn.$el.style = 'background-color: #EE6363 !important; border-color: #EE6363 !important;'
        setTimeout(() => {
          this.$refs.submitBtn.$el.style = ''
        }, 1500)
      } else if (requestDataReturn.code === -1) {
        this.$parent.$parent.$parent.$emit('showSnackBar', 'error', '网络错误, 请重试', '5000', true)
        this.$data.usernameErr = true
        this.$data.passwordErr = true
        this.$data.pwdErrMsg = '网络错误, 请重试'
        this.$data.pwdErrCount = 1
        this.$data.isSubmitting = false
        this.$refs.submitBtn.$el.style = 'background-color: #EE6363 !important; border-color: #EE6363 !important;'
        setTimeout(() => {
          this.$refs.submitBtn.$el.style = ''
        }, 1500)
      } else {
        this.$parent.$parent.$parent.$emit('showSnackBar', 'error', '发生未知错误, 请重试', '5000', true)
        this.$data.usernameErr = true
        this.$data.passwordErr = true
        this.$data.pwdErrMsg = '发生未知错误, 请重试'
        this.$data.pwdErrCount = 1
        this.$data.isSubmitting = false
        this.$refs.submitBtn.$el.style = 'background-color: #EE6363 !important; border-color: #EE6363 !important;'
        setTimeout(() => {
          this.$refs.submitBtn.$el.style = ''
        }, 1500)
      }
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
