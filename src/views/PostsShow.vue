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
};
</script>

<template>
  <h1>Posts show</h1>
  <h2>Title: {{ post.title }}</h2>
  <img :src="post.image" v-bind:alt="post.title" />
  <p>Post: {{ post.body }}</p>
  <a href="/posts">Back to all posts!</a>
</template>
