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
export default {
  name: 'IndexPage',
  head: () => ({
    title: '概览 - 工作台'
  })
}
</script>
