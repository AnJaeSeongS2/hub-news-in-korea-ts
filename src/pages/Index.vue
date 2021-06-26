<template>
  <news-table></news-table>
</template>
<script lang="ts">
import { defineComponent } from 'vue';
import NewsTable from './../layouts/NewsTable.vue';

export default defineComponent({
  name: 'router-view',
  components: {
    NewsTable,
  },
});
</script>
<style></style>
