<template lang="html5">
<div>
  <h1>hello</h1>
</div>
</template>
<script lang="ts">
export default {
  async created() {
    const response = await this.$axios.get(
      "https://jsonplaceholder.typicode.com/todos/1"
    );
    console.log(response);
  },
};
</script>
<style lang=""></style>
