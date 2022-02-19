<template>
  <div class="list">
    <h2 class=""> RESUMES</h2>
    <div  v-for="resume in resumes" :key="resume.id">
      <ResumeComp :resume="resume" :dlt="dlt" :edit="edit" />
    </div>
    <CreateComp :create="create" />
  </div>
</template>
<script>
import axios from "axios";
import ResumeComp from "../components/ResumeComp.vue";
import CreateComp from "../components/CreateComp.vue";
export default {
  name: "App",
  data() {
    return {
      resumes: [],
      componenKey: 0,
    };
  },
  async created() {
    this.getAll();
  },
  components: {
    ResumeComp,
    CreateComp,
  },
  methods: {
    async getAll() {
      const { data } = await axios.get("http://localhost:8000/resume/get/");
      this.resumes = [...data];
      console.log(this.resumes);
    },
    async dlt(id) {
      await axios
        .delete("http://localhost:8000/resume/delete/", {
          data: {
            pk: id,
          },
        })
        .catch((e) => console.log(e));
      this.getAll();
    },
    async edit(id, newText, user) {
      await axios
        .post("http://localhost:8000/resume/edit/", {
          pk: id,
          text: newText,
          user: user,
        })
        .catch((e) => console.log(e));
      this.getAll();
    },
    async create(text, user) {
      await axios
        .post("http://localhost:8000/resume/create/", {
          text: text,
          user: user,
        })
        .catch((e) => alert(e));
      this.getAll();
    },
  },
};
</script>
<style scoped>
.list{
  margin-top: 100px;
}
h2{
  text-align: center;
}
</style>