<!-- 工作台首页 概览页 -->
<template>
  <div>
    <TableTabs />
    <!-- 比较硬核的空行 -->
    <br>
    <TableViewall />
  </div>
</template>

<script>
import sessionUtils from '~/utils/SessionUtils.vue'
export default {
  name: 'IndexPage',
  mixins: [sessionUtils],
  head: () => ({
    title: '概览 - 工作台'
  }),
  mounted () {
    this.validateSession()
  }
}
</script>
