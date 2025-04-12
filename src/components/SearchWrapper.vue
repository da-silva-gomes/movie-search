<script>
import SearchInput from './SearchInput.vue';
import SearchResultsWrapper from './SearchResultsWrapper.vue';

export default {
  name: 'SearchWrapper',
  data() {
    return {
      movieList: [],
      searchTerm: '',
      renderList: false
    }
  },
  components: {
    SearchInput,
    SearchResultsWrapper
  },
  methods: {
    setMovieList(list, term) {
      this.movieList = list
      this.searchTerm = term
      this.renderList = true
      this.$emit('list-rendered', this.renderList)
    }
  }
}
</script>

<template>
  <SearchInput v-if="!renderList" @search-results-found='setMovieList' />
  <SearchResultsWrapper v-else :searchTerm="searchTerm" :searchResults="movieList" />
</template>