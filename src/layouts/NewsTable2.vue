<template>
  <div>
    <q-table
      title="News(Tistorys) Table"
      :rows="state.newsList"
      :columns="state.columns"
      :filter="state.filter"
      :pagination="state.myInitialPagination"
      row-key="guid"
    >
      <template v-slot:top-right>
        <q-input
          borderless
          dense
          debounce="300"
          v-model="state.filter"
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
import { ref, reactive, onMounted } from 'vue';
import type Row from '../models/Row';
// no use strict mode.
// const parser = new Parser({ xml2js: { strict: false } });
const parser = new Parser();
moment.locale('ko-kr');
const CORS_PROXY = 'https://cors-anywhere.herokuapp.com/';

export default {
  setup() {
    const state = reactive({
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
            return fromNow(val);
          },
          sortable: true,
        },
      ],
    });

    onMounted(async () => {
      const response = await parser.parseURL(
        // rss 만 지원하는 곳을 통해 rss수집.
        // `${CORS_PROXY}https://news.google.com/rss?hl=ko&gl=KR&ceid=KR:ko`
        `${CORS_PROXY}https://muzbox.tistory.com/rss`
      );
      console.log('show response:');
      console.log(response);
      state.newsList = response.items as never;
    });

    const fromNow = (timestamp: moment.MomentInput): string => {
      return moment(timestamp).fromNow();
    };
    return {
      state,
      fromNow,
    };
  },
};
</script>
<style></style>
