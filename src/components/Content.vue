<script>
import PostsIndex from "./PostsIndex.vue";
import axios from "axios";
import PostsNew from "./PostsNew.vue"
import Modal from "./Modal.vue"
import PostsShow from "./PostsShow.vue"

export default {
    components: {
        PostsIndex,
        PostsNew,
        Modal,
        PostsShow,
    },
    data: function () {
        return {
            posts: [],
            currentPost: {},
            isPostsShowVisible: false,
        };
    },
    created: function () {
        this.handleIndexPosts();
    },
    methods: {
        handleIndexPosts: function () {
            axios.get("posts.json").then((response) => {
                console.log("posts index", response);
                this.posts = response.data
            });
        },
        handleCreatePost: function (params) {
            axios
                .post("posts.json", params)
                .then((response) => {
                    console.log("posts create", response);
                    this.posts.push(response.data);
                })
                .catch((error) => {
                    console.log("posts create erro", error.response)
                });
        },
        handleShowPost: function (post) {
            console.log("handleshowPost", post);
            this.currentPost = post;
            this.isPostsShowVisible = true;
        },
        handleUpdatePost: function (id, params) {
            console.log("handleUpdatePost", id, params);
            axios
                .patch(`/posts/${id}.json`, params)
                .then((response) => {
                    console.log("posts update", response);
                    this.posts = this.posts.map((post) => {
                        if (post.id === response.data.id) {
                            return response.data;
                        } else {
                            return post;
                        }
                    });
                    this.handleClose();
                })
                .catch((error) => {
                    console.log("posts update error", error.response);
                });
        },
        handleClose: function () {
            this.isPostsShowVisible = false;
        },
    },
};
</script>

<template>
    <main>
        <PostsNew v-on:createPost="handleCreatePost" />
        <PostsIndex v-bind:posts="posts" v-on:showPost="handleShowPost" />
        <Modal v-bind:show="isPostsShowVisible" v-on:close="handleClose">
            <PostsShow v-bind:post="currentPost" v-on:updatePost="handleUpdatePost" />
        </Modal>
    </main>
</template>

<style></style>