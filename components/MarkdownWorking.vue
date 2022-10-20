<script lang="ts">
export default defineNuxtComponent({
  props: {
    content: {
      type: String,
      required: true,
    },
    inline: { type: Boolean, required: false, default: true },
    tag: { type: String, required: false, default: 'p' },
  },
  setup(props) {

    const { $markdown } = useNuxtApp()
    // renderInline() removes the <p> tag
    const markdownContent = computed(() =>
      props.inline
        ? $markdown.renderInline(props.content)
        : $markdown.render(props.content)
    )

    const renderedTag = computed(() => (!props.inline ? "div" : props.tag))
    return () => h(renderedTag.value, { class: 'markdown-content__markdown', innerHTML: markdownContent.value })
  }
})
</script>