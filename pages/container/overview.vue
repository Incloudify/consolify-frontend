<template>
  <div>
    <p class="display-1 text--primary">
      容器云
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
          您的玲行云端容器云实例总览
        </span>
      </v-card-subtitle>
      <v-card-text>
        <v-row>
          <!-- 卡片左列 -->
          <v-col
            cols="5"
          >
            <v-row>
              <v-btn text to="./productlist">
                <v-icon>
                  mdi-server
                </v-icon>
                已开通实例({{ OwnedProductsMessage }})/运行中实例({{ OwnedProductsRunningMessage }})
              </v-btn>
            </v-row>
            <v-row>
              <v-btn text to="./cedlist">
                <v-icon>
                  mdi-harddisk
                </v-icon>
                数据盘列表({{ OwnedDisksMessage }} 单位ATE)
              </v-btn>
            </v-row>
            <v-row>
              <v-btn text to="./snapshotlist">
                <v-icon>
                  mdi-content-save
                </v-icon>
                我的快照({{ OwnedSnapshotMessage }} 个)
              </v-btn>
            </v-row>
            <v-row>
              <v-btn class="new-instance-btn" color="primary" to="./create/instance">
                <v-icon>
                  mdi-plus-circle-outline
                </v-icon>
                &nbsp;新建实例
              </v-btn>
              &nbsp;&nbsp;&nbsp;
              <v-btn to="./productlist">
                管理实例
              </v-btn>
            </v-row>
          </v-col>
          <!-- 卡片右列 -->
          <v-col>
            <v-row>
              <v-col>
                <v-progress-circular rotate="-90" :value="(OwnedProductsRunningMessage / OwnedProductsMessage) * 100" size="150" width="10">
                  实例运行状态
                  <p><strong style="font-size: 24px;">{{ OwnedProductsRunningMessage }}</strong>/{{ OwnedProductsMessage }}</p>
                </v-progress-circular>
              </v-col>
              <v-col>
                <v-progress-circular rotate="-90" value="0" size="150" width="10">
                  数据用量
                  <p><strong style="font-size: 24px;">暂不支持</strong></p>
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
  name: 'ContainerOverview',
  layout: 'container',
  data: () => ({
    OwnedProductsMessage: 54,
    OwnedProductsRunningMessage: 14,
    OwnedDisksMessage: 19,
    OwnedSnapshotMessage: 8
  }),
  head: () => ({
    title: '概览 - 容器云'
  })
}
</script>
<style>
.new-instance-btn {
  margin-left: 10px;
}

.v-progress-circular__info {
  display: unset;
  text-align: center;
}
</style>
