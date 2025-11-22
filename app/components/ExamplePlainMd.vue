<script setup lang="ts">
import { markdown } from '#shared/constants';
import markdownit from 'markdown-it';

const md = markdownit();
const result = md.render(markdown);
</script>

<template>
  <h2>Plain Markdown</h2>
  <p>
    🚨 This example will just use plain HTML rendering via <code>v-html</code>,
    so the link will force a page reload:
  </p>
  <div v-html="result"></div>
</template>
