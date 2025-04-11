<script>
export default {
  name: 'SearchResultsWrapper',
  data() { return {} },
  components: {},
  props: {
    searchTerm: {
      type: String,
      default: null,
    },
    searchResults: {
      type: Array,
      default: null
    }
  },
  computed: {
    // Removed setMovieDurationFormat from here
  },
  methods: {
    setMovieDurationFormat(runtime) {
      return `${Math.floor(runtime / 60)}h${runtime % 60}m`;
    },
    formatDate(dateString) {
      const options = { year: 'numeric', month: 'long', day: 'numeric' };
      const date = new Date(dateString);
      return date.toLocaleDateString('en-GB', options).replace(',', '');
    },
  }
};
</script>

<template>
  <div class="w-full flex flex-col text-white mt-15">
    <div class="flex justify-between">
      <div class="block text-start">
        <h2 class="font-bold text-xl">Results for '{{ searchTerm }}'</h2>
        <p class="text-white/60">We found 50 results for '{{ searchTerm }}'</p>
      </div>
      <!-- <Sort /> FIX -->
    </div>
    <div class="flex mt-11 flex-wrap justify-between">
      <div class="max-w-60 mb-10 mr-4" v-for="movie in searchResults" :key="movie.title">
        <div class="mb-6">
          <img class="w-full h-90 rounded-xl" :src="`https://image.tmdb.org/t/p/original/${movie.poster_path}`"
            alt="Poster of {{ movie.title }}">
        </div>
        <div>
          <div class="flex flex-col items-start">
            <h3 class="w-full text-lg mb-2 leading-none truncate">{{ movie.title }}</h3>
            <p class="w-full opacity-60 text-[15px] truncate">
              {{ setMovieDurationFormat(movie.runtime) }} |
              {{ movie.genres[0].name }} |
              {{ formatDate(movie.release_date) }}
            </p>
          </div>
          <p class="bg-white/6 flex items-center justify-start rounded-[8px] px-2 py-1.5 mt-4.5 w-fit">
            <span class="text-sm pr-2.5">
              {{ movie.vote_average }}/10
            </span>
            <img src="../assets/star.svg" alt="star(s)" class="w-4 h-4">
          </p>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped />
