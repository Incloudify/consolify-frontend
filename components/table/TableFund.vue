<!-- 工作台概览 余额卡片 -->
<template>
  <div>
    <!-- 卡片是好文明 -->
    <v-card
      max-height="600px"
    >
      <v-card-title>
        爷的余额
      </v-card-title>
      <v-card-text>
        <p class="display-1 text--primary">
          {{ TableFundCurrent }}
          元
        </p>
      </v-card-text>
      <v-alert
        v-if="TableFundCurrent < 0"
        dense
        type="error"
        icon="mdi-alert-octagon-outline"
        class="v-alert-arrearage"
        style="background-color: rgba(255, 127, 127) !important;"
      >
        你的账户发生欠费, 请尽快补齐款项, 否则你的账户及名下资产将在 <strong>{{ deletionRemainDays }} 日后被删除</strong>
      </v-alert>
      <v-card-actions style="padding-bottom: 20px;">
        <v-btn to="/addfunds/vme50" color="primary">
          <v-icon>mdi-cash</v-icon>
          氪金
        </v-btn>
        <v-btn to="/billing/history">
          账单
        </v-btn>
      </v-card-actions>
    </v-card>
  </div>
</template>

<script>
export default {
  data: () => ({
    TableFundCurrent: -86837,
    deletionRemainDays: 3
  })
}
</script>
<style>
.v-alert-arrearage {
  font-size: 7px;
  margin: 0 4px;
}
</style>
