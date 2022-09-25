<template>
  <!-- <Loading v-if="fetchState.pending" /> -->
  <div class="text-white">{{ movie.title }}</div>
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
  mounted() {
    this.$fetch();
  },

  async fetch() {
    await this.getSingleMovie();
  },
  fetchDelay: 3000,
  methods: {
    async getSingleMovie() {
      const apiKey = "c3e3b715db7ed78cea000e0969eda5d5";
      const url = `https://api.themoviedb.org/3/movie/${this.$route.params.movieid}?api_key=${apiKey}&language=en-US`;
      console.log(this.$route.params);
      axios
        .get(
          url
        )
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