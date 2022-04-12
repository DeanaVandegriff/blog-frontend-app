<script>
import axios from "axios";

export default {
  data: function () {
    return {
      post: {},
    };
  },
  created: function () {
    axios.get("http://localhost:3000/posts/" + this.$route.params.id + "json").then((response) => {
      console.log(response.data);
      this.post = response.data;
    });
  },
  methods: {
    destroyPost: function (post) {
      axios.delete("http://localhost:3000/post/" + post.id).then((response) => {
        console.log("post destroy", response);
        this.$router.push("/posts");
      });
    },
  },
};
</script>

<template>
  <h1>Posts show</h1>
  <h2>Title: {{ post.title }}</h2>
  <img :src="post.image" v-bind:alt="post.title" />
  <p>Post: {{ post.body }}</p>
  <a v-bind:href="`/posts/${post.id}/edit`">Edit</a>
  <br />
  <button v-on:click="destroyPost(post)">Delete post</button>
  <br />
  <a href="/posts">Back to all posts!</a>
</template>
