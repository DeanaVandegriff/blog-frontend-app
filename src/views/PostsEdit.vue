<script>
import axios from "axios";

export default {
  data: function () {
    return {
      post: {},
      editPostParams: {},
    };
  },
  created: function () {
    axios.get("http://localhost:3000/posts/" + this.$route.params.id + "json").then((response) => {
      console.log(response.data);
      this.post = response.data;
    });
  },
  methods: {
    updatePost: function () {
      console.log("Update a recipe!");
      axios.patch("http://localhost3000/posts/" + this.$route.params.id + "json", this.post).then((response) => {
        console.log("Success", response.data);
        this.$router.push("/posts");
      });
    },
  },
};
</script>

<template>
  <div class="posts-edit">
    <form v-on:submit.prevent="updatePost()">
      <h1>Update a post!!</h1>
      <div>
        <div class="post-group">
          title:
          <input type="text" v-model="editPostsParams.title" />
        </div>
        <div class="post-group">
          body:
          <input type="text" v-model="editPostsParams.body" />
        </div>
        <div class="post-group">
          image:
          <input type="text" v-model="editPostsParams.image" />
        </div>
        <div class="post-group">
          user_id:
          <input type="text" v-model="editPostsParams.user_id" />
        </div>
      </div>
      <input type="submit" value="editsPost" />
    </form>
    <a href="`/posts/${post.id}`">Back to all posts!</a>
  </div>
</template>
