<template>
  <div class="editor" v-if="editor">
    <editor-btn-group class="editor__header" :editor="editor" />
    <v-btn>change html</v-btn>
    <editor-content class="editor__content" :editor="editor" />
  </div>
</template>

<script>
import { Editor, EditorContent } from "@tiptap/vue-2";
import CharacterCount from "@tiptap/extension-character-count";
import Highlight from "@tiptap/extension-highlight";
import TaskItem from "@tiptap/extension-task-item";
import TaskList from "@tiptap/extension-task-list";
import TextAlign from "@tiptap/extension-text-align";
import StarterKit from "@tiptap/starter-kit";
import History from "@tiptap/extension-history";
import Underline from "@tiptap/extension-underline";

import EditorBtnGroup from "./EditorBtnGroup.vue";

export default {
  name: "TextEditor",
  components: {
    EditorContent,
    EditorBtnGroup,
  },
  data() {
    return {
      editor: null,
    };
  },

  mounted() {
    console.log("gu");
    this.editor = new Editor({
      extensions: [
        StarterKit.configure({
          history: false,
        }),
        History,
        Highlight,
        TaskList,
        TaskItem,
        Underline,
        TextAlign.configure({
          types: ["heading", "paragraph"],
        }),
        CharacterCount.configure({
          limit: 10000,
        }),
      ],
      content: "",
      onUpdate: () => {
        console.log(this.editor.commands);
        console.log(this.editor.getHTML());
      },
    });
    // this.editor = new Editor({
    //   content: this.value,
    //   extensions: [
    //     StarterKit.configure({
    //       // Disable an included extension
    //       // history: false,

    //       // Configure an included extension
    //       heading: {
    //         levels: [1, 2, 3, 4],
    //       },
    //     }),
    //   ],

    //   onUpdate: () => {
    //     // console.log(this.editor.commands.set);
    //     // HTML
    //     // this.$emit("input", this.editor.getHTML());
    //     // JSON ==> 디비 저장?
    //     // this.$emit("input", this.editor.getJSON());
    //   },
    // });
  },

  beforeDestroy() {
    this.editor.destroy();
  },
};
</script>

<style lang="scss">
.editor {
  background-color: #fff;
  border: 3px solid #0d0d0d;
  // border-radius: 0.75rem;
  color: #0d0d0d;
  display: flex;
  flex-direction: column;
  max-height: 26rem;

  &__header {
    align-items: center;
    background: #5d5d5d;
    border-bottom: 3px solid #5d5d5d;
    // border-top-left-radius: 0.25rem;
    // border-top-right-radius: 0.25rem;
    display: flex;
    flex: 0 0 auto;
    flex-wrap: wrap;
    padding: 0.25rem;
  }

  &__content {
    flex: 1 1 auto;
    overflow-x: hidden;
    overflow-y: auto;
    padding: 1.25rem 1rem;
    -webkit-overflow-scrolling: touch;
  }

  // &__footer {
  //   align-items: center;
  //   border-top: 3px solid #0d0d0d;
  //   color: #0d0d0d;
  //   display: flex;
  //   flex: 0 0 auto;
  //   flex-wrap: wrap;
  //   font-size: 12px;
  //   font-weight: 600;
  //   justify-content: space-between;
  //   padding: 0.25rem 0.75rem;
  //   white-space: nowrap;
  // }

  /* Some information about the status */
  // &__status {
  //   align-items: center;
  //   border-radius: 5px;
  //   display: flex;

  //   &::before {
  //     background: rgba(#0d0d0d, 0.5);
  //     border-radius: 50%;
  //     content: " ";
  //     display: inline-block;
  //     flex: 0 0 auto;
  //     height: 0.5rem;
  //     margin-right: 0.5rem;
  //     width: 0.5rem;
  //   }

  //   &--connecting::before {
  //     background: #616161;
  //   }

  //   &--connected::before {
  //     background: #b9f18d;
  //   }
  // }

  // &__name {
  //   button {
  //     background: none;
  //     border: none;
  //     border-radius: 0.4rem;
  //     color: #0d0d0d;
  //     font: inherit;
  //     font-size: 12px;
  //     font-weight: 600;
  //     padding: 0.25rem 0.5rem;

  //     &:hover {
  //       background-color: #0d0d0d;
  //       color: #fff;
  //     }
  //   }
  // }
}
.ProseMirror:focus {
  outline: none;
}
/* Give a remote user a caret */
// .collaboration-cursor__caret {
//   border-left: 1px solid #0d0d0d;
//   border-right: 1px solid #0d0d0d;
//   margin-left: -1px;
//   margin-right: -1px;
//   pointer-events: none;
//   position: relative;
//   word-break: normal;
// }

/* Render the username above the caret */
// .collaboration-cursor__label {
//   border-radius: 3px 3px 3px 0;
//   color: #0d0d0d;
//   font-size: 12px;
//   font-style: normal;
//   font-weight: 600;
//   left: -1px;
//   line-height: normal;
//   padding: 0.1rem 0.3rem;
//   position: absolute;
//   top: -1.4em;
//   user-select: none;
//   white-space: nowrap;
// }

/* Basic editor styles */
.tiptap {
  > * + * {
    margin-top: 0.75em;
  }

  ul,
  ol {
    padding: 0 1rem;
  }

  h1,
  h2,
  h3,
  h4,
  h5,
  h6 {
    line-height: 1.1;
  }

  code {
    background-color: rgba(#616161, 0.1);
    color: #616161;
  }

  pre {
    background: #0d0d0d;
    border-radius: 0.5rem;
    color: #fff;
    font-family: "JetBrainsMono", monospace;
    padding: 0.75rem 1rem;

    code {
      background: none;
      color: inherit;
      font-size: 0.8rem;
      padding: 0;
    }
  }

  mark {
    background-color: #faf594;
  }

  img {
    height: auto;
    max-width: 100%;
  }

  hr {
    margin: 1rem 0;
  }

  blockquote {
    border-left: 2px solid rgba(#0d0d0d, 0.1);
    padding-left: 1rem;
  }

  hr {
    border: none;
    border-top: 2px solid rgba(#0d0d0d, 0.1);
    margin: 2rem 0;
  }

  ul[data-type="taskList"] {
    list-style: none;
    padding: 0;

    li {
      align-items: center;
      display: flex;

      > label {
        flex: 0 0 auto;
        margin-right: 0.5rem;
        user-select: none;
      }

      > div {
        flex: 1 1 auto;
      }
    }
  }
}
</style>
