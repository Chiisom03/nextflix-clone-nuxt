<template>
  <div>
    <Hero />

    <div class="">
      <div class="">
        <div id="movie-grid" class="">
          <div class="" v-for="(movie, idx) in movies" :key="idx">
            <div class="">
              <img
                :src="`https://image.tmbd.org/t/p/${movie.poster_path}`"
                alt=""
              />
              <p class="">{{ movie.vote_average }}</p>
              <p class="">{{ movie.overview }}</p>
            </div>
            <div class="">
              <p class="title">
                {{ movie.title.slice(0, 25) }}
                <span v-if="movie.title.length > 25">...</span>
              </p>
              <p class="release">
                Released:
                {{
                  new Date(movie.release_date).toLocaleDateString("en-us", {
                    month: "long",
                    day: "numeric",
                    year: "numeric",
                  })
                }}
              </p>
              <NuxtLink
                class="btn"
                :to="{
                  name: 'movies-movieID',
                  params: { movies: movieID },
                }"
              ></NuxtLink>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
import Hero from "../components/Hero.vue";
import axios from "axios";
export default {
  name: "IndexPage",
  components: { Hero },
  data() {
    return {
      movies: [],
    };
  },
  async fetch() {
    await this.getMovies();
  },
  methods: {
    async getMovies() {
      const data = axios.get(
        "https://api.themoviedb.org/3/movie/now_playing?api_key=37ed43a4f8eaa2abd75f9283692947bc&language=en-US&page=1"
      );
      const result = await data;
      result.data.results.forEach((movie) => {
        this.movies.push();
      });
    },
  },
};
</script>
