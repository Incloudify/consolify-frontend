<template>
  <v-app />
</template>

<script>
export default {
  name: 'IndexPage',
  head: () => ({
    title: '首页'
  }),
  mounted () {
    window.location.replace('/table')
  }
}
</script>
