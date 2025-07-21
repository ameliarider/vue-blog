<script>
export default {
  props: {
    post: Object,
  },
  data: function () {
    return {
      editPostParams: {},
    };
  },
  created: function () {
    this.editPostParams = { ...this.post };
  },
  methods: {
    handleSubmit: function () {
      this.$emit("updatePost", this.post.id, this.editPostParams)
    },
  },
};
</script>

<template>
  <div>
    <h1>Post information</h1>
    <p>Title: {{ post.title }}</p>
    <p>Content: {{ post.content }}</p>
    <form v-on:submit.prevent="handleSubmit">
        <div>
            Title:
            <input type="text" v-model="editPostParams.title" />
        </div>
        <div>
            Content:
            <input type="text" v-model="editPostParams.content">
        </div>
        <button type="submit">Update post</button>
    </form>
    <button v-on:click="$emit('destroyPost', post)">Destroy post</button>
  </div>
</template>

<style></style>