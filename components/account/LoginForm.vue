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
  methods: {
    submit () {
      this.isSubmitting = !this.isSubmitting
      this.$refs.infoForm.validate()
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
