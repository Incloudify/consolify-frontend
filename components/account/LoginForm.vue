<template>
  <div>
    <v-card
      elevation="0"
      max-width="35%"
      min-width="300px"
    >
      <v-text-field
        label="Username"
        hint="大小写A-z, 数字0-9, 下划线_"
        outlined
      />
      <v-text-field
        label="Password"
        hint="注册时设置的密码"
        :type="passwdShow ? 'text' : 'password'"
        :append-icon="passwdShow ? 'mdi-eye' : 'mdi-eye-off'"
        outlined
        @click:append="passwdShow = !passwdShow"
      />
      <v-btn
        rounded
        block
        elevation="1"
        color="primary"
        :loading="isSubmitting"
        @click="isSubmitting = !isSubmitting"
      >
        登录
      </v-btn>
    </v-card>
  </div>
</template>

<script>
export default {
  name: 'LoginForm',
  data: () => ({
    isSubmitting: false,
    passwdShow: false
  })
}
</script>

<style>
.v-card{
  margin: 5px auto;
  border-radius: 0 !important;
}
.v-btn{
  margin: 0;
}
.v-input{
  margin-top: 5px;
}
</style>
