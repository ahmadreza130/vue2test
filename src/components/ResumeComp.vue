<template>
  <div class="resume">
    <div class="content">
      <v-card elevation="2"
        ><v-card-title>id:{{ resume.id }}</v-card-title
        ><v-card-subtitle>user:{{ resume.user }}</v-card-subtitle
        ><v-card-text>{{ resume.text }}</v-card-text>
        <v-btn color="error" class="ml-4 mb-4" @click="dlt(resume.id)">
          delete
        </v-btn>
        <v-btn
          color="primary"
          class="ml-4 mb-4"
          @click="
            () => {
              showEdit = !showEdit;
            }
          "
        >
          edit
        </v-btn>
      </v-card>

      <v-dialog v-model="showEdit" persistent width="600">
        <div class="dialog">
          <v-textarea filled v-model="newText" label="text"></v-textarea>
          <v-text-field v-model="newUser" type="number" label="user"></v-text-field>
          <v-btn
            @click="
              edit(resume.id, newText, newUser);
              showEdit = false;
            "
            color="primary"
            class="ml-4 mb-4"
          >
            change
          </v-btn>
          <v-btn
            @click="
              showEdit = false;
              newText = resume.text;
              newUser = resume.user;
            "
            color="error"
            class="ml-4 mb-4"
          >
            cancel
          </v-btn>
        </div>
      </v-dialog>
    </div>
  </div>
</template>
<script>
export default {
  name: "ResumeComp",
  props: {
    resume: Object,
    dlt: Function,
    edit: Function,
  },
  data() {
    return {
      newText: this.resume.text,
      newUser: this.resume.user,
      showEdit: false,
    };
  },
};
</script>
<style scoped>
.resume {
  margin-top: 20px;
  display: flex;
  justify-content: center;
}
.dialog {
  padding: 30px;
  background: white;
}
.content {
  width: 60vw;
}

@media (max-width: 1200px) {
  .content {
    width: 85vw;
  }
}
@media (max-width: 750px) {
  .content {
    width: 100vw;
  }
}
</style>
