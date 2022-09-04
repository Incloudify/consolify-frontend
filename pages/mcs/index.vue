<template>
  <div />
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
  }),
  mounted () {
    window.location.replace('/mcs/overview')
  }
}
</script>
