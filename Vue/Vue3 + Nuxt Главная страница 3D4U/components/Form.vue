<template>
  <form class="form" action="#">
    <div class="form__text">
      <Input
        v-model="validationFields.userName"
        class="form__field"
        :type="'text'"
        :id="'userName'"
        :name="'userName'"
        :placeholder="'Иван Иванов'"
        :label="'Ваше имя*'"
        :error="v$.userName.$error"
        :errorText="'Это поле обязательно'"
      />
      <Input
        v-model="validationFields.userPhone"
        class="form__field"
        :type="'number'"
        :id="'userPhone'"
        :name="'userPhone'"
        :placeholder="'+7 (___) ___-__-__'"
        :label="'Телефон*'"
        :error="v$.userPhone.$error"
        :errorText="'Это поле обязательно'"
      />
      <Input
        class="form__field"
        :type="'text'"
        :id="'userMessage'"
        :name="'userMessage'"
        :label="'Расскажите нам о своем проекте'"
      />
      <Input 
        v-model="validationFields.userCheckbox"
        class="form__agreement"
        :type="'checkbox'"
        :id="'form-checkbox'"
        :name="'form-checkbox'"
        :label="'Я соглашаюсь с Политикой Конфиденциальности сайта'"
        :error="v$.userCheckbox.$error"
        :errorText="'Необходимо поставить галочку'"
      />
    </div>
    <Button
      @click.prevent="submitForm"
      class="form__button"
      :text="'Отправить'"
    />
  </form>
</template>

<script setup>
import { useVuelidate } from '@vuelidate/core';
import { required, sameAs } from '@vuelidate/validators';

const validationFields = reactive({
  userName: '',
  userPhone: '',
  userText: '',
  userCheckbox: false,
});

const validationRules = computed(() => {
  return {
    userName: { required },
    userPhone: { required },
    userCheckbox: { required, sameAs: sameAs(true) },
  };
});

const v$ = useVuelidate(validationRules, validationFields);

const submitForm = async () => {
  await v$.value.$validate();
};

</script>

<style lang="scss">

.form {
  display: flex;
  align-items: start;
  justify-content: space-between;
  gap: 24px;
  z-index: 1;

  &__text {
    display: flex;
    flex-wrap: wrap;
    gap: 16px 24px;
  }

  &__field {
    position: relative;
    max-width: 322px;
    width: 100%;
  }

  &__agreement {
    max-width: 100%;
  }

  &__button {
    border: none;
    cursor: pointer;
    padding: 20.5px 118px;
    max-width: 322px;
    width: 100%;
  }

  &__error {
    @extend %err;
    color: var(--color-error);
    position: absolute;
    margin: 2px 0 0;
  }
}

@media screen and (max-width: 1439px) {
  .form {
    flex-direction: column;

    &__text {
      width: 100%;
    }
  }
}

@media screen and (max-width: 1093px) {
  .form {
    &__text {
      justify-content: space-between;
    }

    &__field {
      max-width: calc(50% - 24px);

      &:nth-child(3) {
        max-width: 100%;
      }
    }
  }
}

@media screen and (max-width: 540px) {
  .form {
    &__button {
      max-width: 100%;
    }

    &__field {
      max-width: 100%;
    }

    &__text {
      margin: 0;
    }
  }
}

</style>
