<template>
  <v-app />
</template>

<script>
export default {
  name: 'RedirectPage',
  head: () => ({
    title: '正在跳转'
  }),
  mounted () {
    const targetUrl = window.location.href.split('?')[1].split('=')[1]
    const splitedUrlPatternLs = targetUrl.split('%2F')
    let targetUrlFixed = ''
    for (let i = 0; i < splitedUrlPatternLs.length; i++) {
      targetUrlFixed += splitedUrlPatternLs[i] + '/'
    }
    window.location.href = 'https://' + targetUrlFixed
  }
}
</script>
