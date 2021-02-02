<template>
  <div class="home">
    <h1 class="text-3xl md:text-4xl text-white font-bold text-center py-5">
      Search Movie
    </h1>
    <!-- search button -->
    <div class="relative max-w-lg w-full mx-auto">
      <input
        aria-label="Search movie"
        type="text"
        placeholder="Search movie"
        v-model="searchMovie"
        @keyup.enter="getMovies"
        class="block w-full px-4 py-2 border rounded-md border-gray-900 bg-gray-800 text-gray-100"
      />
      <svg
        class="absolute w-5 h-5 text-gray-400 right-3 top-3 dark:text-gray-300"
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
      >
        <path
          strokeLinecap="round"
          strokeLinejoin="round"
          strokeWidth="{2}"
          d="M21 21l-6-6m2-5a7 7 0 11-14 0 7 7 0 0114 0z"
        />
      </svg>
    </div>
    <!-- end of search button -->
    <!-- Section Movies -->
    <section class="flex justify-center items-center w-full flex-wrap py-5">
      <!-- fallback movie -->
      <!-- Card Movie -->
      <div
        class="w-full md:w-1/4 bg-gray-800 rounded shadow p-1 mx-3 my-5"
        v-for="movie in movies"
        :key="movie.imdbID"
      >
        <div>
          <img
            :src="movie.Poster"
            :alt="movie.Title"
            class="w-3/5 mx-auto pt-2"
          />
        </div>
        <div class="my-3 px-3">
          <h2 class="text-2xl md:text-xl text-white font-bold text-center mb-2">
            {{ movie.Title }}
          </h2>
          <p class="text-lg md:text-base text-white font-medium">
            type : {{ movie.Type }}
          </p>
          <p class="text-lg md:text-base text-white">year : {{ movie.Year }}</p>
          <router-link :to="/movie/ + movie.imdbID">
            <button
              class="bg-gray-900 p-2 text-white w-full mt-2 rounded hover:bg-gray-700"
            >
              Movie Detail
            </button>
          </router-link>
        </div>
      </div>
      <!-- end of Card Movie -->
    </section>
    <!-- end of Section Movies -->
  </div>
</template>

<script>
export default {
  name: 'Home',
  data: () => ({
    searchMovie: '',
    movies: [],
  }),
  methods: {
    getMovies(){
      fetch(`http://www.omdbapi.com/?apikey=${process.env.VUE_APP_API_KEY}&s=${this.searchMovie}`)
          .then(response => response.json())
          .then(data => {
           this.movies = data.Search
          });
    }
  },
}
</script>
