<template>
  <news-table2></news-table2>
</template>
<script lang="ts">
import { defineComponent } from 'vue';
import NewsTable2 from '../layouts/NewsTable2.vue';

export default defineComponent({
  name: 'router-view',
  components: {
    NewsTable2,
  },
});
</script>
<style></style>
