<template>
  <div class="about">
    <div>
      <form @submit.prevent="signup">
        <h1>Sign Up</h1>
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

        <input type="password" placeholder="Confirm Password" v-model="credentials.confirmPassword">
        <p v-if="passwordError">{{passwordError}}</p>

        <div class="bg-background mb-3 p-3 bg-light text-danger" v-show="error">{{ error }}</div>
        <button type="submit" class="px-4">signup</button>
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
        password: "",
        confirmPassword: ""
      },
      error: "",
      passwordError: null
    };
  },
  methods: {
    signup() {
      this.credentials.password !== this.credentials.confirmPassword
        ? (this.passwordError = "Passwords do not match")
        : (this.passwordError = null);

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