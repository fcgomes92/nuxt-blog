<template>
  <v-app dark>
    <h1 v-if="error.statusCode === 404">
      <span v-if="error.message">{{ error.message }}</span>
      <span v-else>{{ pageNotFound }}</span>
    </h1>
    <h1 v-else>
      {{ otherError }}
    </h1>
    <NuxtLink v-if="error.redirect" :to="error.redirect.path">
      {{ error.redirect.text }}
    </NuxtLink>
    <NuxtLink v-else to="/">
      Home page
    </NuxtLink>
  </v-app>
</template>

<script>
export default {
  layout: 'empty',
  props: {
    error: {
      type: Object,
      default: null,
    },
  },
  data() {
    return {
      pageNotFound: '404 Not Found',
      otherError: 'An error occurred',
    };
  },
  head() {
    const title =
      this.error.statusCode === 404 ? this.pageNotFound : this.otherError;
    return {
      title,
    };
  },
};
</script>
