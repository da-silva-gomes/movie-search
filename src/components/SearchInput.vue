<script>
import SearchBackground from './SearchBackground.vue';
import SearchIcon from './icons/SearchIcon.vue';
import axios from 'axios';

const API_KEY = import.meta.env.VITE_TMDB_API_KEY
const MOVIE_API_URL = `https://api.themoviedb.org/3/search/movie?`;
const DETAIL_API_URL = `https://api.themoviedb.org/3/movie/`;

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
      const options = {
        method: 'GET',
        url: MOVIE_API_URL,
        params: { query: this.searchTerm, include_adult: 'false', language: 'en-US', page: '1' },
        headers: {
          accept: 'application/json',
          Authorization: API_KEY
        }
      };
      let initialList = []

      try {
        const response = await axios.request(options)
        initialList = response.data;
      } catch (error) {
        console.error('Error popular movies:', error);
      }

      if (initialList && initialList.results) {
        for (const movie of initialList.results) {
          const movieDetails = await this.getMovieDetails(movie.id)
          if (movieDetails) {
            this.searchResults.push(movieDetails);
          }
        }

        this.$emit('search-results-found', this.searchResults, this.searchTerm)
      }
    },
    async getMovieDetails(id) {
      const options = {
        method: 'GET',
        url: `${DETAIL_API_URL}${id}`,
        params: { language: 'en-US' },
        headers: {
          accept: 'application/json',
          Authorization: API_KEY
        }
      };

      let details = {}

      try {
        const response = await axios.request(options)
        details = response.data
      } catch (error) {
        console.error('Error popular movies:', error);
      }

      return details
    }
  },
};
</script>

<template>
  <SearchBackground class="mb-12.5 mt-50" />
  {{ API_KEY }}
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