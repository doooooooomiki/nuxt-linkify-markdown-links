<script setup lang="ts">
import { NuxtLink } from '#components';
import type { StoryblokRichTextNode } from '@storyblok/vue';
import { StoryblokRichText } from '@storyblok/vue';
import { MarkTypes } from '@storyblok/richtext';
import { markdownToStoryblokRichtext } from '@storyblok/richtext/markdown-parser';

const mdForceReload = 'A link to [about](/about) forcing a page reload.';
const richtextDocForceReload = markdownToStoryblokRichtext(mdForceReload);

const mdWithoutReload =
  'A link to [about](/about) without forcing a page reload.';
const richtextDocWithoutReload = markdownToStoryblokRichtext(mdWithoutReload);

// https://www.storyblok.com/docs/packages/storyblok-nuxt#storyblokrichtext
const resolvers = {
  [MarkTypes.LINK]: (node: StoryblokRichTextNode<VNode>) =>
    h(
      NuxtLink,
      {
        to: node.attrs?.href,
        target: node.attrs?.target,
      },
      node.text
    ),
};
</script>

<template>
  <h2>Storyblok</h2>
  <StoryblokRichText :doc="richtextDocForceReload" />
  <StoryblokRichText :doc="richtextDocWithoutReload" :resolvers="resolvers" />
</template>
