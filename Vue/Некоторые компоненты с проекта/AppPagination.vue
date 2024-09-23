<script setup lang="ts">
import { computed, watch } from 'vue'
import { RouterLink, useRoute, useRouter } from 'vue-router'
import type { RouteLocationNormalized, Router } from 'vue-router'
import IconCaretLeft from '@/assets/icons/caret-left.svg?component'
import IconCaretRight from '@/assets/icons/caret-right.svg?component'

const props = withDefaults(
  defineProps<{
    pages: number
  }>(),
  {
    pages: 20,
  }
)

const route: RouteLocationNormalized = useRoute()
const router: Router = useRouter()
const currentPage = computed((): number => {
  if (route.query.page && +route.query.page <= props.pages && +route.query.page > 0) {
    return +route.query.page
  } else {
    return 1
  }
})

// Навигация

const getPreviousPage = (): number => {
  if (currentPage.value === 1) {
    return 1
  } else {
    return currentPage.value - 1
  }
}
const getNextPage = (): number => {
  if (currentPage.value === props.pages) {
    return props.pages
  } else {
    return currentPage.value + 1
  }
}
const goToPage = (page: number): string => {
  return `/?page=${page}`
}
const goToFirstPage = (): string => {
  return `/?page=1`
}

watch(currentPage, () => {
  if (currentPage.value === 1) {
    router.push(goToFirstPage())
  }
})

// Отображаем определенное количество страниц

const sliceLength = 5
let sliceStart = computed((): number => {
  if (currentPage.value <= sliceLength) {
    return 0
  } else if (currentPage.value + sliceLength >= props.pages) {
    return props.pages - sliceLength
  } else {
    return currentPage.value - sliceLength
  }
})

// Отслеживаем изменения количества страниц

let pagesNumbers: number[] = []
for (let i = 1; i <= props.pages; i++) {
  pagesNumbers.push(i)
}

watch(props, () => {
  const result = []
  for (let i = 1; i <= props.pages; i++) {
    result.push(i)
  }
  pagesNumbers = result
})

// Скрываем страницы, если не помещаются

const showFirstPage = computed((): boolean => {
  if (props.pages > sliceLength + 2 && currentPage.value > sliceLength) {
    return true
  } else {
    return false
  }
})

const showLastPage = computed((): boolean => {
  if (props.pages > sliceLength + 2 && currentPage.value < props.pages - 2) {
    return true
  } else {
    return false
  }
})

// Размер среза в зависимости от страницы

const pagesSlice = computed((): number[] => {
  if (showFirstPage.value && showLastPage.value) {
    return pagesNumbers.slice(currentPage.value - 2, currentPage.value + 1)
  } else if (props.pages > sliceLength + 2) {
    return pagesNumbers.slice(sliceStart.value, sliceStart.value + sliceLength)
  } else {
    return pagesNumbers
  }
})
</script>

<template>
  <nav
    v-if="props.pages > 1"
    class="app-pagination"
  >
    <RouterLink
      :to="goToPage(getPreviousPage())"
      class="app-pagination__link"
    >
      <IconCaretLeft />
    </RouterLink>
    <ul class="app-pagination__list">
      <template v-if="showFirstPage">
        <li
          :key="1"
          :class="['app-pagination__item', { 'app-pagination__item_active': currentPage === 1 }]"
        >
          <RouterLink
            :to="goToFirstPage()"
            class="app-pagination__link"
          >
            {{ 1 }}
          </RouterLink>
        </li>
        <li class="app-pagination__item app-pagination__link">...</li>
      </template>

      <li
        v-for="page in pagesSlice"
        :key="page"
        :class="['app-pagination__item', { 'app-pagination__item_active': page === currentPage }]"
      >
        <RouterLink
          :to="goToPage(page)"
          class="app-pagination__link"
        >
          {{ page }}
        </RouterLink>
      </li>
      <template v-if="showLastPage">
        <li class="app-pagination__item app-pagination__link">...</li>
        <li
          :key="props.pages"
          :class="[
            'app-pagination__item',
            { 'app-pagination__item_active': currentPage === props.pages },
          ]"
        >
          <RouterLink
            :to="goToPage(props.pages)"
            class="app-pagination__link"
          >
            {{ props.pages }}
          </RouterLink>
        </li>
      </template>
    </ul>
    <RouterLink
      :to="goToPage(getNextPage())"
      class="app-pagination__link"
    >
      <IconCaretRight />
    </RouterLink>
  </nav>
</template>

<style lang="scss">
.app-pagination {
  display: inline-flex;
  flex-wrap: wrap;
  overflow: hidden;
  background-color: var(--color-gray-800);
  border: 1px solid var(--color-gray-600);
  border-radius: 6px;

  &__link {
    display: block;
    padding: 8px 12px;
    color: var(--color-gray-0);
    text-decoration: none;
  }
  &__list {
    display: flex;
    flex-wrap: wrap;
    list-style-type: none;
  }
  &__item {
    border-left: 1px solid var(--color-gray-600);
    transition: 0.3s ease-in-out;
  }
  &__item:last-child {
    border-right: 1px solid var(--color-gray-600);
  }

  &__item_active {
    background-color: var(--color-primary-400);
  }
}
</style>
