<template>
    <div class="modal">
      <div class="modal-content">
        <span class="close" @click="$emit('close')">&times;</span>
        <h2>{{ country.name.official }}</h2>
        <img :src="country.flags.png" alt="Flag" width="100">
        <p><strong>2-char Code:</strong> {{ country.cca2 }}</p>
        <p><strong>3-char Code:</strong> {{ country.cca3 }}</p>
        <p><strong>Native Name:</strong> {{ country.name.nativeName ? Object.values(country.name.nativeName)[0].common : '' }}</p>
        <p><strong>Alternative Names:</strong> {{ country.altSpellings.join(', ') }}</p>
        <p><strong>Calling Codes:</strong> {{ country.idd.root }}{{ country.idd.suffixes ? country.idd.suffixes.join(', ') : '' }}</p>
        <!-- Add any other fields you want to display here -->
      </div>
    </div>
</template>
  
<script>
export default {
  props: ['country'],
};
</script>
  
<style>
  .modal {
    display: flex;
    justify-content: center;
    align-items: center;
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
  }
  
  .modal-content {
    background: white;
    padding: 20px;
    border-radius: 5px;
    width: 80%;
    max-width: 600px;
  }
  
  .close {
    float: right;
    cursor: pointer;
  }
</style>