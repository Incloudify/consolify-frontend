<template>
  <v-app>
    <img src="~/static/incloudify-logo-large.png">
    <h1>忘记密码</h1>
    <p>「最后, 森林会记住一切」</p>
    <AccountForgotForm @submitSucceed="submitSucceed" @submit.native.prevent />
    <div ref="optionsTxt" class="options">
      <v-btn elevation="0" color="transparent" rounded max-width="200px" to="/account/login">
        我又双叒叕想起来了
      </v-btn>
      <p style="margin-top: 5px">
        &nbsp;|&nbsp;
      </p>
      <v-btn elevation="0" color="transparent" rounded max-width="100px" to="/account/register">
        注册账户
      </v-btn>
    </div>
  </v-app>
</template>

<script>
export default {
  name: 'PasswordResetPage',
  head: () => ({
    title: '密码重置'
  }),
  methods: {
    submitSucceed () {
      this.$refs.optionsTxt.style = 'opacity: 0;'
      setTimeout(() => {
        this.$refs.optionsTxt.style = 'opacity: 0; display: none;'
        this.$parent.$emit('showSnackBar', 'success', '密码重置邮件已发送', 3000, true)
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
}

img {
  margin: 5px auto;
  max-width: 150px;
  max-height: 100px;
}

.options {
  display: flex;
  margin: 10px auto;
  transition: all 0.5s;
}
</style>
