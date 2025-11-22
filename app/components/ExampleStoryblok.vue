<script setup lang="ts">
import { NuxtLink } from '#components';
import { markdown } from '#shared/constants';
import type { StoryblokRichTextNode } from '@storyblok/vue';
import { StoryblokRichText } from '@storyblok/vue';
import { MarkTypes } from '@storyblok/richtext';
import { markdownToStoryblokRichtext } from '@storyblok/richtext/markdown-parser';

const richtextDoc = markdownToStoryblokRichtext(markdown);

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

  <section>
    <p>
      🚨 This example does <strong>not</strong> use a custom link resolver, so
      the link will force a page reload:
    </p>
    <StoryblokRichText :doc="richtextDoc" />
  </section>
  <section>
    <p>
      ✅ This example uses a custom link resolver, so the link will use
      <code>&lt;NuxtLink&gt;</code> and not force a page reload:
    </p>
    <StoryblokRichText :doc="richtextDoc" :resolvers="resolvers" />
  </section>
</template>
