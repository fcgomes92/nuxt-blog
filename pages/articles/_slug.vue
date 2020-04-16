<template>
  <v-layout column justify-center align-center>
    <v-flex xs12>
      <component :is="postComponent" />
    </v-flex>
  </v-layout>
</template>

<script>
export default {
  async asyncData({ params, error }) {
    try {
      const post = await import(`~/content/articles/${params.slug}.md`);
      return {
        postComponent: post.vue.component,
      };
    } catch (err) {
      error({
        statusCode: 404,
        message: 'Article not found',
        redirect: {
          name: 'Articles',
          path: '/articles',
        },
      });
    }
  },
};
</script>

<style lang="scss">
.frontmatter-markdown {
  img {
    max-width: 100%;
    width: auto;
  }
}
</style>
