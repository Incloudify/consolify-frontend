<!-- 实例列表 -->
<template>
  <div>
    <p class="display-1 text--primary">
      我的实例
    </p>
    <!-- 工具栏 -->
    <v-toolbar>
      <v-toolbar-title>
        轻松管理容器云
      </v-toolbar-title>
      <v-spacer />
      <v-btn>
        产品文档
      </v-btn>
      &nbsp;&nbsp;
      <v-btn color="primary" to="./create/instance">
        创建实例
      </v-btn>
    </v-toolbar>
    <br>
    <!-- 卡片组 开始 -->
    <div>
      <v-card width="40%">
        <v-card-title>
          <span>
            实例名称
          </span>
          <v-chip
            class="ma-2"
            color="secondary"
          >
            MCSM 面板服
          </v-chip>
        </v-card-title>
        <v-card-text>
          <span>
            1核心 1GB内存 5M宽带 20GB ECD
          </span>
        </v-card-text>
        <v-card-actions>
          <v-btn text color="primary">
            管理实例
          </v-btn>
        </v-card-actions>
      </v-card>
    </div>
    <!-- 卡片组 结束 -->
  </div>
</template>

<script>
export default {
  name: 'ContainerList',
  title: '实例列表',
  layout: 'container',
  data: () => ({
    OwnedProductsMessage: '14',
    OwnedProductsRunningMessage: '54',
    OwnedDisksMessage: '19',
    OwnedSnapshotMessage: '8'
  }),
  head: () => ({
    title: '实例列表 - MineCraft 服务器'
  })
}
</script>
