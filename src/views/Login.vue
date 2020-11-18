<template>
  <div>
    <h1>Login Page</h1>
    <b-form @submit.prevent="pressed">
      <div class="email">
        <b-form-input type="email" placeholder="Email" v-model="email" />
      </div>
      <div class="password">
        <b-form-input
          type="password"
          placeholder="Password"
          v-model="password"
        />
      </div>
      <b-button type="submit">Login</b-button>
    </b-form>
    <div class="error" v-if="error">{{ error.message }}</div>
    <span
      >Need an account? Click here to
      <router-link to="/register">register</router-link></span
    >
  </div>
</template>

<script>
import firebase from "firebase/app";
import "firebase/auth";
export default {
  data() {
    return {
      email: "",
      password: "",
      error: "",
    };
  },
  methods: {
    async pressed() {
      try {
        const val = await firebase
          .auth()
          .signInWithEmailAndPassword(this.email, this.password);
        console.log(val);
        this.$router.replace({ name: "secret" });
      } catch (error) {
        console.log(error);
      }
    },
  },
};
</script>

<style lang="scss" scoped>
.error {
  color: red;
  font-size: 18px;
}
input {
  width: 300px;
  padding: 5px;
  margin: 20px;
  font-size: 18px;
  margin-left: 42%;
}
button {
  width: 200px;
  height: 50px;
  font-size: 100%;
  background-color: #42b983;
  margin-bottom: 10px;
}
</style>
