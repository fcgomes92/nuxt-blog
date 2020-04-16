<template>
  <div>
    <h1>My blog posts</h1>
    <ul>
      <li v-for="post in posts" :key="post.attributes.title">
        <NuxtLink :to="getArticlePost(post)">
          {{ post.attributes.title }}
        </NuxtLink>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name: 'Articles',
  data() {
    const resolve = require.context('~/content/articles/', true, /\.md$/);
    const imports = resolve.keys().map(key => {
      return resolve(key);
    });
    return {
      posts: imports,
      prefix: 'articles',
    };
  },
  methods: {
    getArticlePost(post) {
      return `${this.prefix}/${
        post.meta.resourcePath
          .split('\\')
          .pop()
          .split('/')
          .pop()
          .split('.')[0]
      }`;
    },
  },
};
</script>
