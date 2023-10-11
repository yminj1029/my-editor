<template>
  <v-container v-if="editor">
    <v-btn
      @click="editor.chain().focus().toggleHeading({ level: 1 }).run()"
      :class="{ 'is-active': editor.isActive('heading', { level: 1 }) }"
    >
      H1
    </v-btn>
    <v-btn
      @click="editor.chain().focus().toggleHeading({ level: 2 }).run()"
      :class="{ 'is-active': editor.isActive('heading', { level: 2 }) }"
    >
      H2
    </v-btn>
    <v-btn
      @click="editor.chain().focus().toggleHeading({ level: 3 }).run()"
      :class="{ 'is-active': editor.isActive('heading', { level: 3 }) }"
    >
      H3
    </v-btn>
    <v-btn
      @click="editor.chain().focus().toggleHeading({ level: 4 }).run()"
      :class="{ 'is-active': editor.isActive('heading', { level: 4 }) }"
    >
      H4
    </v-btn>
    <v-btn
      @click="editor.chain().focus().undo().run()"
      :disabled="!editor.can().undo()"
    >
      undo
    </v-btn>
    <v-btn
      @click="editor.chain().focus().redo().run()"
      :disabled="!editor.can().redo()"
    >
      redo
    </v-btn>

    <editor-content :editor="editor" />
    <v-textarea :value="editor.getHTML()"></v-textarea>
  </v-container>
</template>

<script>
import { Editor, EditorContent } from "@tiptap/vue-2";
import StarterKit from "@tiptap/starter-kit";

export default {
  name: "TextEditor",
  components: {
    EditorContent,
  },
  props: {
    value: {
      type: String,
      default: "default",
    },
  },
  data() {
    return {
      editor: null,
    };
  },
  watch: {
    value(value) {
      // HTML
      const isSame = this.editor.getHTML() === value;

      // JSON
      // const isSame = JSON.stringify(this.editor.getJSON()) === JSON.stringify(value)

      if (isSame) {
        return;
      }

      this.editor.commands.setContent(value, false);
    },
  },
  mounted() {
    console.log("gu");
    this.editor = new Editor({
      content: this.value,
      extensions: [
        StarterKit.configure({
          // Disable an included extension
          // history: false,

          // Configure an included extension
          heading: {
            levels: [1, 2],
          },
        }),
      ],

      onUpdate: () => {
        // HTML
        // this.$emit("input", this.editor.getHTML());
        // JSON ==> 디비 저장?
        // this.$emit("input", this.editor.getJSON());
      },
    });
  },

  beforeDestroy() {
    this.editor.destroy();
  },
};
</script>
