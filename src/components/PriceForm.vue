<template>
  <form class="price-form" @submit.prevent>
    <label for="service_price" class="text-gray-500">Service Price</label>
    <input
      type="number"
      id="service_price"
      placeholder="Enter a price"
      class="price-form__input site-border"
      v-model.number="price"
      @keydown="onKeydown"
    />
  </form>
</template>

<script setup lang="ts">
const price = defineModel('price', { type: Number })

// Filter exponent and minus from the number
function onKeydown(evt: KeyboardEvent) {
  if (evt.key === 'e' || evt.key === '-') {
    evt.preventDefault()
  }
}
</script>

<style scoped>
.price-form {
  display: flex;
  flex-direction: column;
  grid-gap: 6px;
}

.price-form__input {
  height: 56px;
  font-size: 18px;
  padding: 15px;
}

/* For Chrome, Safari, Edge, Opera */
.price-form__input::-webkit-outer-spin-button,
.price-form__input::-webkit-inner-spin-button {
  -webkit-appearance: none;
  margin: 0;
}

/* For Firefox */
.price-form__input[type='number'] {
  -moz-appearance: textfield;
}
</style>
