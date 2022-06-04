<template>
  <ThemeLayout>
    <h2 class="text-2xl leading-7 font-semibold">
      {{ $t('welcome') }}
    </h2>
    <div
      v-for="(post, index) in posts"
      :key="post.title || index"
      class="mt-4 pt-4 text-gray-800 border-t border-dashed"
    >
      <a class="text-base font-semibold">{{ post.title }}</a>
      <div class="mt-2 text-sm">{{ post.description }}</div>
      <nuxt-link :to="localePath(post.path)" class="text-sm mt-2">
        <button :to="localePath(post.path)" class="btn btn-teal">
          {{ $t('read-more') }}
        </button>
      </nuxt-link>
    </div>
  </ThemeLayout>
</template>

<script lang="ts">
import { IContentDocumentBase } from '@nuxt/content/types/content'
import Vue from 'vue'

export default Vue.extend({
  name: 'IndexPage',
  async asyncData({ $content, app }) {
    const locale = app.i18n.locale
    const data = await $content('posts')
      .where({ slug: { $contains: [`.${locale}`] } })
      .fetch()
    const posts = data as IContentDocumentBase[]
    return {
      posts: posts.map((post) => {
        const { path, ...restFields } = post
        return {
          ...restFields,
          path: path.substring(0, path.lastIndexOf(locale) - 1),
        }
      }),
    }
  },
})
</script>
