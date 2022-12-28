<template>
  <!-- u1s1, 这页面代码乱的要死 -->
  <!-- 但没精力重构了 -->
  <!-- 不纯, 写于2022/12/28 22:17 -->
  <div>
    <v-stepper v-model="e1" elevation="0">
      <v-stepper-header class="elevation-0 reg-stepper-header">
        <v-stepper-step :complete="e1 > 1" step="1">
          账户信息
        </v-stepper-step>
        <v-divider />
        <v-stepper-step :complete="e1 > 2" step="2">
          安全性
        </v-stepper-step>
        <v-divider />
        <v-stepper-step :complete="e1 > 3" step="3">
          个性化
        </v-stepper-step>
        <v-divider />
        <v-stepper-step :complete="e1 > 4" step="4">
          验证邮箱
        </v-stepper-step>
        <v-divider />
        <v-stepper-step step="5">
          完成注册
        </v-stepper-step>
      </v-stepper-header>
      <v-stepper-items>
        <v-stepper-content step="1">
          <v-form v-if="stepNum === 1" ref="infoForm" elevation="0" lazy-validation>
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
              <v-btn ref="nextStepBtn" rounded elevation="1" color="primary" @click="setPassword">
                下一步
              </v-btn>
            </v-col>
          </v-form>
        </v-stepper-content>

        <v-stepper-content step="2">
          <v-form v-if="stepNum === 2" ref="passwdForm" class="passwd-form" elevation="0">
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
              <v-btn ref="nextStepBtn" rounded elevation="1" color="primary" @click="passwordCheck">
                下一步
              </v-btn>
            </v-col>
          </v-form>
        </v-stepper-content>

        <v-stepper-content step="3">
          <v-form ref="personForm" class="person-form" elevation="0">
            <v-text-field
              ref="nickNameField"
              v-model="nickName"
              label="用户名"
              hint="1-16个字符, 大小写A-z, 下划线_, 数字0-9, 中文字符, 横杠-"
              class="reg-nick-name-field"
              :rules="nickNameRule"
              :error="nickNameErr"
              :error-count="nickNameErrCount"
              :error-messages="nickNameErrMsg"
              maxlength="16"
            />
            <v-select
              ref="sexSelector"
              v-model="sex"
              :items="sexSelect"
              label="性别"
              persistent-hint
              hint="我们会根据您提供的性别选项（如果提供）来为您提供个性化称呼。"
            />
            <v-select
              ref="respectSelector"
              v-model="respectChoice"
              :items="respectSelect"
              label="尊称模式"
              item-value="respectId"
              item-text="des"
              persistent-hint
              hint="我们可能根据您选择的尊称模式，在相关消息中对您使用尊敬称呼。"
            />
            <br>
            <v-col style="display: flex; padding: 0;">
              <v-btn
                id="backwardBtn"
                ref="backwardBtn"
                rounded
                elevation="1"
                color="primary"
                :disabled="isSubmitting"
                @click="e1 = 2"
              >
                上一步
              </v-btn>
              <v-spacer />
              <v-btn
                id="nextStepBtn"
                ref="nextStepBtn"
                rounded
                right
                elevation="1"
                color="primary"
                :disabled="isSubmitting"
                @click="e1 = 4"
              >
                下一步
              </v-btn>
            </v-col>
          </v-form>
        </v-stepper-content>

        <v-stepper-content step="4">
          <v-form ref="captchaForm" class="captcha-form" elevation="0">
            <p style="text-align: center;">
              我们已向您的邮箱发送验证码, 请检查收件箱。
            </p>
            <v-otp-input
              length="6"
              type="number"
              class="register-verify-code-otp-input"
              v-model="verifyCode"
              :rules="verifyCodeRule"
              :error="captchaError"
              :error-count="captchaErrCount"
              :error-message="captchaErrMessage"
            ></v-otp-input>
            <div style="width: 100%; text-align: center;">
              <v-btn class="register-verify-code-resend-btn" elevation="0" @click="resendVerifyCode" color="primary">没有收到? 尝试重新发送</v-btn>
            </div>
            <v-col style="display: flex; padding: 0;">
              <v-btn
                id="backwardBtn"
                ref="backwardBtn"
                rounded
                elevation="1"
                color="primary"
                :disabled="isSubmitting"
                @click="e1 = 3"
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
        </v-stepper-content>

        <v-stepper-content step="5">
          <v-form v-if="stepNum === 3" ref="succeedForm" class="succeed-form" elevation="0">
            <v-icon size="120" color="grey darken-2">
              mdi-check
            </v-icon>
            <p>注册成功</p>
            <v-btn rounded block elevation="1" color="primary" to="/account/login">
              返回登录
            </v-btn>
          </v-form>
        </v-stepper-content>
      </v-stepper-items>
    </v-stepper>
  </div>
</template>

<script>
import SessionUtils from '~/utils/SessionUtils.vue'
import HttpUtils from '~/utils/HttpUtils.vue'
export default {
  name: 'LoginForm',
  mixins: [SessionUtils, HttpUtils],
  data: () => ({
    e1: 1,
    sexSelect: ['保密', '男', '女', '武装直升机', '其他'],
    respectSelect: [
      { des: '请用标准尊称称呼我', hint: '1', respectId: 1 },
      { des: '请以朋友的态度称呼我', hint: '2', respectId: 2 },
      { des: '请以最好的伙伴的态度称呼我', hint: '3', respectId: 3 }
    ],
    respectGroupSelect: ['溜溜梅'],
    canRespectGroupSelected: false,
    stepNum: 1,
    passwdShow: false,
    mailData: '',
    nickName: '',
    originPassword: '',
    mailErr: false,
    passwordErr: false,
    mailErrCount: 1,
    pwdErrCount: 1,
    mailErrMsg: '',
    pwdErrMsg: '',
    nickNameErr: false,
    nickNameErrCount: 1,
    nickNameErrMsg: '',
    captchaErr: false,
    captchaErrCount: 1,
    captchaErrMessage: '',
    isSubmitting: false,
    sex: 1,
    respectChoice: 1,
    verifyCode: '',
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
    ],
    nickNameRule: [
      value => !!value || '会被认不出的',
      (value) => {
        const nickNamePattern = /[A-Za-z0-9_\-\u4E00-\u9FA5]+/
        if (nickNamePattern.test(value)) {
          return true
        } else {
          return false || '仔细看看Hint哦 (1-16个字符, 大小写A-z, 下划线_, 数字0-9, 中文字符, 横杠-)'
        }
      }
    ],
    verifyCodeRule: [
      value => !!value || '你的验证码去哪儿了'
    ]
  }),
  methods: {
    setPassword () {
      if (this.$refs.infoForm.validate()) {
        this.$data.stepNum = 1
        this.$emit('processStarted')
        setTimeout(() => {
          this.$data.stepNum = 2
          this.$data.e1 = 2
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
        this.$data.e1 = 1
      }, 500)
    },
    passwordCheck () {
      const validateResult = this.$refs.passwdForm.validate()
      this.$refs.submitBtn.$el.style = ''
      if (validateResult === true) {
        this.$data.e1 = 3
      } else {
        this.$refs.submitBtn.$el.style = 'background-color: #EE6363 !important; border-color: #EE6363 !important;'
        setTimeout(() => {
          this.$refs.submitBtn.$el.style = ''
        }, 1500)
        return false
      }
    },
    submit () {
      const cryptoInstance = require('crypto')
      this.isSubmitting = !this.isSubmitting
      const mailData = this.$data.mailData
      const nickName = this.$data.nickName
      const originPassword = this.$data.originPassword
      const saltPassword = originPassword + '81262035b6d4babbcfd8fe71892edced'
      const sha512 = cryptoInstance.createHash('sha512')
      const saltPasswordSHA512 = sha512.update(saltPassword).digest('hex')
      const sex = this.$data.sexSelect.indexOf(this.$data.sex)
      const respectId = this.$data.respectChoice
      const verifyCode = this.$data.verifyCode
      const dataObj = {}
      dataObj.email = mailData
      dataObj.password = saltPasswordSHA512
      dataObj.username = nickName
      dataObj.sex = sex
      dataObj.respectId = respectId
      dataObj.captcha = verifyCode
      this.sendPostToApi('/account/register', dataObj, this.reqDataCallback, false)
    },
    reqDataCallback (requestDataReturn) {
      if (requestDataReturn.code === 1000) {
        this.$data.stepNum = 0
        setTimeout(() => {
          this.$data.stepNum = 3
          this.$data.e1 = 5
        }, 500)
        this.$emit('submitSucceed')
      } if (requestDataReturn.data !== undefined && requestDataReturn.data.code !== undefined) {
        if ((requestDataReturn.data.code === 1002 && requestDataReturn.code === 500) || requestDataReturn.code === 500) {
          this.$parent.$parent.$parent.$emit('showSnackBar', 'error', '服务器内部错误, 请重试', '5000', true)
          this.$data.mailErr = true
          this.$data.passwordErr = true
          this.$data.pwdErrMsg = '服务器内部错误, 请重试'
          this.$data.pwdErrCount = 1
          this.$data.isSubmitting = false
          this.$refs.submitBtn.$el.style = 'background-color: #EE6363 !important; border-color: #EE6363 !important;'
          setTimeout(() => {
            this.$refs.submitBtn.$el.style = ''
          }, 1500)
        } else if (requestDataReturn.data.code === 3012 && requestDataReturn.code === 409) {
          this.$parent.$parent.$parent.$emit('showSnackBar', 'error', '邮箱已被注册', '5000', true)
          this.$data.mailErr = true
          this.$data.mailErrMsg = '用户名或邮箱已被注册'
          this.$data.mailErrCount = 1
          this.$data.isSubmitting = false
          this.$refs.submitBtn.$el.style = 'background-color: #EE6363 !important; border-color: #EE6363 !important;'
          setTimeout(() => {
            this.$refs.submitBtn.$el.style = ''
          }, 1500)
        } else if ((requestDataReturn.data.code === 1003 && requestDataReturn.code === 422) || requestDataReturn.code === 422) {
          this.$parent.$parent.$parent.$emit('showSnackBar', 'error', '参数错误, 请联系系统管理员', '5000', true)
          this.$data.isSubmitting = false
          this.$refs.submitBtn.$el.style = 'background-color: #EE6363 !important; border-color: #EE6363 !important;'
          setTimeout(() => {
            this.$refs.submitBtn.$el.style = ''
          }, 1500)
        } else if (requestDataReturn.code === 403 && requestDataReturn.data.code === 3017) {
          this.$parent.$parent.$parent.$emit('showSnackBar', 'error', '验证码错误', '5000', true)
          this.$data.isSubmitting = false
          this.$data.verifyCode = ''
          this.$data.captchaErr = true
          this.$refs.submitBtn.$el.style = 'background-color: #EE6363 !important; border-color: #EE6363 !important;'
          setTimeout(() => {
            this.$refs.submitBtn.$el.style = ''
          }, 1500)
        } else if (requestDataReturn.data.code !== undefined) {
          this.$parent.$parent.$parent.$emit('showSnackBar', 'error', '未识别的错误, 请联系系统管理员', '5000', true)
          this.$data.mailErr = true
          this.$data.passwordErr = true
          this.$data.pwdErrMsg = '未识别的错误'
          this.$data.pwdErrCount = 1
          this.$data.isSubmitting = false
          this.$refs.submitBtn.$el.style = 'background-color: #EE6363 !important; border-color: #EE6363 !important;'
          setTimeout(() => {
            this.$refs.submitBtn.$el.style = ''
          }, 1500)
        } else {
          this.$parent.$parent.$parent.$emit('showSnackBar', 'error', '发生未知错误, 请重试', '5000', true)
          this.$data.mailErr = true
          this.$data.passwordErr = true
          this.$data.pwdErrMsg = '发生未知错误, 请重试'
          this.$data.pwdErrCount = 1
          this.$data.isSubmitting = false
          this.$refs.submitBtn.$el.style = 'background-color: #EE6363 !important; border-color: #EE6363 !important;'
          setTimeout(() => {
            this.$refs.submitBtn.$el.style = ''
          }, 1500)
        }
      } else if (requestDataReturn.code === -1) {
        this.$parent.$parent.$parent.$emit('showSnackBar', 'error', '网络错误, 请重试', '5000', true)
        this.$data.mailErr = true
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
        this.$data.mailErr = true
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
.v-form {
  margin: 5px auto;
  max-width: 35%;
  min-width: 300px;
}

.v-btn {
  margin: 0;
  transition: all 0.5s;
}

.v-input {
  margin-top: 5px;
}

.succeed-form {
  text-align: center;
}

.succeed-form p {
  font-size: 22px;
  opacity: .5;
}

.reg-stepper-header {
  margin: 10px auto;
  max-width: 50%;
}

.reg-nick-name-field {
  margin-top: 15px;
}

.register-verify-code-otp-input .v-input .v-input__control .v-input__slot {
  min-height: 80px;
  font-size: 30px;
}

.register-verify-code-resend-btn {
  margin-top: 10px;
  margin-bottom: 40px;
}
</style>
