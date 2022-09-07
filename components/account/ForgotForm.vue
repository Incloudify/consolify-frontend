<template>
  <div>
    <v-form
      ref="infoForm"
      elevation="0"
      lazy-validation
    >
      <v-text-field
        label="还记得你的名字吗"
        placeholder="填写用户名或注册邮箱"
        hint="你的名字仅包含大小写A-z, 数字0-9, 下划线_, @, ."
        maxlength="35"
        :rules="userNameRule"
        outlined
      />
      <v-btn
        rounded
        block
        ref="submitBtn"
        elevation="1"
        color="primary"
        :loading="isSubmitting"
        :disabled="isSubmitting"
        @click="submit"
      >
        开始唤醒
      </v-btn>
    </v-form>
  </div>
</template>

<script>
export default {
  name: 'ForgotForm',
  data: () => ({
    isSubmitting: false,
    userNameRule: [
      value => !!value || '这下完了, 连自己名字也忘记了',
      (value) => {
        const emailPattern = /\w[-\w.+]*@([A-Za-z0-9][-A-Za-z0-9]+\.)+[A-Za-z]/
        const userNamePattern = /\w([A-Za-z0-9][-A-Za-z0-9]*)/
        if (emailPattern.test(value)) {
          return true
        } else if (userNamePattern.test(value)) {
          return true
        } else {
          return false || '名字不是你想叫什么就叫什么的啊!'
        }
      }
    ]
  }),
  methods: {
    submit () {
      const validateResult = this.$refs.infoForm.validate()
      this.$refs.submitBtn.$el.style = ''
      if (validateResult === true) {
        this.isSubmitting = !this.isSubmitting
      } else {
        this.$refs.submitBtn.$el.style = 'background-color: #EE6363 !important; border-color: #EE6363 !important;'
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
