<template>
  <div>
    <template v-for="(item, index) in items">
      <div
        class="divider"
        v-if="item.type === 'divider'"
        :key="`divider${index}`"
      ></div>
      <menu-item v-else :key="index" v-bind="item" />
    </template>
  </div>
</template>

<script>
import MenuItem from "./MenuItem.vue";

export default {
  components: {
    MenuItem,
  },

  props: {
    editor: {
      type: Object || null,
      required: true,
    },
  },

  data() {
    return {
      items: [
        {
          icon: "format-bold",
          title: "Bold",
          action: () => this.editor.chain().focus().toggleBold().run(),
          isActive: () => this.editor.isActive("bold"),
        },
        {
          icon: "format-italic",
          title: "Italic",
          action: () => this.editor.chain().focus().toggleItalic().run(),
          isActive: () => this.editor.isActive("italic"),
        },
        {
          icon: "format-underline",
          title: "Underline",
          action: () => this.editor.chain().focus().toggleUnderline().run(),
          isActive: () => this.editor.isActive("underline"),
        },
        {
          icon: "format-strikethrough",
          title: "Strike",
          action: () => this.editor.chain().focus().toggleStrike().run(),
          isActive: () => this.editor.isActive("strike"),
        },
        {
          icon: "format-color-fill",
          title: "Highlight",
          action: () => this.editor.chain().focus().toggleHighlight().run(),
          isActive: () => this.editor.isActive("highlight"),
        },
        {
          icon: "format-color-text",
          title: "Color Text",
          action: () => this.editor.chain().focus().toggleHighlight().run(),
          isActive: () => this.editor.isActive("highlight"),
        },
        {
          type: "divider",
        },
        {
          icon: "format-align-justify",
          title: "align justify",
          action: () =>
            this.editor.chain().focus().setTextAlign("justify").run(),
          isActive: () => this.editor.isActive({ textAlign: "justify" }),
        },
        {
          icon: "format-align-center",
          title: "align center",
          action: () =>
            this.editor.chain().focus().setTextAlign("center").run(),
          isActive: () => this.editor.isActive({ textAlign: "center" }),
        },
        {
          icon: "format-align-left",
          title: "align left",
          action: () => this.editor.chain().focus().setTextAlign("left").run(),
          isActive: () => this.editor.isActive({ textAlign: "left" }),
        },
        {
          icon: "format-align-right",
          title: "align right",
          action: () => this.editor.chain().focus().setTextAlign("right").run(),
          isActive: () => this.editor.isActive({ textAlign: "right" }),
        },
        {
          type: "divider",
        },
        {
          icon: "format-header-1",
          title: "Heading 1",
          action: () =>
            this.editor.chain().focus().toggleHeading({ level: 1 }).run(),
          isActive: () => this.editor.isActive("heading", { level: 1 }),
        },
        {
          icon: "format-header-2",
          title: "Heading 2",
          action: () =>
            this.editor.chain().focus().toggleHeading({ level: 2 }).run(),
          isActive: () => this.editor.isActive("heading", { level: 2 }),
        },
        {
          icon: "format-header-3",
          title: "Heading 3",
          action: () =>
            this.editor.chain().focus().toggleHeading({ level: 3 }).run(),
          isActive: () => this.editor.isActive("heading", { level: 3 }),
        },
        {
          icon: "format-header-4",
          title: "Heading 4",
          action: () =>
            this.editor.chain().focus().toggleHeading({ level: 4 }).run(),
          isActive: () => this.editor.isActive("heading", { level: 4 }),
        },
        {
          icon: "format-paragraph",
          title: "Paragraph",
          action: () => this.editor.chain().focus().setParagraph().run(),
          isActive: () => this.editor.isActive("paragraph"),
        },
        {
          icon: "format-list-bulleted",
          title: "Bullet List",
          action: () => this.editor.chain().focus().toggleBulletList().run(),
          isActive: () => this.editor.isActive("bulletList"),
        },
        {
          icon: "format-list-numbered",
          title: "Numbered List",
          action: () => this.editor.chain().focus().toggleOrderedList().run(),
          isActive: () => this.editor.isActive("orderedList"),
        },
        {
          type: "divider",
        },
        {
          icon: "wrap",
          title: "Hard Break",
          action: () => this.editor.chain().focus().setHardBreak().run(),
        },
        {
          icon: "format-clear",
          title: "Clear Format",
          action: () =>
            this.editor.chain().focus().clearNodes().unsetAllMarks().run(),
        },
        {
          icon: "arrow-left",
          title: "Undo",
          action: () => this.editor.chain().focus().undo().run(),
        },
        {
          icon: "arrow-right",
          title: "Redo",
          action: () => this.editor.chain().focus().redo().run(),
        },
      ],
    };
  },
};
</script>

<style lang="scss">
.divider {
  background-color: rgba(#fff, 0.25);
  height: 1.25rem;
  margin-left: 0.5rem;
  margin-right: 0.75rem;
  width: 1px;
}
</style>
