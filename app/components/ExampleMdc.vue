<script setup lang="ts">
import { parseMarkdown } from '@nuxtjs/mdc/runtime';

const markdown = 'A link to [about](/about) *without* forcing a page reload.';
const { data: ast } = await useAsyncData('md', () => parseMarkdown(markdown));
</script>

<template>
  <h2>MDC</h2>
  <MDCRenderer v-if="ast?.body" :body="ast.body" :data="ast.data" />
</template>
