<template>
  <article>
    <h1>{{ article.title }}</h1>
    <p>{{ article.description }}</p>
    <img :src="article.img" :alt="article.alt" />
    <p>0309</p>
    <pre> {{ article }} </pre>
    <p>Post last updated: {{ article.updatedAt }}</p>
    <p>Article last updated: {{ formatDate(article.updatedAt) }}</p>
    <br>
    <nuxt-content :document="article" />
  </article>
</template>





<script>
  export default {
    async asyncData({ $content, params }) {
      const article = await $content('articles', params.slug).fetch()

      return { article }
    },
    methods: {
      formatDate(date) {
        const options = { year: 'numeric', month: 'long', day: 'numeric' }
        return new Date(date).toLocaleDateString('en', options)
      }
    }
  }
</script>
