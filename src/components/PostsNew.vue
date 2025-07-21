<script>
export default {
    data: function () {
        return {
            newPostParams: {},
        };
    },
    methods: {
        handleSubmit: function () {
            this.$emit("createPost", this.newPostParams);
            this.newPostParams = {};
        },
    },
};
</script>

<template>
    <div>
        <h1>New Post</h1>
        <form v-on:submit.prevent="handleSubmit">
            <div>
                Title:
                <input type="text" v-model="newPostParams.title" />
            </div>
            <div>
                Content:
                <input type="text" v-model="newPostParams.content">
            </div>
            <button type="submit">Publish</button>
        </form>
    </div>
</template>

<style></style>