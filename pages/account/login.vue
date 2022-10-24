<template>
  <v-app>
    <img src="~/static/incloudify-logo-large.png">
    <h1>登录到玲行云端控制台</h1>
    <p ref="welcomeTxt">
      欢迎回来!
    </p>
    <AccountLoginForm class="login-form" @submitSucceed="submitSucceed" />
    <div ref="optionsTxt" class="options">
      <v-btn elevation="0" color="transparent" rounded max-width="100px" to="/account/forgot">
        忘记密码
      </v-btn>
      <p style="margin-top: 5px">
        &nbsp;|&nbsp;
      </p>
      <v-btn elevation="0" color="transparent" rounded max-width="100px">
        注册账户
      </v-btn>
    </div>
  </v-app>
</template>

<script>
export default {
  name: 'AccountLoginPage',
  head: () => ({
    title: '账户登录'
  }),
  methods: {
    submitSucceed () {
      this.$refs.welcomeTxt.style = 'opacity: 0;'
      this.$refs.optionsTxt.style = 'opacity: 0;'
      setTimeout(() => {
        this.$refs.welcomeTxt.innerHTML = '&nbsp;'
        this.$parent.$emit('showSnackBar', 'success', '登录成功', 3000, true)
      }, 500)
    }
  }
}
</script>
<style>
h1 {
  font-weight: 200;
  font-size: 25px;
  margin-bottom: 15px;
  margin-left: auto;
  margin-right: auto;
}
p {
  font-weight: 200;
  margin-left: auto;
  margin-right: auto;
  transition: opacity 0.5s;
}
img{
  margin: 5px auto;
  max-width: 150px;
  max-height: 100px;
}
.options{
  display: flex;
  margin: 10px auto;
  transition: opacity 0.5s;
}
.login-form{
  transition: all 0.5s;
}
</style>
