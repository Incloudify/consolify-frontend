<!-- 工作台概览 代办卡片 -->
<template>
  <div>
    <v-card
      max-height="600px"
    >
      <v-card-title>
        待办事项
      </v-card-title>
      <v-card-text>
        <v-row>
          <v-col v-if="!(TicketsToSolve == 0)">
            <v-btn text>
              <v-icon size="20">
                mdi-bell-alert-outline
              </v-icon>&nbsp;
              待办工单({{ TicketsToSolve }})
            </v-btn>
          </v-col>
          <v-col v-if="!(ProductsToRenew == 0)">
            <v-btn text>
              <v-icon size="20">
                mdi-database-alert-outline
              </v-icon>&nbsp;
              待续费产品({{ ProductsToRenew }})
            </v-btn>
          </v-col>
          <v-col v-if="!(WarningToReview == 0)">
            <v-btn text>
              <v-icon size="20">
                mdi-email-alert-outline
              </v-icon>&nbsp;
              待处理告警({{ WarningToReview }})
            </v-btn>
          </v-col>
        </v-row>
        <div v-if="(TicketsToSolve == 0) && (ProductsToRenew == 0) && (WarningToReview == 0)" class="complete-div">
          <v-row>
            <v-icon size="100">
              mdi-check
            </v-icon>
          </v-row>
          <v-row>
            <span>全部完成!</span>
          </v-row>
          <v-row>
            <p>前面的区域, 以后再来探索吧</p>
          </v-row>
        </div>
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
export default {
  data: () => ({
    TicketsToSolve: 0,
    ProductsToRenew: 0,
    WarningToReview: 0
  })
}
</script>
<style>
.complete-div span {
  margin: 0 auto;
  font-size: 18px;
  margin-bottom: 10px;
}

.complete-div p {
  margin: 0 auto;
  font-size: 7px;
  margin-bottom: 10px;
}

.complete-div .v-icon {
  margin: 0 auto;
}

</style>
