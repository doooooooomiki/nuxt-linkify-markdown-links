<script setup lang="ts">
import markdownit from 'markdown-it';

const md = markdownit();
const markdown = 'A link to [about](/about) *forcing* a page reload.';
const result = md.render(markdown);
</script>

<template>
  <h2>Plain Markdown</h2>
  <div v-html="result"></div>
</template>
