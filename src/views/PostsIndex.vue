<script>
import axios from "axios";

export default {
  data: function () {
    return {
      posts: [],
    };
  },
  created: function () {
    axios.get("http://localhost:3000/posts.json").then((response) => {
      this.posts = response.data;
      console.log("Posts", this.posts);
    });
  },
};
</script>

<template>
  <div class="index">
    <h1>These are my blog posts!</h1>
    <div v-for="post in posts" v-bind:key="post.id">
      <h2>Title: {{ post.title }}</h2>
      <img :src="post.image" v-bind:alt="post.title" />
      <p>Post: {{ post.body }}</p>
      <a href="/posts">More Info!</a>
    </div>
  </div>
</template>
