<template>
  <div>
    <q-list bordered>
      <q-item clickable v-ripple v-for="news in newsList" :key="news.guid">
        <q-item-section>{{ news.title }}</q-item-section>
        <q-item-section>{{ news.pubDate }}</q-item-section>
      </q-item>
    </q-list>
  </div>
</template>
<script lang="ts">
import Parser = require('rss-parser');
import { defineComponent } from 'vue';
// no use strict mode.
// const parser = new Parser({ xml2js: { strict: false } });
const parser = new Parser();
const CORS_PROXY = 'https://cors-anywhere.herokuapp.com/';

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
});
</script>
<style></style>
