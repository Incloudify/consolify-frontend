<template>
  <v-app>
    <v-icon class="err-icon" size="70">
      mdi-alert-octagon-outline
    </v-icon>
    <h1>
      {{ errorMessage }}
    </h1>
    <v-btn to="/" class="back-to-home" width="150" rounded text>
      <v-icon>mdi-home-variant-outline</v-icon>返回首页
    </v-btn>
  </v-app>
</template>

<script>
export default {
  name: 'Error',
  props: {
    error: {
      type: Object,
      default: null
    }
  },
  data () {
    return {
      errorMessage: '发生错误: 错误码为 ' + this.error.statusCode
    }
  },
  head () {
    return {
      title: '发生错误'
    }
  }
}
</script>

<style>
h1 {
  font-size: 20px;
  margin: 0 auto;
  color: rgba(0, 0, 0, .6);
  margin-top: 10px;
}
.err-icon {
  color: rgba(0, 0, 0, .4);
  margin-left: auto;
  margin-right: auto;
  margin-top: 20px;
}
.back-to-home{
  margin: 10px auto !important;
}
</style>
