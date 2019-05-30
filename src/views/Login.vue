<template>
  <div class="about">
    <div>
      <form @submit.prevent="login">
        <h1>Login</h1>
        <p>Sign In to your account</p>
        <input
          type="text"
          placeholder="Username"
          v-model="credentials.username"
          autocomplete="username"
        >

        <input
          type="password"
          placeholder="Password"
          v-model="credentials.password"
          autocomplete="current-password"
        >

        <div class="bg-background mb-3 p-3 bg-light text-danger" v-show="error">{{ error }}</div>
        <button type="submit" class="px-4">Login</button>
      </form>
    </div>
  </div>
</template>

<script>
import axios from "axios";

export default {
  data() {
    return {
      credentials: {
        username: "",
        password: ""
      },
      error: ""
    };
  },
  methods: {
    login() {
      axios
        .post("some url", this.credentials)
        .then(res => {
          console.log(res);
          localStorage.setItem("token", res.data.token);
        })
        .catch(err => {
          console.log(err);
        });
    }
  }
};
</script>
