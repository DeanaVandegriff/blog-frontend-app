<script>
import axios from "axios";
export default {
  data: function () {
    return {
      newPostsParams: { body: "" },
      errors: [],
      status: "",
    };
  },
  methods: {
    createPost: function () {
      console.log("make a new post");
      axios
        .post("http://localhost:3000/posts", this.newPostsParams)
        .then((response) => {
          console.log("success", response.data);
          this.posts.push(response.data);
        })
        .catch((error) => console.log(error.response));
    },
  },
};
</script>

<template>
  <div class="posts-new">
    <img v-if="status" v-bind:src="`https://http.cat/${status}`" alt="" />
    <form v-on:submit.prevent="createPost()">
      <h1>Make a post!!</h1>
      <div>
        <div class="post-group">
          title:
          <input type="text" v-model="newPostsParams.title" />
        </div>
        <div class="post-group">
          body:
          <input type="text" v-model="newPostsParams.body" />
          <small>{{ 120 - newPostsParams.body.length }} characters remaining</small>
        </div>
        <div class="post-group">
          image:
          <input type="text" v-model="newPostsParams.image" />
        </div>
        <div class="post-group">
          user_id:
          <input type="text" v-model="newPostsParams.user_id" />
        </div>
      </div>
      <input type="submit" value="createPost" />
    </form>
  </div>
</template>
