<template>
  <div>
    <p class="display-1 text--primary">
      MineCraft 服务器
    </p>
    <!-- 总览卡片 开始 -->
    <v-card>
      <v-card-title>
        <span>
          总览
        </span>
      </v-card-title>
      <v-card-subtitle>
        <span>
          您的玲行云端 MineCraft 服务器实例总览
        </span>
      </v-card-subtitle>
      <v-card-text>
        <v-row>
          <!-- 卡片左列 -->
          <v-col
            cols="5"
          >
            <v-row>
              <v-btn text>
                <v-icon>
                  mdi-server
                </v-icon>
                已开通实例({{ OwnedProductsMessage }})/运行中实例({{ OwnedProductsRunningMessage }})
              </v-btn>
            </v-row>
            <v-row>
              <v-btn text>
                <v-icon>
                  mdi-harddisk
                </v-icon>
                数据盘列表({{ OwnedDisksMessage }} 单位CED)
              </v-btn>
            </v-row>
            <v-row>
              <v-btn text>
                <v-icon>
                  mdi-content-save
                </v-icon>
                我的快照({{ OwnedSnapshotMessage }} 个)
              </v-btn>
            </v-row>
            <v-row>
              <v-btn color="primary">
                <v-icon>
                  mdi-plus-circle
                </v-icon>
                新建实例
              </v-btn>
              <v-btn>
                管理实例
              </v-btn>
            </v-row>
          </v-col>
          <!-- 卡片右列 -->
          <v-col>
            <v-row>
              <v-col>
                <v-progress-circular value="20" size="150" width="10">
                  实例运行状态
                </v-progress-circular>
              </v-col>
              <v-col>
                <v-progress-circular value="20" size="150" width="10">
                  数据用量
                </v-progress-circular>
              </v-col>
            </v-row>
          </v-col>
        </v-row>
      </v-card-text>
    </v-card>
    <!-- 总览卡片 结束 -->
  </div>
</template>

<script>
export default {
  name: 'MCSMIndex',
  layout: 'mcs',
  data: () => ({
    OwnedProductsMessage: '14',
    OwnedProductsRunningMessage: '54',
    OwnedDisksMessage: '19',
    OwnedSnapshotMessage: '8'
  }),
  head: () => ({
    title: '概览 - MineCraft 服务器'
  })
}
</script>
