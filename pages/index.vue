<template>
  <div>
    <Hero />

    <div class="py-8 px-4">
      <div
        id="movie-grid"
        class="grid gap-x-8 gap-y-16 grid-cols-1 md:grid-cols-3 lg:grid-cols-4"
      >
        <div
          class="relative flex flex-col"
          v-for="(movie, idx) in movies"
          :key="idx"
        >
          <div
            class="
              relative
              overflow-hidden
              hover:transform hover:translate-y-0
              text-white
            "
          >
            <img
              :src="`https://image.tmdb.org/t/p/w500/${movie.poster_path}`"
              class="block h-full w-full"
              alt=""
            />
            <p
              class="
                absolute
                top-0
                left-0
                flex
                justify-center
                items-center
                w-10
                h-10
                bg-touch
              "
            >
              {{ movie.vote_average }}
            </p>
            <p
              class="
                leading-normal
                absolute
                bottom-0
                bg-fade
                p-3
                transform
                translate-y-full
                transition-all
              "
            >
              {{ movie.overview }}
            </p>
          </div>
          <div class="">
            <p class="text-white">
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
                params: { movieID: movies.id },
              }"
              >Get More Info</NuxtLink
            >
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
        this.movies.push(movie);
      });
    },
  },
};
</script>
