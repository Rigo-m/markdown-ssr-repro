

<script setup lang="ts">
import type { MarkdownProps } from "./Markdown.props"
const { $markdown } = useNuxtApp()
const props = withDefaults(defineProps<MarkdownProps>(), {
  inline: true,
  tag: "p",
})
// renderInline() removes the <p> tag
const markdownContent = computed(() =>
  props.inline
    ? $markdown.renderInline(props.content)
    : $markdown.render(props.content)
)
const renderedTag = computed(() => (!props.inline ? "div" : props.tag))
</script>

<template>
  <component :is="renderedTag" class="markdown-content__markdown" v-html="markdownContent" />
</template>