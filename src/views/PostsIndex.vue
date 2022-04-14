<script>
import axios from "axios";

export default {
  data: function () {
    return {
      posts: [],
      currentPost: {},
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
    <div v-for="post in posts" v-on:click="currentPosts = posts" v-bind:key="post.id">
      <div v-bind:class="{ selected: post === currentPost }">
        <h2>{{ post.title }}</h2>
        <img :src="post.image" v-bind:alt="post.title" />
      </div>
      <a v-bind:href="`/posts/${post.id}`">More Info!</a>
      <br />
      <br />
    </div>
  </div>
</template>

<style>
.selected {
  background-color: lightblue;
}
</style>
