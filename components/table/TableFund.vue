<!-- 工作台概览 余额卡片 -->
<template>
  <div>
    <!-- 卡片是好文明 -->
    <v-card
      height="200px"
    >
      <v-card-title>
        爷的余额
      </v-card-title>
      <v-card-text>
        <p class="display-1 text--primary">
          {{ tableFundCurrent }}
          元
        </p>
      </v-card-text>
      <v-card-actions>
        <v-btn color="primary">
          <v-icon>mdi-cash</v-icon>
          氪金
        </v-btn>
        <v-btn>
          账单
        </v-btn>
      </v-card-actions>
    </v-card>
  </div>
</template>

<script>
export default {
  data: () => ({
    tableFundCurrent: 0
  })
}
</script>
