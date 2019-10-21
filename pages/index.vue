<template>
  <div class="container">
    <div class="row justify-content-center">
      <b-card
        v-for="(article, index) in articles"
        :key="index"
        no-body
        class="col-6 col-md-4 mb-2"
        :img-src="article.urlToImage"
        img-top
      >
        <template v-slot:header>
          <h4 class="mb-0">{{ article.source.name }}</h4>
        </template>

        <b-card-body>
          <b-card-title>{{ article.author }}</b-card-title>
          <b-card-sub-title class="mb-2">{{ article.title }}</b-card-sub-title>
          <b-card-text>
            {{ article.description }}
          </b-card-text>
        </b-card-body>

        <b-card-footer><a :href="article.url" target="_blank" rel="noopener noreferrer">Read more</a></b-card-footer>
      </b-card>
    </div>
  </div>
</template>

<script>

export default {
 async asyncData({ app }) {
    const { articles } = await app.$axios.$get(
      `https://newsapi.org/v2/everything?q=apple&from=2019-10-20&to=2019-10-20&sortBy=popularity&apiKey=${
        process.env.API_KEY
      }`
    );

    return { articles };
  },
}
</script>
