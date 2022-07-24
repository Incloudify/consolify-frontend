<template>
  <div>
    <!-- 卡片是好文明 -->
    <v-card
      height="200px"
    >
      <v-tabs>
        <!-- 概览导航头部 开始 -->
        <v-tab
          href="#tabs-viewall"
        >
          <v-icon>mdi-home</v-icon>
          概览
        </v-tab>
        <v-tab
          href="#tabs-safecenter"
        >
          <v-icon>mdi-safe</v-icon>
          安全中心
        </v-tab>
        <v-tab
          href="#tabs-monitor"
        >
          <v-icon>mdi-monitor-dashboard</v-icon>
          运维
        </v-tab>
        <!-- 概览导航头部 结束 -->
        <!-- 概览导航内容 开始 -->
        <v-tab-item
          value="tabs-viewall"
        >
          概览
        </v-tab-item>
        <v-tab-item
          value="tabs-safecenter"
        >
          安全中心
        </v-tab-item>
        <v-tab-item
          value="tabs-monitor"
        >
          运维
        </v-tab-item>
        <!-- 概览导航内容 结束 -->
      </v-tabs>
    </v-card>
  </div>
</template>

<script>
export default {}
</script>
