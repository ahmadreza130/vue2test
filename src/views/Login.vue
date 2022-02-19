<template>
  <div >
    <h3>login</h3>
  <input v-model="username" type="text" placeholder="username" />
  <input v-model="password" type="password" placeholder="password" />
  <button @click="login">login</button>
  <button @click="logout">logout</button>
  </div>
</template>

<script>
// @ is an alias to /src
import axios from "axios"
export default {
  name: 'HomeView',
   data() {
    return {
      username: "",
      password: "",
    };
  },
  methods: {
    async login() {
      const { data } = await axios.post("http://localhost:8000/resume/login/", {
        username: this.username,
        password: this.password,
      });
      localStorage.setItem("token", data);
      this.username = "";
      this.password = "";
    },
     logout() {
      localStorage.removeItem('token')
    },
  },
};

</script>
