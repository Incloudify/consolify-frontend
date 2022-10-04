<template>
  <v-app>
    <img src="~/static/incloudify-logo-large.png">
    <h1>忘记密码</h1>
    <p>「最后, 森林会记住一切」</p>
    <AccountForgotForm />
    <div class="options">
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
  name: 'AccountLoginPage',
  head: () => ({
    title: '账户登录'
  })
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
img{
  margin: 5px auto;
  max-width: 150px;
  max-height: 100px;
}
.options{
  display: flex;
  margin: 10px auto;
}
</style>
