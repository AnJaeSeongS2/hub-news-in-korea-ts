<template>
  <div>
    <q-table
      title="News(Tistorys) Table"
      :rows="newsList"
      :columns="columns"
      :filter="filter"
      :pagination="myInitialPagination"
      row-key="guid"
    >
      <template v-slot:top-right>
        <q-input
          borderless
          dense
          debounce="300"
          v-model="filter"
          placeholder="Search"
        >
          <template v-slot:append>
            <q-icon name="search" />
          </template>
        </q-input>
      </template>
    </q-table>
  </div>
</template>
<script lang="ts">
import Parser = require('rss-parser');
import moment = require('moment');
import { defineComponent, ref } from 'vue';
// no use strict mode.
// const parser = new Parser({ xml2js: { strict: false } });
const parser = new Parser();
const CORS_PROXY = 'https://cors-anywhere.herokuapp.com/';
moment.locale('ko-kr');

interface Row {
  title: string;
  pubDate: moment.MomentInput;
}

export default defineComponent({
  name: 'news-table',
  props: {},
  data() {
    return {
      myInitialPagination: {
        rowsPerPage: 10,
      },
      filter: ref(''),
      newsList: [],
      columns: [
        {
          name: 'title',
          required: true,
          label: 'Title',
          align: 'left',
          field: (row: Row) => row.title,
          format: (val: string) => `${val}`,
          sortable: true,
        },
        {
          name: 'pubDate',
          required: true,
          label: 'Published Date',
          align: 'right',
          field: (row: Row) => row.pubDate,
          format: (val: moment.MomentInput): string => {
            return this.fromNow(val) as string;
          },
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
    fromNow(timestamp: moment.MomentInput): string {
      return moment(timestamp).fromNow();
    },
  },

  updated() {
    console.log('asdasda');
  },
});
</script>
<style></style>
