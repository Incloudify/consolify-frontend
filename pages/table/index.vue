<template>
  <v-row>
    <v-col
      sm="9"
    >
      <TableTabs />
    </v-col>
    <v-col
      sm="3"
    >
      <TableFund />
    </v-col>
  </v-row>
</template>

<script>
export default {
  name: 'IndexPage',
  head () {
    return {
      title: '首页'
    }
  }
}
</script>
