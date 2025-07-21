<script>
export default {
    props: {
        posts: Array,
    },
};
</script>

<template>
  <div>
    <h1>All posts</h1>
    <div v-for="post in posts" v-bind:key="post.id">
       <h2>{{ post.title }}</h2>
       <p>Content: {{ post.content }}</p>
       <button v-on:click="$emit('showPost', post)">Details</button>
     </div>
  </div>
</template>

<style></style>