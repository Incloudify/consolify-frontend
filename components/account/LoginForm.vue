<template>
  <div>
    <v-form
      ref="infoForm"
      elevation="0"
      lazy-validation
    >
      <v-text-field
        ref="usrField"
        label="用户名或邮箱"
        hint="大小写A-z, 数字0-9, 下划线_, @, ."
        :rules="userNameRule"
        maxlength="35"
        outlined
      />
      <v-text-field
        label="密码"
        hint="注册时设置的密码"
        :type="passwdShow ? 'text' : 'password'"
        :append-icon="passwdShow ? 'mdi-eye' : 'mdi-eye-off'"
        :rules="passwordRule"
        maxlength="128"
        outlined
        @click:append="passwdShow = !passwdShow"
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
        登录
      </v-btn>
    </v-form>
  </div>
</template>

<script>
export default {
  name: 'LoginForm',
  data: () => ({
    isSubmitting: false,
    passwdShow: false,
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
    this.validateSession()
  },
  methods: {
    submit () {
      const validateResult = this.$refs.infoForm.validate()
      this.$refs.submitBtn.$el.style = ''
      if (validateResult === true) {
        this.isSubmitting = !this.isSubmitting
      } else {
        this.$refs.submitBtn.$el.style = 'background-color: #EE6363 !important; border-color: #EE6363 !important;'
      }
      const sessionId = '1AE2BD6716D871278F712A78E78C121120987D1283'
      document.cookie += 'sessionId=' + sessionId + ';'
    },
    getCookieValue (cookie, cookieName) {
      for (let i = 0; i < cookie.length; i++) {
        const splitedData = cookie[i].split('=')
        if (splitedData[0] === cookieName) {
          return splitedData[1]
        }
      }
    },
    validateSession () {
      const cookie = document.cookie.split(';')
      const sessionId = this.getCookieValue(cookie, 'sessionId')
      // Send Cookie Value to the backend for validating
      let validateResult = false
      if (sessionId === '1AE2BD6716D871278F712A78E78C121120987D1283') {
        validateResult = true
      } else {
        validateResult = false
      }
      if (validateResult) {
        window.location.replace('/account/settings')
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
