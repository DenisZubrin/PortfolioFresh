<script setup lang="ts">
import IconTick from "@/assets/icons/tick.svg?component";

const props = withDefaults(
  defineProps<{
    /** Отключает возможность переключения checkbox. Значение остается равным modelValue */
    disabled?: boolean;
  }>(),
  {
    disabled: false,
  }
);

const model = defineModel<boolean>();
defineSlots<{
  /** Название чекбокса */
  label?: string;
  /** Описание чекбокса */
  description?: string;
}>();
</script>

<template>
  <label
    :class="[
      'app-checkbox',
      {
        'app-checkbox_disabled': props.disabled,
      },
    ]"
  >
    <div class="app-checkbox__field">
      <input
        v-model="model"
        :checked="model"
        :disabled="props.disabled"
        class="app-checkbox__input"
        type="checkbox"
      />
      <IconTick
        :class="[
          'app-checkbox__icon',
          {
            'app-checkbox__icon_checked': model,
          },
        ]"
      />
    </div>
    <div class="app-checkbox__text s4">
      <span class="app-checkbox__label">
        <slot name="label">Label</slot>
      </span>
      <p class="app-checkbox__description">
        <slot name="description">Description</slot>
      </p>
    </div>
  </label>
</template>

<style lang="scss">
.app-checkbox {
  display: inline-flex;
  flex-wrap: wrap;
  padding: var(--spacing-2xs);
  cursor: pointer;

  &_disabled {
    opacity: 0.6;
  }

  &:hover:not(&_disabled) {
    color: var(--color-primary-600);
  }

  &__field {
    position: relative;
    width: 16px;
    height: 16px;
    padding: var(--spacing-2xs);
    margin: 2px 0 0 0;
    cursor: pointer;
    background-color: var(--color-gray-800);
    border: 1px solid var(--color-gray-300);
    border-radius: 4px;
  }

  &__field:has(&__icon_checked) {
    background-color: var(--color-primary-400);
    border-color: var(--color-primary-400);
  }

  &__field:focus-within {
    outline: 2px solid var(--color-primary-400);
    outline-offset: 1px;
  }

  &_disabled &__field:focus-within {
    outline: none;
  }

  &:hover:not(&_disabled) > &__field {
    background-color: var(--color-primary-600);
    border-color: var(--color-primary-400);
  }

  &__input {
    cursor: pointer;
    opacity: 0;
  }

  &__icon {
    position: absolute;
    top: 3px;
    left: 2px;
    color: transparent;
    content: "";
  }

  &__icon_checked {
    color: var(--color-gray-50);
  }

  &__text {
    display: flex;
    flex-direction: column;
    gap: 4px;
    margin: 0 0 0 12px;
  }

  &__label {
    color: var(--color-gray-50);
  }

  &:hover:not(&_disabled) &__label {
    color: var(--color-primary-600);
  }

  &__description {
    color: var(--color-gray-400);
  }
}
</style>
