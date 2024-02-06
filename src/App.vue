<script setup lang="ts">
import PriceForm from '@/components/PriceForm.vue'
import PriceSpectrum from '@/components/PriceSpectrum.vue'
import { ref, provide } from 'vue'

const price = ref<number>(100)
provide('selectedPrice', price)
</script>

<template>
  <main>
    <section class="price-wrapper">
      <PriceForm v-model:price="price" />
      <section class="price-insight site-border">
        <div class="price-insight__container">
          <span class="price-insight__label">Price insight</span>
          <strong class="price-insight__rate">${{ price || 0 }}</strong>
          <span class="price-insight__rate-label">Hourly Rate</span>
        </div>
        <PriceSpectrum :selectedPrice="price" />
      </section>
    </section>
  </main>
</template>

<style scoped>
.price-wrapper {
  width: 100vw;
  max-width: 480px;
  min-width: 360px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  grid-gap: 6px;
}

.price-insight {
  display: flex;
  flex-direction: column;
  padding: 15px 30px;
}

.price-insight__container {
  display: flex;
  flex-direction: column;
  position: relative;
  z-index: 3;
}

.price-insight__label {
  margin-bottom: 30px;
}

.price-insight__rate {
  font-size: 60px;
}

.price-insight__caption {
  transform: translateY(-10px);
}
</style>
