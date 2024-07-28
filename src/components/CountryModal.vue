<template>
  <div class="modal" :class="{ 'modal-closed': isClosing }" @click="handleClose">
    <div class="modal-content" @click.stop>
      <span class="close" @click="handleClose">&times;</span>
      <div class="modal-body">
        <div>
          <img :src="country.flags.png" alt="Flag" class="modal-flag">
          <div class="mt-5">
            <p><strong class="text-md">2-char Code:</strong> {{ country.cca2 }}</p>
            <p><strong class="text-md">3-char Code:</strong> {{ country.cca3 }}</p>
          </div>
        </div>
        <div class="modal-details">
          <h2 class="mb-4"><strong class="text-2xl">{{ country.name.official }}</strong></h2>
          <p><strong>Native Name:</strong> {{ country.name.nativeName ? Object.values(country.name.nativeName)[0].common : '' }}</p>
          <p><strong>Alternative Names:</strong> {{ country.altSpellings.join(', ') }}</p>
          <p><strong>Calling Codes:</strong> {{ country.idd.root }}{{ country.idd.suffixes ? country.idd.suffixes.join(', ') : '' }}</p>
        </div>
      </div>
    </div>
  </div>
</template>

<script>
export default {
  props: ['country'],
  data() {
    return {
      isClosing: false
    };
  },
  methods: {
    handleClose() {
      this.isClosing = true;
      setTimeout(() => {
        this.$emit('close');
      }, 500);
    }
  }
};
</script>

<style scoped>
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
  z-index: 1000;
  opacity: 0;
  animation: fadeIn 0.5s forwards, floatIn 0.5s forwards;
}

.modal-closed {
  opacity: 0;
  animation: fadeOut 0.5s forwards, floatOut 0.5s forwards;
}

.modal-content {
  background: white;
  padding: 20px;
  border-radius: 5px;
  width: 80%;
  max-width: 500px;
  display: flex;
  position: relative;
  box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);
  overflow: auto;
  transform: translateY(-50px);
  animation: floatIn 0.5s forwards;
}

.close {
  position: absolute;
  top: 10px;
  right: 10px;
  font-size: 24px;
  cursor: pointer;
}

.modal-body {
  display: flex;
  justify-content: space-around;
  flex-wrap: wrap;
}

.modal-flag {
  width: 150px;
  height: 100px;
  margin-right: 20px;
}

.modal-details {
  flex: 1;
  display: flex;
  flex-direction: column;
}

@media (max-width: 768px) {
  .modal-content {
    width: 90%;
  }

  .modal-body {
    flex-direction: column;
    align-items: center;
  }

  .modal-flag {
    margin: 0 0 20px 0;
    width: 100px;
  }
}

@keyframes fadeIn {
  from {
    opacity: 0;
  }
  to {
    opacity: 1;
  }
}

@keyframes floatIn {
  from {
    transform: translateY(-50px);
  }
  to {
    transform: translateY(0);
  }
}

@keyframes fadeOut {
  from {
    opacity: 1;
  }
  to {
    opacity: 0;
  }
}

@keyframes floatOut {
  from {
    transform: translateY(0);
  }
  to {
    transform: translateY(-50px);
  }
}
</style>
