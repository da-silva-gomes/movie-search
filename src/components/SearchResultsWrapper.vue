<script>

const IMAGE_URL = 'https://image.tmdb.org/t/p/original/'

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
    }
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
    <div class="flex mt-11">
      <div v-for="movie in searchResults" :key="movie.title">
        <div class="mb-6">
          <!-- <img src=`${IMAGE_URL}` alt=""> -->
        </div>
        <div>
          <div class="flex flex-col items-start">
            <h3 class="text-lg mb-2 leading-none">{{ movie.title }}</h3>
            <p class="opacity-60 text-[15px]">
              {{ setMovieDurationFormat(movie.runtime) }} |
              {{ movie.genres[0].name }} |
              {{ movie.release_date }} |
              {{ movie.runtime }}
            </p>
          </div>
          <div class="bg-white/6 flex justify-center rounded-[8px] max-w-22 px-2 py-1.5 mt-4.5">
            <span class="text-sm pr-2.5">
              8.6/10
            </span>
            <img src="../assets/star.svg" alt="star(s)">
          </div>
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped />
