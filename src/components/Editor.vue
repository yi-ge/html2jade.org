<template>
  <codemirror class="editor" :value="mutableCode" :options="codeMirrorOptions" @focus="onFocus" @input="onCmCodeChange"></codemirror>
</template>

<script>
import "codemirror/addon/selection/active-line.js";
import "codemirror/addon/edit/closetag.js";

export default {
  name: "editor",
  props: ["code", "options", "mode"],
  computed: {
    codeMirrorOptions() {
      return Object.assign(
        {
          tabSize: 2,
          styleActiveLine: true,
          autoCloseTags: true,
          line: true
        },
        this.options
      );
    },
    mutableCode() {
      return this.code;
    }
  },
  methods: {
    onFocus() {
      this.$emit("focus");
    },
    onCmCodeChange(newCode) {
      this.$emit("change", newCode);
    }
  }
};
</script>

<style>
.CodeMirror {
  font-family: "Monaco", "Menlo", "Ubuntu Mono", "Consolas", "source-code-pro",
    monospace;
  text-align: left;
  height: auto;
  padding-left: 5px;
}
</style>
