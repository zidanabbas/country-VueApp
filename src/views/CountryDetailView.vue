<template>
  <div v-if="country" class="max-w-4xl mx-auto p-6">
    <router-link
      class="inline-flex items-center space-x-2 text-blue-600 hover:text-blue-800"
      :to="{ name: 'home' }"
    >
      <span>Back to Homepage</span>
    </router-link>
    <div class="mt-8 flex flex-col lg:flex-row lg:space-x-8">
      <div class="flex-1">
        <h1 class="text-5xl font-bold">{{ country.name.common }}</h1>
        <div class="mt-4 flex space-x-2">
          <badge variant="secondary">{{ country.name.official }}</badge>
          <badge variant="default">{{ country.name.native.ind.common }}</badge>
        </div>
        <div class="mt-6">
          <h2 class="text-lg font-semibold">LatLong</h2>
          <p class="text-2xl font-bold text-blue-600">{{ country.latlng.join(', ') }}</p>
        </div>
        <div class="mt-6">
          <h2 class="text-lg font-semibold">Calling Code</h2>
          <p class="text-2xl font-bold text-blue-600">{{ country.idd.suffixes[0] }}</p>
          <p class="text-sm text-gray-500">
            {{ country.idd.suffixes.length }} countries with this calling code
          </p>
        </div>
      </div>
      <div class="flex-1 mt-8 lg:mt-0">
        <card class="w-full">
          <card-content>
            <div class="space-y-4">
              <div>
                <h2 class="text-lg font-semibold">Capital: {{ country.capital[0] }}</h2>
              </div>
              <div>
                <h2 class="text-lg font-semibold">Region: {{ country.region }}</h2>
              </div>
              <div>
                <h2 class="text-lg font-semibold">Subregion: {{ country.subregion }}</h2>
              </div>
            </div>
          </card-content>
        </card>
        <div class="mt-6">
          <h2 class="text-lg font-semibold">Currency</h2>
          <p class="text-2xl font-bold text-blue-600">{{ country.currencies.IDR.symbol }}</p>
          <p class="text-sm text-gray-500">
            {{ Object.keys(country.currencies).length }} countries with this currency
          </p>
        </div>
      </div>
    </div>
  </div>
  <div v-else class="max-w-4xl mx-auto p-6">Loading...</div>
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
    // Memeriksa apakah ada data negara yang diteruskan melalui properti $route
    if (this.$route.params.countryData) {
      this.country = this.$route.params.countryData
    } else {
      // Jika tidak ada, lakukan permintaan ke API dengan menggunakan countryName dari route params
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
