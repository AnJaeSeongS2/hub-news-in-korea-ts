<template>
  <div>
    <q-table
      title="News(Tistorys) Table"
      :rows="newsList"
      :columns="columns"
      :class="classObject"
      row-key="guid"
    />
  </div>
</template>
<script lang="ts">
import Parser = require('rss-parser');
import moment = require('moment');
import { defineComponent } from 'vue';
// no use strict mode.
// const parser = new Parser({ xml2js: { strict: false } });
const parser = new Parser();
const CORS_PROXY = 'https://cors-anywhere.herokuapp.com/';
moment.locale('ko-kr');

export default defineComponent({
  name: 'news-table',
  props: {},
  data() {
    return {
      newsList: [],
      columns: [
        {
          name: 'title',
          required: true,
          label: 'Title',
          align: 'left',
          field: (row: any) => row.title,
          format: (val: string) => `${val}`,
          sortable: true,
        },
        {
          name: 'pubDate',
          required: true,
          label: 'Published Date',
          align: 'right',
          field: (row: any) => row.pubDate,
          format: (val: moment.MomentInput) => `${this.fromNow(val)}`,
          sortable: true,
        },
      ],
    };
  },
  async created() {
    const response = await parser.parseURL(
      // rss 만 지원하는 곳을 통해 rss수집.
      // `${CORS_PROXY}https://news.google.com/rss?hl=ko&gl=KR&ceid=KR:ko`
      `${CORS_PROXY}https://muzbox.tistory.com/rss`
    );
    console.log('show response:');
    console.log(response);
    this.newsList = response.items as never;
  },
  methods: {
    fromNow(timestamp: moment.MomentInput) {
      return moment(timestamp).fromNow();
    },
  },

  updated() {
    console.log('asdasda');
  },
});
</script>
<style></style>
