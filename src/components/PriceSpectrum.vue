<template>
  <section class="price-spectrum">
    <BarGroup :dataset="dataset" :min="min" :max="max" />
  </section>
  <div class="price-spectrum__minmax">
    <div class="price-spectrum__min">
      <span class="price-spectrum__min-price">${{ min }}</span>
      <span class="price-spectrum__min-label">Min</span>
    </div>
    <div class="price-spectrum__max">
      <span class="price-spectrum__max-price">${{ max }}</span>
      <span class="price-spectrum__max-label">Max</span>
    </div>
  </div>
</template>

<script setup lang="ts">
import { ref } from 'vue'
import BarGroup from '@/components/BarGroup.vue'

const min = ref(65)
const max = ref(250)

const dataset = ref([
  {
    price: 65,
    bars: [10, 10]
  },
  {
    price: 64,
    bars: [15, 17]
  },
  {
    price: 96,
    bars: [27, 29]
  },
  {
    price: 128,
    bars: [39, 41, 41]
  },
  {
    price: 169,
    bars: [48, 53, 53]
  },
  {
    price: 250,
    bars: [80, 92]
  }
])
</script>

<style scoped>
.price-spectrum {
  min-height: 60px;
  position: relative;
  width: calc(100% - 26px);
  margin: 0 auto;
}

.price-spectrum:after {
  content: '';
  display: block;
  position: absolute;
  bottom: 0;
  left: 0;
  right: 0;
  height: 1px;
  background: var(--gray-100);
}

.price-spectrum__minmax {
  display: flex;
  justify-content: space-between;
  margin-top: 15px;
  padding: 0 25px;
}

.price-spectrum__min,
.price-spectrum__max {
  display: flex;
  flex-direction: column;
  grid-gap: 5px;
  align-items: center;
}

.price-spectrum__min-price,
.price-spectrum__max-price {
  font-weight: 700;
}

.price-spectrum__min-label,
.price-spectrum__max-label {
  color: var(--gray-400);
}
</style>
