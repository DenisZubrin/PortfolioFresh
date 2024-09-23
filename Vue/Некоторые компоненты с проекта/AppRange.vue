<script setup lang="ts">
import { onMounted, ref, watch } from 'vue'

const percent = defineModel<number>({ default: 50 })
const range = ref<HTMLInputElement>()

const updateRangeSlider = () => {
  if (range.value) {
    range.value.style.setProperty('--value', `${percent.value}%`)
  }
}

onMounted((): void => {
  updateRangeSlider()
})

watch(percent, (): void => {
  updateRangeSlider()
})
</script>

<template>
  <label class="range">
    <div class="range__text">
      <span class="range__label">{{ $t('range-rating-seller') }}</span>
      <span class="range__percent">{{ percent }} %</span>
    </div>
    <input
      v-model="percent"
      ref="range"
      class="range__slider"
      max="100"
      min="0"
      type="range"
    />
  </label>
</template>

<style lang="scss">
.range {
  display: block;

  &__text {
    display: flex;
    justify-content: space-between;
    margin-bottom: 16px;
  }

  &__label {
    font-size: 12px;
    font-weight: 500;
    line-height: 1.35;
    color: var(--color-gray-300);
  }

  &__percent {
    font-size: 12px;
    font-weight: 600;
    line-height: 1.1;
    color: var(--color-primary-400);
  }

  &__slider {
    --value: 50%;
    width: 100%;
    -webkit-appearance: none;
    appearance: none;
    cursor: pointer;
    background: linear-gradient(
      to right,
      var(--color-primary-400),
      var(--color-primary-400) var(--value),
      var(--color-gray-700) var(--value),
      var(--color-gray-700)
    );
    border-radius: 100px;
    outline: none;
  }

  // Chrome

  &__slider::-webkit-slider-runnable-track {
    height: 8px;
    -webkit-appearance: none;
    border-radius: 100px;
  }

  &__slider::-webkit-slider-thumb {
    width: 16px;
    height: 16px;
    margin-top: -4px;
    -webkit-appearance: none;
    background-color: var(--color-gray-900);
    border: 2px solid var(--color-primary-400);
    border-radius: 50%;
  }

  // Firefox

  &__slider::-moz-range-track {
    height: 8px;
    -webkit-appearance: none;
    background: var(--color-gray-700);
    border-radius: 100px;
  }

  &__slider::-moz-range-progress {
    background: var(--color-primary-400);
  }

  &__slider::-moz-range-thumb {
    width: 16px;
    height: 16px;
    margin-top: -4px;
    -webkit-appearance: none;
    background: var(--color-gray-900);
    border: 2px solid var(--color-primary-400);
    border-radius: 50%;
  }
}
</style>