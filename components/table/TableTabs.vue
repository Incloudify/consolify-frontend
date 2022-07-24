<!-- 工作台导航 -->
<template>
  <div>
    <v-toolbar elevation="0">
      <v-tabs>
        <!-- 概览导航头部 开始 -->
        <v-tab
          to="/table"
        >
          <v-icon>mdi-home</v-icon>
          概览
        </v-tab>
        <v-tab
          to="/table/safecenter"
        >
          <v-icon>mdi-safe</v-icon>
          安全中心
        </v-tab>
        <v-tab
          disabled
          to=""
        >
          <v-icon>mdi-monitor-dashboard</v-icon>
          运维事件
        </v-tab>
      </v-tabs>
    </v-toolbar>
    <!-- 概览导航头部 结束 -->
  </div>
</template>

<script>
export default {}
</script>
