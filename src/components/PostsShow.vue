<script>
export default {
  props: {
    post: Object,
  },
};
</script>

<template>
  <div>
    <h1>Post information</h1>
    <p>Title: {{ post.title }}</p>
    <p>Content: {{ post.content }}</p>
  </div>
</template>

<style></style>