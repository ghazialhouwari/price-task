<template>
  <div class="price-spectrum__container">
    <div
      v-for="(group, groupIndex) in groups"
      :ke="`group-${groupIndex}`"
      class="price-spectrum__bar-group"
      :style="{ '--left': `calc(${group.position}% - ${(group.bars.length * barWidth) / 2}px)` }"
    >
      <span
        v-for="(bar, barIndex) in group.bars"
        :ke="`bar-${barIndex}`"
        class="price-spectrum__bar"
        :style="{ '--height': `${bar}px` }"
      ></span>
    </div>
    <span
      v-if="cursorPosition !== undefined"
      class="price-spectrum__cursor"
      :style="{ '--cursor-position': `${cursorPosition}%` }"
    ></span>
  </div>
</template>

<script setup lang="ts">
import { ref, computed, inject, type Ref } from 'vue'

interface BarGroup {
  price: number
  bars: number[]
}
interface Props {
  dataset: BarGroup[]
  min: number
  max: number
}

const props = defineProps<Props>()
const barWidth = ref(8)
const selectedPrice = inject<Ref<number | undefined>>('selectedPrice', ref())

const cursorPosition = computed<number | undefined>(() => percentagePosition(selectedPrice.value))

const groups = computed(() =>
  props.dataset.map((group) => {
    let position = percentagePosition(group.price)
    return {
      ...group,
      position
    }
  })
)

function percentagePosition(price: number | undefined): number | undefined {
  if (!price) return undefined
  const position = Math.ceil(((price - props.min) / (props.max - props.min)) * 100)

  if (position < -9) return -9
  if (position > 109) return 109

  return position
}
</script>

<style scoped>
.price-spectrum__container {
  position: absolute;
  height: 100%;
  left: 30px;
  right: 30px;
}

.price-spectrum__bar-group {
  position: absolute;
  bottom: 0;
  left: var(--left);
  display: flex;
  align-items: end;
}

.price-spectrum__bar {
  height: var(--height, 50px);
  width: 8px;
  background: var(--gray-100);
}

.price-spectrum__cursor {
  position: absolute;
  bottom: -12px;
  left: calc(var(--cursor-position) - 2px);
  width: 4px;
  height: calc(24px + calc(var(--cursor-position) * 0.5));
  background: var(--primary-500);
  border-radius: 4px;
  z-index: 2;
  will-change: left, height;
  transition:
    left 150ms linear,
    height 150ms linear;
}
</style>
