<template>
  <div>
    <Hero />

    <div class="flex py-8 px-4">
      <input
        @keyup.enter="$fetch"
        class="
          max-w-[350px]
          w-full
          py-3
          px-2
          text-sm
          focus:ring-touch
          outline-2
          focus:outline-dashed
          outline-touch
          mr-2
        "
        type="text"
        placeholder="search movies"
        v-model="searchInput"
      />
      <button
        @click="searchInput == ''"
        class="btn text-white"
        v-show="searchInput !== ''"
      >
        clear search
      </button>
    </div>

    <!-- Movies -->
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
          <div class="relative overflow-hidden text-white group">
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
                bg-touch
                p-3
                transform
                translate-y-full
                transition-all
                ease-in-out
                group-hover:opacity-100 group-hover:translate-y-0
              "
            >
              {{ movie.overview }}
            </p>
          </div>
          <div class="mt-auto">
            <p class="text-white mt-2 text-sm">
              {{ movie.title.slice(0, 25) }}
              <span v-if="movie.title.length > 25">...</span>
            </p>
            <p class="my-2 text-white">
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
      searchMovies: [],
      searchInput: "",
    };
  },

  async fetch() {
    this.searchInput !== ""
      ? await this.searchedMovies()
      : await this.getMovies();
    return;
  },
  methods: {
    async getMovies() {
      const data = axios.get(
        "https://api.themoviedb.org/3/movie/now_playing?api_key=c3e3b715db7ed78cea000e0969eda5d5&language=en-US&page=1"
      );
      const result = await data;
      result.data.results.forEach((movie) => {
        this.movies.push(movie);
      });
    },
    async searchedMovies() {
      const data = axios.get(
        `https://api.themoviedb.org/3/search/movie?api_key=c3e3b715db7ed78cea000e0969eda5d5&language=en-US&page=1&query=${this.searchInput}`
      );
      const result = await data;
      result.data.results.forEach((movie) => {
        this.searchMovies.push(movie);
        return;
      });
    },
    watch: {
      searchInput() {
        console.log(this.searchInput);
      },
    },
  },
};
</script>
