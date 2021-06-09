<!-- eslint-disable vue/no-v-html -->
<template>
  <div id="markdown" v-html="renderInput"></div>
</template>
<script>
import marked from 'marked';

export default {
  props: {
    input: {
      type: String,
      required: true,
    },
  },
  computed: {
    renderInput() {
      return marked(this.input, { sanitize: true });
    },
  },
};
</script>
