<template>
  <div class="input">
    <input
      v-model="model"
      v-if="type === 'checkbox'"
      class="input__checkbox"
      :type="type"
      :id="id"
      :name="name"
    />
    <label
      v-if="label"
      :class="{
        'input__label': type === 'text' || type === 'number',
        'input__label_focused': model,
        'input__checkbox-label': type === 'checkbox',
      }"
      :for="id"
    >
      {{ label }}
    </label>
    <input
      v-model="model"
      v-if="type === 'text' || type === 'number'"
      :class="[
        'input__field', {
          'input__field_focused': model
        }
      ]"
      :type="type"
      :id="id"
      :name="name"
      :placeholder="placeholder"
    />
    <div v-if="error" class="input__error">
      {{ errorText }}
    </div>
  </div>
</template>

<script setup>
defineProps({
  type: {
    type: String,
    required: true,
  },
  id: {
    type: [String, Number],
    required: true,
  },
  label: {
    type: String,
  },
  placeholder: String,
  error: [String, Number],
  errorText: {
    type: String,
    default: 'Проверьте правильность данных',
  },
});

const model = defineModel();
</script>

<style lang="scss">
.input {
  position: relative;
  max-width: 322px;
  width: 100%;

  // type="text"

  &__label {
    @extend %p5;
    color: var(--color-text-elements);
    position: absolute;
    top: 30px;
    transition: 0.3s cubic-bezier(0.4, 0, 0.2, 1);

    &_focused {
      top: 0;
      color: var(--color-secondary);
    }
  }

  &__field {
    width: 100%;
    background: inherit;
    outline: none;
    @extend %s4;
    color: var(--color-text);
    border: none;
    border-bottom: 1px solid var(--color-text);
    transition: 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    padding: 30px 0 12px;
    box-sizing: border-box;

    &::placeholder {
      opacity: 0;
      @extend %s4; 
      color: var(--color-text-elements);
      transition: 0.3s;
    }

    &_focused {
      border-color: var(--color-secondary);
    }
  }

  &__field:focus {
    border-bottom: 1px solid var(--color-secondary);

    &::placeholder {
      opacity: 1;
    }
  }

  &:focus-within &__label {
    top: 0;
    color: var(--color-secondary);
  }

  &__error {
    @extend %err;
    color: var(--color-error);
    position: absolute;
    margin: 2px 0 0;
  }

  // type="number"

  &__field[type='number']::-webkit-outer-spin-button,
  &__field[type='number']::-webkit-inner-spin-button {
    -webkit-appearance: none;
  }

  &__field[type='number'],
  &__field[type='number']:hover,
  &__field[type='number']:focus {
    appearance: none;
    -moz-appearance: textfield;
  }

  // type="checkbox"

  &__checkbox {
    display: none;
  }

  &__checkbox-label {
    display: inline-flex;
    flex-wrap: wrap;
    align-items: center;
    justify-content: start;
    @extend %p3;
    color: var(--color-text-elements);
    cursor: pointer;

    &::before {
      content: '';
      display: block;
      margin: 0 12px 0 0;
      width: 18px;
      height: 18px;
      border: 1px solid var(--color-text);
      border-radius: 2px;
      box-sizing: border-box;
      transition-duration: 0.3s;
      cursor: pointer;
    }
  }

  &__checkbox:checked ~ &__checkbox-label::before {
    background-image: url('~/assets/img/icons/Check.svg');
    background-color: var(--color-secondary);
    border-color: var(--color-secondary);
  }

  &__field_focused {
    border-bottom: 1px solid var(--color-secondary);

    &::placeholder {
      opacity: 1;
    }
  }

  &__label_focused {
    top: 0;
    color: var(--color-secondary);
  }
  
}

@media screen and (max-width: 540px) {
  .input {
    // type="text"

    &__label,
    &:focus-within &__label {
      top: 0;
      color: var(--color-text);
    }

    &__field:focus {
      border-bottom: 1px solid var(--color-text);
    }

    &__field::placeholder {
      opacity: 1;
    }

    // type="checkbox"

    &__checkbox:checked ~ &__checkbox-label::before {
      background-image: url('~/assets/img/icons/Check_alternative.svg');
      background-position: -1px -1px;
      background-color: var(--color-text);
      color: transparent;
      border-color: var(--color-text);
    }

    &__checkbox-label {
      display: inline-block;

      &::before {
        float: left;
      }
    }

    &__field_focused {
      border-bottom: 1px solid var(--color-text);
    }

    &__label_focused {
      color: var(--color-text);
    }
  }
}
</style>
