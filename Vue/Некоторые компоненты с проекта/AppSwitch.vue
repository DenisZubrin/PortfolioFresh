<script setup lang="ts">
const props = withDefaults(
  defineProps<{
    /** Выключает свич. Не дает быть активным, не переключает состояние*/
    disabled?: boolean;
  }>(),
  {
    disabled: false,
  }
);
const model = defineModel<boolean>();

defineSlots<{
  /** Текст слева от переключателя */
  default?: string;
}>();

</script>

<template>
  <label :class="['app-switch s4', { 'app-switch_disabled': props.disabled }]">
    <slot>Label</slot>
    <div
      :class="[
        'app-switch__toggle',
        {
          'app-switch__toggle_disabled': props.disabled,
          'app-switch__toggle_active': model,
        },
      ]"
    >
      <input
        v-model="model"
        :checked="model"
        :class="[
          'app-switch__checkbox',
          {
            'app-switch__checkbox_disabled': props.disabled,
            'app-switch__checkbox_active': model,
          },
        ]"
        :disabled="props.disabled"
        type="checkbox"
      />
    </div>
  </label>
</template>


<style lang="scss">
.app-switch {
  display: inline-flex;
  flex-wrap: wrap;
  gap: 18px;
  color: var(--color-gray-50);
  cursor: pointer;
  transition: color 0.3s ease;

  &_disabled {
    opacity: 0.6;
  }

  &:hover:not(&_disabled) {
    color: var(--color-primary-600);
  }

  &__toggle {
    display: flex;
    align-items: center;
    width: 36px;
    height: 20px;
    padding: var(--spacing-2xs);
    cursor: pointer;
    background-color: var(--color-gray-400);
    border: 1px solid transparent;
    border-radius: 16px;
    transition: background-color 0.3s ease;
  }

  &__toggle_active {
    background-color: var(--color-primary-400);
  }

  &:hover > &__toggle_active:not(&__toggle_disabled) {
    background-color: var(--color-primary-600);
  }

  &__toggle:not(&__toggle_disabled):focus-within {
    outline: 2px solid var(--color-primary-400);
    outline-offset: 1px;
  }

  &__checkbox {
    width: 16px;
    height: 16px;
    -webkit-appearance: none;
    appearance: none;
    cursor: pointer;
    background-color: var(--color-gray-50);
    border-radius: 50%;
    outline: none;
    transition: 0.3s ease;
  }

  &__checkbox_active {
    transform: translateX(calc(100% - 2px));
  }
}
</style>