<template>
  <ThemeLayout>
    <h1>{{ page.title }}</h1>
    <p>{{ page.description }}</p>
    <nuxt-content :document="page" />
  </ThemeLayout>
</template>

<script>
export default {
  async asyncData({ $content, app, error, params }) {
    try {
      const slug = params.slug || 'index'
      const page = await $content('posts', `${slug}.${app.i18n.locale}`).fetch()
      return {
        page,
      }
    } catch (e) {
      error({ statusCode: 404, message: 'Post not found' })
    }
  },
}
</script>
