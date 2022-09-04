<template>
  <v-app>
    <img src="~/static/incloudify-logo-large.png">
    <h1>登录到玲行云端控制台</h1>
    <AccountLoginForm />
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
img{
  margin: 5px auto;
  max-width: 150px;
  max-height: 100px;
}
</style>
