<template>
  <div class="container text-center">
    <img src="./assets/marvel.jpg" class="bg position-fixed top-0 w-100 vh-full" alt="">
    <div class="row">
      <div class="col-4 offset-4">
        <h1 class="title p-3">Apple news.</h1>
      </div>
    </div>
    <div class="row">
      <div class="col-6 mt-4" v-for="(item, index) in searchResults.articles" :key="index">
        <div class="card h-100">
          <h2 class="card__title p-4">{{ item.title }}</h2>
          <img :src="item.urlToImage" class="card__img w-100" />
          <p class="card__description p-3 pb-0">
            {{item.description}}
          </p>
          <p class="card__text">Published by <a class="card__link" :href="item.url" target="_blank">{{ item.source.name }}</a></p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import axios from "axios";
export default {
  data() {
    return {
      base_url: 'https://newsapi.org/v2/everything?q=apple&from=2021-11-04&to=2021-11-04&sortBy=popularity&apiKey=',
      api_key: '00ec4b3f07d642568e8b1570739468a3',
      searchResults: {}
    };
  },
  created: function() {
        this.search();
  },
  methods: {
    search() {
      axios.get(this.base_url + this.api_key)
      .then(response => {
        this.searchResults = response.data
        console.log(this.searchResults);
      })
      .catch(e => {
        console.log(e)
      })
    },
  }
};
</script>

<style lang="scss">
.card__link{
  text-decoration: none;
  color: aqua;
}
.bg{ 
  z-index: -1;
  left: 0;
}
.title {
  color: white;
}
.card__title{
  font-size: 20px;
}
.card__img{
  height: 250px;
}
 
</style>
