<template>
  <div class="text-white">
    {{ movie.title }}
  </div>
</template>

<script>
import axios from "axios";

export default {
  name: "single-movie",
  data() {
    return {
      movie: {},
    };
  },

  async fetch() {
    await this.getSingleMovie();
  },
  fetchDelay: 3000,
  methods: {
    async getSingleMovie() {
      const apiKey = "c3e3b715db7ed78cea000e0969eda5d5";
      const url = `https://api.themoviedb.org/3/movie/${this.$route.query.movieid}?api_key=${apiKey}&language=en-US`;
      axios
        .get(url)
        .then(({ data }) => {
          this.movie = data;
        })
        .catch((error) => {
          alert(error);
        });
    },
  },
};
</script>

<style lang='scss' scoped>
</style>