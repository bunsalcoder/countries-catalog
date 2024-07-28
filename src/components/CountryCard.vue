<template>
    <div class="country-card" @mouseenter="showIcon = true" @mouseleave="showIcon = false">
      <img :src="country.flags.png" alt="Flag" class="country-card__flag" />
      <div class="country-card__content">
        <div class="country-card__info">
          <h2 class="country-card__name font-semibold">{{ country.name.official }}</h2>
          <p class="country-card__code text-sm"><strong>cca2: </strong> {{ country.cca2 }}</p>
          <p class="country-card__code text-sm"><strong>cca3: </strong> {{ country.cca3 }}</p>
        </div>
        <div v-if="showIcon" class="country-card__info-icon" @click.stop="openModal">
          <svg class="country-card__icon" xmlns="http://www.w3.org/2000/svg" fill="none" viewBox="0 0 24 24" stroke="currentColor">
            <path stroke-linecap="round" stroke-linejoin="round" stroke-width="2" d="M9 5l7 7-7 7" />
          </svg>
        </div>
      </div>
    </div>
  </template>
  
<script>
export default {
  props: {
    country: {
      type: Object,
      required: true
    }
  },
  data() {
    return {
      showIcon: false
    };
  },
  methods: {
    openModal() {
      this.$emit('open-modal', this.country);
    }
  }
};
</script>
  
  <style scoped>
  .country-card {
    border: 1px solid #ddd;
    border-radius: 8px;
    overflow: hidden;
    box-shadow: 0 6px 12px rgba(0, 0, 0, 0.2);
    background-color: white;
    width: 280px;
    margin: 4px;
    position: relative;
    cursor: pointer;
    transition: transform 0.3s ease, box-shadow 0.3s ease;
  }
  
  .country-card:hover {
    transform: translateY(-10px);
    box-shadow: 0 12px 24px rgba(0, 0, 0, 0.3);
  }
  
  .country-card__flag {
    width: 100%;
    height: 150px;
    object-fit: cover;
    position: relative;
  }
  
  .country-card__content {
    display: flex;
    flex-direction: column;
    padding: 16px;
    box-sizing: border-box;
  }
  
  .country-card__info {
    flex: 1;
    overflow-y: auto;
  }
  
  .country-card__name {
    font-size: 1.25rem;
    margin-bottom: 8px;
  }
  
  .country-card__code {
    margin-bottom: 8px;
  }
  
  .country-card__info-icon {
    position: absolute;
    top: 8px;
    right: 8px;
    background: rgba(0, 0, 0, 0.6);
    color: white;
    padding: 4px;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    opacity: 0;
    transition: opacity 0.3s ease;
    cursor: pointer;
  }
  
  .country-card:hover .country-card__info-icon {
    opacity: 1;
  }
  
  .country-card__icon {
    width: 20px;
    height: 20px;
  }
  </style>
  