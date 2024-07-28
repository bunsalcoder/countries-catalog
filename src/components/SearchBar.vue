<template>
  <input
    type="text"
    placeholder="Search by country name"
    v-model="query"
    @input="updateSearch"
  />
</template>
  
<script>
export default {
  data() {
    return {
      query: '',
    };
  },
  methods: {
    updateSearch() {
      this.$emit('search', this.query);
    },
  },
};
</script>