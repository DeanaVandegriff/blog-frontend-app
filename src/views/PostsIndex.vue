<script>
import axios from "axios";
import moment from "moment";

export default {
  data: function () {
    return {
      posts: [],
      currentPost: {},
      titleFilter: "",
    };
  },
  created: function () {
    axios.get("http://localhost:3000/posts.json").then((response) => {
      this.posts = response.data;
      console.log("Posts", this.posts);
    });
  },
  methods: {
    relativeDate: function (date) {
      return moment(date).fromNow();
    },
    filterPosts: function () {
      return this.posts.filter((post) => {
        var lowerTitle = post.title.toLowerCase();
        var lowerTitleFilter = this.titleFilter.toLowerCase();
        return lowerTitle.includes(lowerTitleFilter);
      });
    },
  },
};
</script>

<template>
  <h1>These are my blog posts!</h1>
  <div class="index">
    <input v-model="titleFilter" type="text" list="titles" />
    <datalist id="titles">
      <option v-for="post in posts" v-bind:key="post.id">{{ posts.title }}</option>
    </datalist>
    <div v-for="post in filterPosts()" v-on:click="currentPost = post" v-bind:key="post.id">
      <div v-bind:class="{ selected: post === currentPost }">
        <h2>{{ post.title }}</h2>
        <img :src="post.image" v-bind:alt="post.title" />
        <p>Created: {{ relativeDate(post.created_at) }}</p>
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
