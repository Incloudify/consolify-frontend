<template>
  <div>
    <v-card
      elevation="0"
      max-width="35%"
      min-width="300px"
    >
      <v-text-field
        label="还记得你的名字吗"
        placeholder="填写用户名或注册邮箱"
        hint="你的名字仅包含大小写A-z, 数字0-9, 下划线_, @, ."
        outlined
      />
      <v-btn
        rounded
        block
        elevation="1"
        color="primary"
        :loading="isSubmitting"
        :disabled="isSubmitting"
        @click="isSubmitting = !isSubmitting"
      >
        开始唤醒
      </v-btn>
    </v-card>
  </div>
</template>

<script>
export default {
  name: 'ForgotForm',
  data: () => ({
    isSubmitting: false
  })
}
</script>

<style>
.v-card{
  margin: 5px auto;
}
.v-btn{
  margin: 0;
}
.v-input{
  margin-top: 5px;
}
</style>
