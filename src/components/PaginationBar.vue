<template>
  <div class="flex">
    <div  v-if="currentPage > 1" @click="$emit('page-changed', currentPage - 1)">
      <button type="button" class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 me-2 mb-2 dark:bg-blue-600">
        Previous
      </button>
    </div>

    <div v-if="currentPage < totalPages" @click="$emit('page-changed', currentPage + 1)">
      <button type="button" class="text-white bg-blue-700 hover:bg-blue-800 focus:ring-4 focus:ring-blue-300 font-medium rounded-lg text-sm px-5 py-2.5 me-2 mb-2 dark:bg-blue-600">
        Next
      </button>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    totalItems: {
      type: Number,
      required: true
    },
    perPage: {
      type: Number,
      required: true
    },
    currentPage: {
      type: Number,
      required: true
    }
  },
  computed: {
    totalPages() {
      return Math.ceil(this.totalItems / this.perPage);
    },
    startItem() {
      return (this.currentPage - 1) * this.perPage + 1;
    },
    endItem() {
      return Math.min(this.currentPage * this.perPage, this.totalItems);
    },
    pagesToShow() {
      const total = this.totalPages;
      const current = this.currentPage;
      const maxPages = 5;
      let pages = [];

      if (total <= maxPages) {
        pages = Array.from({ length: total }, (_, i) => i + 1);
      } else {
        const half = Math.floor(maxPages / 2);
        if (current <= half) {
          pages = Array.from({ length: maxPages }, (_, i) => i + 1);
        } else if (current >= total - half) {
          pages = Array.from({ length: maxPages }, (_, i) => total - maxPages + i + 1);
        } else {
          pages = Array.from({ length: maxPages - 2 }, (_, i) => current - half + i + 1);
          pages = [1, ...pages, total];
        }
      }

      return pages;
    }
  }
};
</script>

<style>
.active {
  font-weight: bold;
}

.arrow-left-icon,
.arrow-right-icon {
  width: 24px;
  height: 24px;
}

</style>
