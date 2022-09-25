<template>
  <!-- Loading -->
  <Loading v-if="$fetchState.pending" />

  <!-- Movie Info -->
  <div
    v-else
    class="
      container
      min-h-screen
      flex flex-col
      justify-center
      py-8
      px-4
      text-white
    "
  >
    <NuxtLink class="btn mb-8" :to="{ name: 'index' }"> Back </NuxtLink>
    <div class="flex flex-col items-center gap-8 md:flex-row md:items-start">
      <div class="min-h-[500px] w-full md:max-h-[700px] md:w-[initial]">
        <img
          :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`"
          alt=""
        />
      </div>
      <div class="">
        <h1 class="text-[56px] font-normal">Title: {{ movie.title }}</h1>
        <p class="mt-3 text-xl leading-6">
          <span class="font-semibold underline-offset-1">Tagline:</span> "{{ movie.tagline }}"
        </p>
        <p class="mt-3 text-xl leading-6">
          <span>Released:</span>
          {{
            new Date(movie.release_date).toLocaleString("en-us", {
              month: "long",
              day: "numeric",
              year: "numeric",
            })
          }}
        </p>
        <p class="mt-3 text-xl leading-6">
          <span>Duration:</span> {{ movie.runtime }} minutes
        </p>
        <p class="">
          <span>Revenue:</span>
          {{
            movie.revenue.toLocaleString("en-us", {
              style: "currency",
              currency: "USD",
            })
          }}
        </p>
        <p class="mt-3 text-xl leading-6"><span>Overview:</span> {{ movie.overview }}</p>
      </div>
    </div>
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
