<template>
    <div>
      <vue-good-table
        :columns="columns"
        :rows="rows"/>
    </div>
  </template>
  
  <script>
import { VueGoodTable } from 'vue-good-table-next';
import 'vue-good-table-next/dist/vue-good-table-next.css'

  
  export default {
    name: 'UserTable',
    props: {
      columns: Array,
      rows: Array,
    },
    components: {
        VueGoodTable,
    }
  };
  </script>
