<script>
import axios from "axios";

export default {
  data: function () {
    return {
      newSessionParams: {},
      errors: [],
    };
  },
  methods: {
    submit: function () {
      axios
        .post("/sessions", this.newSessionParams)
        .then((response) => {
          axios.defaults.headers.common["Authorization"] = "Bearer " + response.data.jwt;
          localStorage.setItem("jwt", response.data.jwt);
          this.$router.push("/");
        })
        .catch((error) => {
          console.log(error.response);
          this.errors = ["Invalid email or password."];
          this.email = "";
          this.password = "";
        });
    },
  },
};
</script>

<template>
  <div class="login">
    <form v-on:submit.prevent="submit()">
      <h1>Login</h1>
      <ul>
        <li v-for="error in errors" v-bind:key="error">{{ error }}</li>
      </ul>
      <div>
        <label class="form-label">Email:</label>
        <input type="email" v-model="newSessionParams.email" class="form-control" />
      </div>
      <div>
        <label class="form-label">Password:</label>
        <input type="password" v-model="newSessionParams.password" class="form-control" />
      </div>
      <input type="submit" value="Submit" class="btn-primary mt-4" />
    </form>
  </div>
</template>
