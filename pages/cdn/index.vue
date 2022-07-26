<template>
  <div>
    <p class="display-1 text--primary">
      内容分发网络
    </p>
    <!-- 总览卡片 开始 -->
    <v-row>
      <v-col>
        <v-card>
          <v-card-title>
            <v-icon>
              mdi-access-point-network
            </v-icon>
            已添加域名数
          </v-card-title>
          <v-card-text>
            <div class="display-1">
              114
            </div>
          </v-card-text>
        </v-card>
      </v-col>
      <v-col>
        <v-card>
          <v-card-title>
            <v-icon>
              mdi-access-point-check
            </v-icon>
            已开始分发数
          </v-card-title>
          <v-card-text>
            <div class="display-1">
              114
            </div>
          </v-card-text>
        </v-card>
      </v-col>
      <v-col>
        <v-card>
          <v-card-title>
            <v-icon>
              mdi-alarm-light
            </v-icon>
            告警中域名数
          </v-card-title>
          <v-card-text>
            <div class="display-1" style="color: red;">
              114
            </div>
          </v-card-text>
        </v-card>
      </v-col>
    </v-row>
    <!-- 总览卡片 结束 -->
  </div>
</template>

<script>
export default {
  name: 'CdnIndex',
  layout: 'cdn',
  data: () => ({
  }),
  head: () => ({
    title: '概览 - 内容分发网络'
  })
}
</script>
