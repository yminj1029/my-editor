<template>
  <div class="text-center">
    <v-dialog
      @click:outside="$emit('close')"
      @keydown.esc="$emit('close')"
      v-model="open"
      width="1000"
    >
      <v-card>
        <text-editor />
      </v-card>
    </v-dialog>
  </div>
</template>
<script>
import TextEditor from "./TextEditor.vue";
export default {
  components: { TextEditor },

  props: {
    openDetail: Boolean,
  },

  data() {
    return {
      open: this.openDetail,
    };
  },

  methods: {},
  computed: {},
  watch: {
    openDetail(newValue) {
      this.open = newValue; // value 프롭이 변경되면 dialog 데이터도 변경
    },
    open(newDialogState) {
      this.$emit("input", newDialogState); // dialog 상태 변경 시 value 프롭에도 반영
    },
  },
};
</script>
