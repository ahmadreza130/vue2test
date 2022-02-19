<template>
  <div class="container">
    <!-- <h3>login</h3>
  <input v-model="username" type="text" placeholder="username" />
  <input v-model="password" type="password" placeholder="password" />
  <button @click="login">login</button>
  <button @click="logout">logout</button> -->
    <v-form class="form" ref="form" v-model="valid" lazy-validation>
      <h4 class="">Login</h4>
      <v-text-field v-model="username" label="userName" required></v-text-field>

      <v-text-field v-model="password" label="password" required></v-text-field>

      <v-btn color="primary" class="mr-4" @click="login"> Login </v-btn>
      <v-btn color="error" class="mr-4" @click="logout"> logout </v-btn>
    </v-form>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from "axios";
export default {
  name: "HomeView",
  data() {
    return {
      username: "",
      password: "",
    };
  },
  methods: {
    async login() {
      if (!this.username || !this.password) {
        alert("username and password is required");
      } else {
        try {
          const { data } = await axios.post(
            "http://localhost:8000/resume/login/",
            {
              username: this.username,
              password: this.password,
            }
          );
          localStorage.setItem("token", data);
          this.$router.push("/about")
        } catch (e) {
          alert(e);
        }
      }
    },
    logout() {
      localStorage.removeItem("token");
    },
  },
};
</script>
<style scoped>
.container {
  display: flex;
  justify-content: center;
  align-items: center;
  height: 80vh;
}
.form {
  border: 1px solid rgb(233, 226, 226);
  padding: 50px;
  min-width: 500px;
  border-radius: 7px;
}
</style>
