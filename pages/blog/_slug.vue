<template>
  <div class="max-w-3xl mx-auto min-h-screen my-12">
    <div v-if="post">
      <h1 class="text-2xl font-semibold mb-6">{{ post.name }}</h1>
      <nuxt-content :document="post" />
      <div class="mt-8">
        <nuxt-link to="/" class="hover:underline">Back to blog</nuxt-link>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      post: null,
    }
  },
  async fetch() {
    this.post = (
      await this.$content()
        .where({ slug: this.$route.params.slug })
        .limit(10)
        .fetch()
    )?.[0]
  },
}
</script>
