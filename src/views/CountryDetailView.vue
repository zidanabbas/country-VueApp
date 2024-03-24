<template>
  <div class="max-w-4xl mx-auto p-6">
    <router-link
      class="inline-flex items-center space-x-2 text-blue-600 hover:text-blue-800"
      :to="{ name: 'home' }"
    >
      <svg
        class="h-5 w-5"
        xmlns="http://www.w3.org/2000/svg"
        fill="none"
        viewBox="0 0 24 24"
        stroke="currentColor"
      >
        <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M15 19l-7-7 7-7" />
      </svg>
      <span>Back to Homepage</span>
    </router-link>
    <div class="mt-8 flex flex-col lg:flex-row lg:space-x-8">
      <div class="flex-1">
        <h1 class="text-5xl font-bold">{{ country.name.common }}</h1>
        <div class="mt-4 flex space-x-2">
          <span
            class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-gray-100 text-gray-800"
          >
            {{ country.name.official }}
          </span>
          <span
            class="px-2 inline-flex text-xs leading-5 font-semibold rounded-full bg-gray-100 text-gray-800"
          >
            {{ country.name.native.ind.common }}
          </span>
        </div>
        <div class="mt-6">
          <h2 class="text-lg font-semibold">LatLong</h2>
          <p class="text-2xl font-bold text-blue-600">{{ country.latlng.join(', ') }}</p>
        </div>
        <div class="mt-6">
          <h2 class="text-lg font-semibold">Calling Code</h2>
          <p class="text-2xl font-bold text-blue-600">
            +{{ country.idd.root }} {{ country.idd.suffixes[0] }}
          </p>
          <p class="text-sm text-gray-500">
            {{ country.idd.suffixes.length }} countries with this calling code
          </p>
        </div>
      </div>
      <div class="flex-1 mt-8 lg:mt-0">
        <div class="mt-6">
          <h2 class="text-lg font-semibold">Capital: {{ country.capital[0] }}</h2>
        </div>
        <div class="mt-6">
          <h2 class="text-lg font-semibold">Region: {{ country.region }}</h2>
        </div>
        <div class="mt-6">
          <h2 class="text-lg font-semibold">Subregion: {{ country.subregion }}</h2>
        </div>
        <div class="mt-6">
          <h2 class="text-lg font-semibold">Currency</h2>
          <p class="text-2xl font-bold text-blue-600">{{ Object.keys(country.currencies)[0] }}</p>
          <p class="text-sm text-gray-500">1 country with this currency</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  name: 'CountryDetailView',
  data() {
    return {
      country: null
    }
  },
  created() {
    if (this.$route.params.countryData) {
      this.country = this.$route.params.countryData
    } else {
      this.fetchCountryDetails(this.$route.params.countryName)
    }
  },
  methods: {
    async fetchCountryDetails(countryName) {
      try {
        const response = await fetch(
          `https://restcountries.com/v3.1/name/${countryName}?fullText=true`
        )
        const data = await response.json()
        console.log(data)
        if (data.length > 0) {
          this.country = data[0]
        } else {
          console.error('No country data found for:', countryName)
        }
      } catch (error) {
        console.error('Error fetching country details:', error)
      }
    }
  }
}
</script>
