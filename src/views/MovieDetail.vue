<template>
  <div class="w-full">
    <div class="p-10 flex flex-col items-center">
      <h2 class="text-white text-2xl font-bold">{{ movie.Title }}</h2>
      <p class="text-white text-base">{{ movie.Year }}</p>
      <img
        :src="movie.Poster"
        loading="lazy"
        alt="Movie Poster"
        class="block max-w-lg mb-6"
      />
      <p class="text-white text-base">{{ movie.Plot }}</p>
    </div>
  </div>
</template>

<script>
export default {
    name: 'MovieDetail',
    data: () => ({
       movie : {}
    }),
    methods : {
      getMovieDetail() {
         fetch(`http://www.omdbapi.com/?apikey=${process.env.VUE_APP_API_KEY}&i=${this.$route.params.id}&plot=full`)
         .then(response => response.json())
         .then(data => {
           this.movie = data;
         });
        // console.log(this.$route.params);
      }
    },
    mounted(){
      this.getMovieDetail()
    }
}
</script>

<style>
</style>