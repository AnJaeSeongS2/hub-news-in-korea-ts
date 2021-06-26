<template>
  <div>
    <q-list bordered>
      <q-item
        class="text-h6 text-weight-medium"
        clickable
        v-ripple
        v-for="news in newsList"
        :key="news.guid"
      >
        <q-item-section>{{ news.title }}</q-item-section>
        <q-item-section class="text-caption" side>{{
          fromNow(news.pubDate)
        }}</q-item-section>
      </q-item>
    </q-list>
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
  data() {
    return {
      newsList: [],
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
});
</script>
<style></style>
