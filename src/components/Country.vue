<template>
  <div class="flex flex-col items-center justify-center min-h-screen bg-gray-100">
    <h1 class="text-4xl font-bold mb-8">Country</h1>
    <div
      class="flex items-center w-full max-w-md mx-auto bg-white rounded-lg shadow-md overflow-hidden"
    >
      <div class="w-full">
        <input
          class="w-full rounded-l-lg border-0"
          placeholder="Type any country name"
          type="text"
          v-model="searchQuery"
          @input="handleSearch"
        />
      </div>
      <button class="rounded-r-lg" style="border: none; background: none">
        <icon-search class="text-gray-500" />
      </button>
    </div>
    <div
      v-if="showSuggestions"
      class="mt-4 w-full max-w-md mx-auto bg-white rounded-lg shadow-md overflow-hidden"
    >
      <div v-if="loading" class="p-4 text-center">Loading...</div>
      <div v-else-if="searchResults.length === 0" class="p-4 text-center">No results found.</div>
      <ul v-else class="divide-y divide-gray-200">
        <li
          v-for="(country, index) in searchResults.slice(0, 5)"
          :key="index"
          class="px-4 py-2 cursor-pointer"
          @click="goToCountryDetail(country.name.common)"
        >
          {{ country.name.common }}
        </li>
      </ul>
    </div>
  </div>
</template>

<script>
import IconSearch from '@/components/icons/IconSearch.vue'
import { debounce } from 'lodash' // Import fungsi debounce dari lodash
import { useRouter } from 'vue-router'

export default {
  components: {
    IconSearch
  },
  data() {
    return {
      searchQuery: '',
      searchResults: [],
      showSuggestions: false,
      loading: false
    }
  },
  methods: {
    async handleSearch() {
      if (this.searchQuery.length > 2) {
        this.loading = true
        try {
          const response = await fetch(`https://restcountries.com/v3.1/name/${this.searchQuery}`)
          const data = await response.json()
          console.log(data)
          this.searchResults = data
          this.showSuggestions = true
        } catch (error) {
          console.error('Error fetching data:', error)
        }
        this.loading = false
      } else {
        this.showSuggestions = false
        this.searchResults = []
      }
    },
    debouncedSearch: debounce(function () {
      this.handleSearch()
    }, 300),
    goToCountryDetail(countryName) {
      this.$router.push({ name: 'country-detail', params: { countryName } })
    }
  },
  watch: {
    searchQuery() {
      this.debouncedSearch()
    }
  }
}
</script>

<style>
.suggestion-item {
  padding: 8px;
  cursor: pointer;
}
</style>
