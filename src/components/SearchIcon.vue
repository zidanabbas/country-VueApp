<template>
  <form
    class="flex items-center w-full max-w-md mx-auto bg-white rounded-lg shadow-md overflow-hidden"
    @submit.prevent="submitSearch"
  >
    <input
      type="search"
      class="w-full rounded-l-lg border-0"
      placeholder="Search..."
      v-model="searchQuery"
    />
    <button type="submit" class="rounded-r-lg">Search</button>
  </form>
</template>
