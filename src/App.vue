<template>
  <v-app>
    <v-btn @click="open"> open dialog </v-btn>

    <v-main>
      <TextEditor @input="test" />
    </v-main>

    <editor-dialog
      v-if="openDetail"
      :openDetail="openDetail"
      @close="openDetail = false"
    />
  </v-app>
</template>

<script>
import EditorDialog from "./components/EditorDialog.vue";
import TextEditor from "./components/TextEditor";

export default {
  name: "App",

  components: {
    TextEditor,
    EditorDialog,
  },

  data: () => ({
    //
    openDetail: false,
  }),
  methods: {
    open() {
      this.openDetail = true;
    },

    test(data) {
      console.log(data);
    },
  },
};
</script>
