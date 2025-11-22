<script setup lang="ts">
import { markdown } from '#shared/constants';
import { parseMarkdown } from '@nuxtjs/mdc/runtime';

const { data: ast } = await useAsyncData('md', () => parseMarkdown(markdown));
</script>

<template>
  <h2>MDC</h2>
  <p>
    ✅ This example uses MDC's built-in rendering, so the link will use
    <code>&lt;NuxtLink&gt;</code> and not force a page reload:
  </p>
  <MDCRenderer v-if="ast?.body" :body="ast.body" :data="ast.data" />
</template>
