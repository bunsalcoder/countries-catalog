<template>
  <div id="app" class="p-4">
    <h1 class="text-4xl font-bold mb-8 text-center mt-5">Countries Catalog</h1>
    <div class="card-container">
      <div class="flex flex-start">
        <SearchBar @search="searchCountries" @sort="sortCountries" class="mb-4 w-3/4 relative" />
        <Pagination
          :total-items="totalCountries"
          :per-page="perPage"
          :current-page="currentPage"
          @page-changed="changePage"
          class="ml-auto"
        />
      </div>
      <div class="country-grid">
        <CountryCard
          v-for="country in filteredCountries"
          :key="country.cca3"
          :country="country"
          @open-modal="openModal"
        />
      </div>
    </div>
    <CountryModal
      v-if="selectedCountry"
      :country="selectedCountry"
      @close="closeModal"
    />
  </div>
</template>

<script>
import axios from 'axios';
import { ref, computed } from 'vue';
import CountryCard from './components/CountryCard.vue';
import CountryModal from './components/CountryModal.vue';
import SearchBar from './components/SearchBar.vue';
import Pagination from './components/PaginationBar.vue';
import _ from 'lodash';

export default {
  components: {
    CountryCard,
    CountryModal,
    SearchBar,
    Pagination,
  },
  setup() {
    const countries = ref([]);
    const selectedCountry = ref(null);
    const searchQuery = ref('');
    const currentPage = ref(1);
    const perPage = 25;
    const sortDirection = ref('asc');

    const fetchCountries = async () => {
      const response = await axios.get('https://restcountries.com/v3.1/all');
      countries.value = response.data;
    };

    const filteredCountries = computed(() => {
      let filtered = _.filter(countries.value, (country) => {
        return country.name.official
          .toLowerCase()
          .includes(searchQuery.value.toLowerCase());
      });

      filtered = _.orderBy(filtered, ['name.official'], [sortDirection.value]);

      return filtered.slice(
        (currentPage.value - 1) * perPage,
        currentPage.value * perPage
      );
    });

    const totalCountries = computed(() => {
      return _.filter(countries.value, (country) => {
        return country.name.official
          .toLowerCase()
          .includes(searchQuery.value.toLowerCase());
      }).length;
    });

    const searchCountries = (query) => {
      searchQuery.value = query;
      currentPage.value = 1;
    };

    const sortCountries = (direction) => {
      sortDirection.value = direction;
    };

    const changePage = (page) => {
      currentPage.value = page;
    };

    const openModal = (country) => {
      selectedCountry.value = country;
    };

    const closeModal = () => {
      selectedCountry.value = null;
    };

    fetchCountries();

    return {
      countries,
      selectedCountry,
      searchQuery,
      currentPage,
      perPage,
      sortDirection,
      filteredCountries,
      totalCountries,
      searchCountries,
      sortCountries,
      changePage,
      openModal,
      closeModal,
    };
  },
};
</script>

<style scoped>
.card-container {
  @apply mx-auto bg-gray-50 p-4 rounded-lg;
  width: 80%;
}

.country-grid {
  @apply grid grid-cols-1 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-5 gap-4;
}
</style>
