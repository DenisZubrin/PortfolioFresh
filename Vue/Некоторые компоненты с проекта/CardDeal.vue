<script setup lang="ts">
import { computed, ref } from 'vue'
import { useI18n } from 'vue-i18n'
import AppSwitch from './AppSwitch.vue'
import AppButton from './AppButton.vue'
import IconBank from '@/assets/icons/bank.svg?component'
import IconPlus from '@/assets/icons/plus.svg?component'
import IconStar from '@/assets/icons/star.svg?component'
import IconOpenCard from '@/assets/icons/open-card.svg?component'
import IconPencil from '@/assets/icons/pencil.svg?component'
import IconCross from '@/assets/icons/cross.svg?component'
import IconBitcoin from '@/assets/icons/bitcoin.svg?component'

const props = withDefaults(
  defineProps<{
    /** Формат отображения карточки*/
    type?: 'default' | 'edit'
    /** Идентификатор карточки. Нужен для удаления */
    id: string | number
    /** Ссылка на объявление */
    link?: string
    /** Имя владельца карточки */
    name?: string
    /** Рейтинг владельца карточки */
    rating?: number
    /** Количество совершенных сделок владельца карточки */
    deals?: number
    /** Минимальное значение цены */
    lowrange?: number
    /** Максимальное значение цены */
    highrange?: number
    /** Итоговая стоимость сделки  */
    price?: number
    /** Валюта сделки */
    currency?: string
    /** Криптовалюта сделки */
    coin?: string
    /** Параметр для переключателя. Включает или выключает отображение карточки */
    switch?: boolean
  }>(),
  {
    id: Math.random(),
    type: 'default',
    name: 'marionette10',
    rating: 100,
    deals: 1585,
    lowrange: 300,
    highrange: 30000,
    price: 6120671,
    currency: 'RUB',
    coin: 'bitcoin',
  }
)
// Статус отображения карточки

const emit = defineEmits<{
  (e: 'showCard', showCard: boolean): void
  (e: 'removeCard', cardId: string | number): void
}>()

const switchToggler = ref<boolean>(props.switch)
const toggleDisplayCard = (event: MouseEvent): void => {
  emit('showCard', switchToggler.value)
}

// Удаление карточки

const removeCard = (event: MouseEvent): void => {
  emit('removeCard', props.id)
}

// Разделитель для чисел

const numberSeparator = /\B(?=(\d{3})+(?!\d))/g

const formattedLowrange = ref<string>(props.lowrange.toString().replace(numberSeparator, ' '))
const formattedHighrange = ref<string>(props.highrange.toString().replace(numberSeparator, ' '))
const formattedPrice = ref<string>(props.price.toString().replace(numberSeparator, ' '))

// Количество звезд на основе рейтинга пользователя

const starsRating = computed((): number => Math.round(props.rating / 20))

const { t } = useI18n()
const copyLinkToClipboard = (): void => {
  if (navigator.clipboard && props.link) {
    navigator.clipboard.writeText(props.link)
  } else {
    throw new Error(t('copy-text-error'))
  }
}
</script>

<template>
  <div class="card">
    <!-- Подробности сделки -->
    <div :class="['card__description', { card__description_edit: props.type === 'edit' }]">
      <!-- Опции карточки -->
      <div class="card__actions">
        <template v-if="props.type === 'default'">
          <button
            class="card__actions-btn"
            type="button"
            @click="copyLinkToClipboard"
          >
            <IconOpenCard class="card__actions-icon" />
          </button>
        </template>
        <template v-else>
          <RouterLink
            class="card__actions-btn"
            to="/editPage"
          >
            <IconPencil class="card__actions-icon" />
          </RouterLink>
          <button
            class="card__actions-btn"
            type="button"
            @click="removeCard"
          >
            <IconCross class="card__actions-icon" />
          </button>
        </template>
      </div>
      <!-- Параметры выкладываемого объявления -->
      <div
        v-if="props.type === 'edit'"
        class="card__settings"
      >
        <AppSwitch
          v-model="switchToggler"
          :label="$t('status')"
          @click="toggleDisplayCard"
        />
      </div>
      <!-- Информация о владельце карточки -->
      <div
        v-if="props.type === 'default'"
        class="card__seller"
      >
        <img
          alt="seller image"
          class="card__seller-img"
          src="@/assets/img/seller.png"
        />
        <div class="card__seller-info">
          <RouterLink
            class="card__seller-name s4"
            to="/userProfile"
            >{{ props.name }}</RouterLink
          >
          <div class="card__seller-rating">
            <div class="card__seller-stars">
              <IconStar
                v-for="star in 5"
                :key="star"
                :class="['card__seller-star', { 'card__seller-star_filled': star <= starsRating }]"
              />
            </div>
            <span class="card__seller-percent s6">{{ props.rating }} %</span>
          </div>
          <span class="card__seller-deals s6">{{ props.deals }} {{ $t('deals') }}</span>
        </div>
      </div>
      <!-- Выбор способа оплаты -->
      <div class="card__payment">
        <span
          v-if="props.type === 'edit'"
          class="card__payment-comment s6"
          >{{ $t('payment-methods') }}</span
        >
        <ul class="card__payment-methods">
          <li class="card__payment-method">
            <IconBank class="card__payment-icon" />
          </li>
          <li class="card__payment-method">
            <IconPlus class="card__payment-icon" />
          </li>
        </ul>
      </div>
    </div>
    <!-- Описание транзакции -->
    <div class="card__transaction">
      <div class="card__price">
        <span class="card__price-range s5"
          >{{ $t('from-preposition') }} {{ formattedLowrange }} {{ $t('to-preposition') }}
          {{ formattedHighrange }} {{ props.currency }}</span
        >
        <span class="card__total-price s2">{{ formattedPrice }} {{ props.currency }}</span>
      </div>
      <AppButton
        v-if="props.type === 'default'"
        :label="$t('buy')"
        :size="'sm'"
      />
      <div
        v-else
        class="card__currency"
      >
        <IconBitcoin
          v-if="props.coin === 'bitcoin'"
          class="card__currency-icon"
        />
      </div>
    </div>
  </div>
</template>

<style lang="scss">
.card {
  min-width: 326px;
  border-radius: 6px;

  &:hover {
    outline: 2px solid var(--color-primary-600);
  }

  &__description {
    position: relative;
    display: flex;
    align-items: flex-end;
    justify-content: space-between;
    padding: 16px;
    background-color: var(--color-gray-700);
    border-radius: 6px 6px 0 0;
  }

  &__description_edit {
    flex-direction: column;
    gap: 18px;
    align-items: flex-start;
  }

  &__actions {
    position: absolute;
    top: 16px;
    right: 16px;
    display: flex;
    gap: 10px;
  }

  &__actions-btn {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    cursor: pointer;
    background-color: inherit;
    border: none;
  }

  &__actions-icon {
    color: var(--color-gray-400);
  }

  &__actions-btn:hover &__actions-icon {
    color: var(--color-gray-50);
  }

  &__seller {
    display: flex;
    gap: 12px;
  }

  &__seller-img {
    width: 42px;
    height: 42px;
    border-radius: 50%;
  }

  &__seller-info {
    display: flex;
    flex-direction: column;
    gap: 6px;
  }

  &__seller-name {
    color: var(--color-gray-50);
    text-decoration: none;
    cursor: pointer;
  }

  &__seller-name:hover {
    color: var(--color-primary-400);
    text-decoration: underline;
  }

  &__seller-rating {
    display: flex;
    gap: 8px;
    align-items: center;
  }

  &__seller-stars {
    display: flex;
    gap: 5px;
  }

  &__seller-star {
    width: 9px;
    height: 9px;
    color: var(--color-gray-400);
  }

  &__seller-star_filled {
    color: var(--color-primary-400);
  }

  &__seller-percent {
    color: var(--color-gray-300);
  }

  &__seller-deals {
    display: inline-flex;
    align-self: flex-start;
    padding: 2px 6px;
    color: var(--color-gray-50);
    background-color: var(--color-gray-600);
    border-radius: 6px;
  }

  &__payment {
    display: flex;
    flex-direction: column;
    gap: 8px;
  }

  &__payment-comment {
    color: var(--color-gray-300);
  }

  &__payment-methods {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    list-style-type: none;
  }

  &__payment-method {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 36px;
    height: 36px;
    padding: 6px;
    background-color: var(--color-gray-800);
    border-radius: 50%;
  }

  &__payment-icon {
    color: var(--color-gray-50);
  }

  &__transaction {
    display: flex;
    align-items: center;
    justify-content: space-between;
    padding: 16px;
    background-color: var(--color-gray-900);
    border-radius: 0 0 6px 6px;
  }

  &__price {
    display: flex;
    flex-direction: column;
    gap: 4px;
    align-items: flex-start;
  }

  &__price-range {
    color: var(--color-gray-400);
  }

  &__total-price {
    color: var(--color-gray-50);
  }

  &__currency {
    width: 36px;
    height: 36px;
    padding: 6px;
    background-color: var(--color-primary-400);
    border-radius: 50%;
  }

  &__currency-icon {
    color: var(--color-gray-50);
  }
}
</style>