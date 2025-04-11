<script>
import SearchBackground from './SearchBackground.vue';
import SearchIcon from './icons/SearchIcon.vue';
import axios from 'axios';

const MOVIE_API_URL = `https://api.themoviedb.org/3/search/movie?`;

export default {
  name: 'SearchInput',
  data() {
    return {
      searchTerm: '',
      searchResults: [],
    }
  },
  components: {
    SearchBackground,
    SearchIcon
  },
  props: {},
  methods: {
    async getMovieList() {
      console.log(this.searchTerm)

      const options = {
        method: 'GET',
        url: MOVIE_API_URL,
        params: { query: this.searchTerm, include_adult: 'false', language: 'en-US', page: '1' },
        headers: {
          accept: 'application/json',
          Authorization: 'Bearer eyJhbGciOiJIUzI1NiJ9.eyJhdWQiOiI5MzlhMjZiY2NiZTJiZjk2MzY3MDQ0NmYzMjhiYTc4YiIsIm5iZiI6MTc0NDE1ODI3NC42NTYsInN1YiI6IjY3ZjViZTQyNzAxYjc1YmZlOWFkMTVkNCIsInNjb3BlcyI6WyJhcGlfcmVhZCJdLCJ2ZXJzaW9uIjoxfQ.0zPLE3VBdY4YjO11QugJhyLEVqm4Qn5NyJaoc6voEBg'
        }
      };

      try {
        const response = await axios.request(options)
        this.searchResults = response.data
        this.$emit('search-results-found', this.searchResults, this.searchTerm);
        console.log(this.searchResults)
      } catch (error) {
        console.error('Error popular movies:', error);
      }
    },
  },
};
</script>

<template>
  <SearchBackground class="mb-12.5 mt-50" />
  <p class="text-white text-center font-bold text-xl mb-5">Search by movie name:</p>
  <div
    class="relative flex items-center w-full max-w-sm border border-(--color-border) focus-within:border-white rounded-xl h-10">
    <form @submit.prevent="getMovieList" class="w-full h-full pl-9 flex items-center">
      <input class="w-full mr-2 text-white outline-none" ref="input" type="text" v-model="searchTerm">
    </form>
    <!-- <Input id="search" type="text" class="pl-10" v-model="inputValue" /> -->
    <span class="absolute start-0 inset-y-0 flex items-center justify-center px-2">
      <SearchIcon class="size-5 text-foreground" />
    </span>
  </div>
</template>