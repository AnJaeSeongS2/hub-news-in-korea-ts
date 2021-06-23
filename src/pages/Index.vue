<template>
  <div>
    <h1>hello</h1>
  </div>
</template>
<script lang="ts">
import Parser = require("rss-parser");
const parser = new Parser();
const CORS_PROXY = "https://cors-anywhere.herokuapp.com/";

export default {
  async created() {
    const response = await parser.parseURL(
      `${CORS_PROXY}https://bbs.ruliweb.com/best/humor/now?custom_list=best`
    );
    console.log(response);
  },
};
</script>
<style></style>
