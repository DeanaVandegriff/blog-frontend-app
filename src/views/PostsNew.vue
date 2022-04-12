<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newPostParams: {},
    };
  },

  methods: {
    createPost: function () {
      console.log("Creating a New Blog Post");

      axios.post("http://localhost:3000.json", this.newPostParams).then((response) => {
        console.log("Sucess", response.data);
        this.posts.push(response.data);
      });
    },
  },
};
</script>

<template>
  <div class="posts-new">
    <form v-on:submit.prevent="createPost()">
      <h1>This is the place to make a new post!</h1>

      <div>
        <div class="form-group">
          title:
          <input type="text" v-model="newPostParams.title" />
        </div>
        <div class="form-group">
          body:
          <input type="text" v-model="newPostParams.body" />
        </div>
        <div class="form-group">
          image:
          <input type="text" v-model="newPostParams.image" />
        </div>
      </div>
      <input type="submit" value="create" />
    </form>
  </div>
</template>
