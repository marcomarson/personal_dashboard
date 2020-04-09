<template>
  <base-table :data="values"
              :columns="table.columns"
              thead-classes="text-primary">
  </base-table>
</template>
<script>
  import { BaseTable } from "@/components";
  export default {
     props: {
      values: {
        type: Array,
        default: () => [],
      },
     },
    components: {
      BaseTable
    },
    computed: {
      table(){
        return this.$t('dashboard.usersTable');
      }
    }
  }
</script>
<style>
</style>
