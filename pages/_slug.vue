<template>
  <section class="container">
    <p class="back">
      <nuxt-link exact to="/">⟵ Back to Home</nuxt-link>
    </p>
    <h1>{{ post.fields.title }}</h1>
    <div
      class="image"
      :style="
        `background: url(https:${post.fields.heroImage.fields.file.url}) center center no-repeat`
      "
    ></div>
    <article v-html="$md.render(post.fields.body)"></article>
  </section>
</template>

<script>
export default {
  data() {
    return {
      slug: this.$route.params.slug
    };
  },
  computed: {
    post() {
      let post = this.$store.state.posts.filter(
        el => el.fields.slug === this.slug
      );
      return post[0];
    }
  },
  head() {
    return {
      title: this.post.fields.title
    };
  }
};
</script>

<style lang="scss" scoped>
.back {
  margin-top: 20px;
}

.image {
  width: 100%;
  height: 300px;
  margin: 30px 0;
  background-size: 100% auto !important;
}
</style>
