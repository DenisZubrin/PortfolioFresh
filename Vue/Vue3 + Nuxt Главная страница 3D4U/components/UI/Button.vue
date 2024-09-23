<template>
  <button
    :class="[
      'button',
      {
        'button_outline': outline,
      },
    ]"
  >
    <span class="button__text">{{ text }}</span>
    <slot name="icon"></slot>
  </button>
</template>

<script setup>
  defineProps({
    text: {
      type: String,
      required: true,
    },
    outline: Boolean,
  });
</script>

<style lang="scss">
  .button {
    border: none;
    border-radius: 8px;
    min-height: 53px;
    box-sizing: border-box;
    background-color: var(--color-text);
    display: flex;
    justify-content: center;
    align-items: center;
    padding: 20px 42px;
    color: var(--color-filler);
    position: relative;
    cursor: pointer;

    &__text {
      display: block;
      @extend %button_l;
    }

    &__icon-wrap {
      position: absolute;
      top: calc(50% - 11px);
      right: 8px;
    }

    &-icon {
      fill: var(--color-filler);
    }

    &:hover &__icon-wrap &__icon {
      fill: var(--color-text);
    }

    &:hover,
    &:active {
      background-color: var(--color-secondary);
      color: var(--color-text);
      border-color: var(--color-secondary);
    }

    &_outline {
      background-color: transparent;
      color: var(--color-text);
      border: 1px solid var(--color-text);
    }
  }
</style>
