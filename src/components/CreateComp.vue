<template>
  <div>
    <v-btn
      @click="showCreate=true"
      showCreate="false;"
      color="primary"
      class="content"
      fab
      dark
    >
       <v-icon dark>
        mdi-plus
      </v-icon>
    </v-btn>
    <v-dialog v-model="showCreate" persistent width="600">
      <div class="dialog">
        <v-textarea class="textarea" filled  v-model="text" label="text"></v-textarea>
        <v-text-field v-model="user" type="number" label="user"></v-text-field>
        <v-btn
          @click="cliclHandeler"
          showCreate="false;"
          color="primary"
          class="ml-4 mb-4"
        >
          create
        </v-btn>
        <v-btn
          @click="
            showCreate = false;
          "
          color="error"
          class="ml-4 mb-4"
        >
          cancel
        </v-btn>
      </div>
    </v-dialog>
  </div>
</template>
<script>
export default {
  name: "CreateComp",
  data() {
    return {
      user: null,
      text: "",
      showCreate: false,
    };
  },
  props: {
    create: Function,
  },
  methods: {
    cliclHandeler() {
      this.create(this.text, this.user);
      this.text = "";
      this.user = null;
    },
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

.content{
  position:fixed !important;
  right: 10vw;
  bottom:  100px;
}

</style>