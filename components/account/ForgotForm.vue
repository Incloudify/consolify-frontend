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
          v-model="usernameData"
          label="还记得你的名字吗"
          placeholder="填写用户名或注册邮箱"
          hint="你的名字仅包含大小写A-z, 数字0-9, 下划线_, @, ."
          maxlength="35"
          :rules="userNameRule"
          outlined
        />
        <v-btn
          ref="submitBtn"
          rounded
          block
          elevation="1"
          color="primary"
          :loading="isSubmitting"
          :disabled="isSubmitting"
          @click="submit"
        >
          开始唤醒
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
          mdi-email-check-outline
        </v-icon>
        <p>邮件已发送</p>
        <v-btn
          ref="backLoginBtn"
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
import HttpUtils from '~/utils/HttpUtils.vue'
export default {
  name: 'ForgotForm',
  mixins: [HttpUtils],
  data: () => ({
    isSubmitting: false,
    userNameRule: [
      value => !!value || '这下完了, 连自己名字也忘记了',
      (value) => {
        const emailPattern = /\w[-\w.+]*@([A-Za-z0-9][-A-Za-z0-9]+\.)+[A-Za-z]/
        const userNamePattern = /\w([A-Za-z0-9][-A-Za-z0-9]*)/
        if (emailPattern.test(value)) {
          return true
        } else if (userNamePattern.test(value)) {
          return true
        } else {
          return false || '名字不是你想叫什么就叫什么的啊!'
        }
      }
    ],
    usernameData: '',
    isSubmitted: false,
    transitionPlayed: false
  }),
  methods: {
    submit () {
      const validateResult = this.$refs.infoForm.validate()
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
      const usernameData = this.$data.usernameData
      const dataObj = {}
      dataObj.username = usernameData
      this.sendPostToApi('/account/forgot', dataObj, this.reqDataCallback, false)
    },
    reqDataCallback (requestDataReturn) {
      if (requestDataReturn.code === 1000) {
        this.$data.isSubmitted = true
        setTimeout(() => {
          this.$data.transitionPlayed = true
        }, 500)
        this.$emit('submitSucceed')
      } else if (requestDataReturn.data !== undefined && requestDataReturn.data.code !== undefined) {
        if (requestDataReturn.data.code === 1021 && requestDataReturn.code === 404) {
          this.$data.usernameErr = true
          this.$data.usrErrMsg = '用户名/邮箱不存在'
          this.$data.usrErrCount = 1
          this.$data.isSubmitting = false
          this.$refs.submitBtn.$el.style = 'background-color: #EE6363 !important; border-color: #EE6363 !important;'
          setTimeout(() => {
            this.$refs.submitBtn.$el.style = ''
          }, 1500)
        } else if ((requestDataReturn.data.code === 1003 && requestDataReturn.code === 422) || requestDataReturn.code === 422) {
          this.$parent.$parent.$parent.$emit('showSnackBar', 'error', '参数错误, 请联系系统管理员', '5000', true)
          this.$data.usernameErr = true
          this.$data.usrErrMsg = '参数错误'
          this.$data.usrErrCount = 1
          this.$data.isSubmitting = false
          this.$refs.submitBtn.$el.style = 'background-color: #EE6363 !important; border-color: #EE6363 !important;'
          setTimeout(() => {
            this.$refs.submitBtn.$el.style = ''
          }, 1500)
        } else if (requestDataReturn.data.code !== undefined) {
          this.$parent.$parent.$parent.$emit('showSnackBar', 'error', '未识别的错误, 请联系系统管理员', '5000', true)
          this.$data.usernameErr = true
          this.$data.usrErrMsg = '未识别的错误'
          this.$data.usrErrCount = 1
          this.$data.isSubmitting = false
          this.$refs.submitBtn.$el.style = 'background-color: #EE6363 !important; border-color: #EE6363 !important;'
          setTimeout(() => {
            this.$refs.submitBtn.$el.style = ''
          }, 1500)
        } else {
          this.$parent.$parent.$parent.$emit('showSnackBar', 'error', '发生未知错误, 请重试', '5000', true)
          this.$data.usernameErr = true
          this.$data.usrErrMsg = '发生未知错误, 请重试'
          this.$data.usrErrCount = 1
          this.$data.isSubmitting = false
          this.$refs.submitBtn.$el.style = 'background-color: #EE6363 !important; border-color: #EE6363 !important;'
          setTimeout(() => {
            this.$refs.submitBtn.$el.style = ''
          }, 1500)
        }
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
}
.v-input{
  margin-top: 5px;
}
</style>
