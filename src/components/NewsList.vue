<template>
  <div class="container">
    <div class="card" v-for="article in articles" v-bind:key="article.publishedAt">
      <div class="row">
        <div class="col-md-3 image-container text-center">
          <img class="image" :src="article.urlToImage" alt="Card image cap">
        </div>
        <div class="col-md-9">
          <div class="card-block">
            <h4 class="card-title">{{article.title}}</h4>
            <p class="card-text">{{article.description}}</p>
            <a :href="article.url" target="_blank" class="btn btn-primary">Read more...</a>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from 'axios';
export default {
  name: 'newslist',
  props: ['source'],
  data() {
    return {
      articles: []
    }
  },
  methods: {
    fetchNews: function (source) {
      axios.get(`https://newsapi.org/v1/articles?source=${source.id}&apiKey=49f76f8896a1480b97fe31fa4d32cbea`).then(response => this.articles = response.data.articles);
    }
  },
  watch: {
    source: function (val) {
      if (val) {
        this.fetchNews(val);
      } else {
        this.articles = [];
      }
    }
  }
}
</script>

<style>
.card {
  margin-bottom: 10px;
}

.image {
  width: 100%;
  height: 100%;
}
</style>
