<template>
  <div>
    <button @click="sort('asc')">Sort Asc</button>
    <button @click="sort('desc')">Sort Desc</button>
    <table>
        <thead>
            <tr>
            <th>Flag</th>
            <th>Country Name</th>
            <th>2-char Code</th>
            <th>3-char Code</th>
            <th>Native Name</th>
            <th>Alternative Names</th>
            <th>Calling Codes</th>
            </tr>
        </thead>
        <tbody>
            <tr v-for="country in countries" :key="country.cca3" @click="countryClicked(country)">
            <td><img :src="country.flags.png" alt="Flag" width="50"></td>
            <td>{{ country.name.official }}</td>
            <td>{{ country.cca2 }}</td>
            <td>{{ country.cca3 }}</td>
            <td>{{ country.name.nativeName ? Object.values(country.name.nativeName)[0].common : '' }}</td>
            <td>{{ country.altSpellings.join(', ') }}</td>
            <td>{{ country.idd.root }}{{ country.idd.suffixes ? country.idd.suffixes.join(', ') : '' }}</td>
            </tr>
        </tbody>
    </table>
  </div>
</template>
  
<script>
export default {
  props: ['countries'],
  methods: {
    countryClicked(country) {
      this.$emit('country-click', country);
    },
    sort(direction) {
      this.$emit('sort', direction);
    },
  },
};
</script>