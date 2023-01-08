<template>
  <v-app>
    <img src="~/static/incloudify-logo-large.png">
    <h1>注册玲行云端账户</h1>
    <p ref="welcomeTxt">
      你好, 世界。
    </p>
    <AccountRegisterForm @processBackward="processBackward" @processStarted="processStarted" @submitSucceed="submitSucceed" @submit.native.prevent />
    <div ref="optionsTxt" class="options">
      <v-btn elevation="0" color="transparent" rounded max-width="250px" to="/account/login">
        事实上我已经有账户了
      </v-btn>
      <p style="margin-top: 5px">
        &nbsp;|&nbsp;
      </p>
      <v-btn elevation="0" color="transparent" rounded max-width="100px" to="/account/forgot">
        忘记密码
      </v-btn>
    </div>
  </v-app>
</template>

<script>
export default {
  name: 'AccountRegisterPage',
  head: () => ({
    title: '账户注册'
  }),
  methods: {
    processStarted () {
      this.$refs.optionsTxt.style = 'opacity: 0;'
      setTimeout(() => {
        this.$refs.optionsTxt.style = 'opacity: 0; display: none;'
      }, 500)
    },
    processBackward () {
      setTimeout(() => {
        this.$refs.optionsTxt.style = 'opacity: 0;'
        setTimeout(() => {
          this.$refs.optionsTxt.style = 'opacity: 1;'
        }, 100)
      }, 500)
    },
    submitSucceed () {
      this.$refs.welcomeTxt.style = 'opacity: 0;'
      setTimeout(() => {
        this.$refs.welcomeTxt.style = 'opacity: 0; display: none;'
        this.$parent.$emit('showSnackBar', 'success', '注册成功', 3000, true)
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
</style>
