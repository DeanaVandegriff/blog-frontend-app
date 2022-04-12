<script>
import axios from "axios";

export default {
  data: function () {
    return {
      post: {},
    };
  },
  created: function () {
    axios.get("http://localhost:3000/posts/1.json").then((response) => {
      console.log(response.data);
      this.post = response.data;
    });
  },
};
</script>

<template>
  <h1>Posts show</h1>
  <p>{{ posts }}</p>
  <a href="/posts">Back to all posts!</a>
</template>
