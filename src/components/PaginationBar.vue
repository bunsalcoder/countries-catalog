<template>
  <div>
    <button
      v-for="page in totalPages"
      :key="page"
      @click="$emit('page-changed', page)"
      :class="{ active: page === currentPage }"
    >
      {{ page }}
    </button>
  </div>
</template>
  
<script>
export default {
  props: ['total', 'perPage', 'currentPage'],
  computed: {
    totalPages() {
      return Math.ceil(this.total / this.perPage);
    },
  },
};
</script>
  
<style>
  .active {
    font-weight: bold;
  }
</style>