<!-- 工作台概览 代办卡片 -->
<template>
  <div>
    <v-card
      height="200px"
    >
      <v-card-title>
        待办事项
      </v-card-title>
      <v-card-text>
        <v-row>
          <v-col>
            <v-btn text>
              待办工单({{ TicketsToSolve }})
            </v-btn>
          </v-col>
          <v-col>
            <v-btn text>
              待续费产品({{ ProductsToRenew }})
            </v-btn>
          </v-col>
        </v-row>
      </v-card-text>
    </v-card>
  </div>
</template>

<script>
export default {
  data: () => ({
    TicketsToSolve: 114,
    ProductsToRenew: 514
  })
}
</script>
