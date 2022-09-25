<template>
  <Loading v-if="fetchState.pending" />
  <div v-else class="c"></div>
</template>

<script>
import axios from "axios";

export default {
  name: "single-movie",
  data() {
    return {
      movie: null,
    };
  },
  
  async fetch(){
    await this.getSingleMovie()
  },
  fetchDelay: 3000,
  methods: {
    async getSingleMovie() {
      const apiKey = "c3e3b715db7ed78cea000e0969eda5d5";
      axios
        .get(
          `https://api.themoviedb.org/3/movie/${this.$route.params.movieID}?api_key=${apiKey}&language=en-US`
        )
        .then((result) => {
          this.movie = result.data;
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