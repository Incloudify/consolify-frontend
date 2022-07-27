<template>
  <div>
    <p class="display-1 text--primary">
      域名列表
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
    <br>
    <v-card>
      <v-data-table
        :headers="dtHeaders"
        :items="dtDomains"
      >
        <template #[`item.actions`]="{ item }">
          <v-btn
            text
            :to="'/cdn/detail/' + item.name"
          >
            管理
          </v-btn>
        </template>
      </v-data-table>
    </v-card>
  </div>
</template>

<script>
export default {
  name: 'CdnDomains',
  layout: 'cdn',
  data: () => ({
    dtHeaders: [{
      text: '域名名称',
      align: 'start',
      sortable: false,
      value: 'name'
    },
    { text: '可用性', value: 'usable' },
    { text: '接入点', value: 'area' },
    { text: '流量', value: 'flow' },
    { text: '操作', value: 'actions' }
    ],
    dtDomains: [{
      name: 'www.incloudify.com',
      usable: '否',
      area: 'Liyue',
      flow: '114GB'
    }]
  }),
  head: () => ({
    title: '域名列表 -  内容分发网络'
  })
}
</script>
