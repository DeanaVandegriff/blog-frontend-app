<script>
export default {
  data: function () {
    return {
      isLoggedIn: !!localStorage.jwt,
    };
  },
  watch: {
    $route: function () {
      this.isLoggedIn = !!localStorage.jwt;
    },
  },
  methods: {
    getUserId: function () {
      return localStorage.getItem("user_id");
    },
  },
};
</script>

<template>
  <nav>
    <span>
      <router-link to="/">Home</router-link>
    </span>
    |
    <span>
      <router-link to="/about">About</router-link>
    </span>
    |
    <span>
      <router-link to="/posts">Posts</router-link>
    </span>
    |
    <span v-if="!isLoggedIn">
      <router-link to="/login">Login</router-link>
    </span>
    |
    <span v-if="isLoggedIn">
      <router-link to="/logout">Logout</router-link>
    </span>
    |
    <span>
      <router-link to="/posts/new">Create a Post</router-link>
    </span>
    |
    <span v-if="!isLoggedIn">
      <router-link to="/signup">Signup</router-link>
    </span>
  </nav>
  <div class="container">
    <router-view />
  </div>
</template>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
