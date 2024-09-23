<template>
  <header class="header">
    <div class="container header__container">
      <div
        @click="toggleMenu"
        :class="['burger header__burger',
          {
            burger_open: state.menuActive,
          }
        ]"
      >
        <div class="burger__line"></div>
        <div class="burger__line"></div>
        <div class="burger__line"></div>
      </div>
      <NuxtLink class="logo header__logo" to="/">
        <figure class="logo__container">
          <IconBase
            :width="46"
            :height="46"
            :iconColor="'var(--color-text)'"
            :iconName="'3D4U logo'"
          >
            <Icon3D4U-logo />
          </IconBase>
          <figcaption class="logo__caption header__logo-caption">
            Cтудия <br />3D-визуализации <br />3D FOR YOU
          </figcaption>
        </figure>
      </NuxtLink>
      <nav
        :class="[
          'nav header__nav',
        {
          header__nav_mobile: state.menuActive,
        }]"
      >
        <ul class="nav__list">
          <li class="nav__item">
            <div class="select nav__select">
              <NuxtLink
                class="link select__link nav__link"
                to="#"
                >Визуализация мебели</NuxtLink
              >
              <IconBase
                class="select__icon-wrap"
                :width="16"
                :height="16"
                :iconName="'CaretDown'"
              >
                <IconCaretDown class="select__icon"/>
              </IconBase>
              <ul class="select__list">
                <li class="select__item">
                  <NuxtLink to="#" class="link select__link"
                    >Мягкая мебель</NuxtLink
                  >
                </li>
                <li class="select__item">
                  <NuxtLink to="#" class="link select__link"
                    >Корпусная мебель</NuxtLink
                  >
                </li>
                <li class="select__item">
                  <NuxtLink to="#" class="link select__link"
                    >Обеденные группы</NuxtLink
                  >
                </li>
                <li class="select__item">
                  <NuxtLink to="#" class="link select__link">Дверь</NuxtLink>
                </li>
              </ul>
            </div>
          </li>
          <li class="nav__item">
            <NuxtLink to="#" class="link nav__link">Верстка каталогов</NuxtLink>
          </li>
          <li class="nav__item">
            <div class="select nav__select">
              <NuxtLink
                class="link select__link nav__link"
                to="#"
                >Дизайн-проекты</NuxtLink
              >
              <IconBase
                class="select__icon-wrap"
                :width="16"
                :height="16"
                :iconName="'CaretDown'"
              >
                <IconCaretDown class="select__icon"/>
              </IconBase>
              <ul class="select__list">
                <li class="select__item">
                  <NuxtLink to="#" class="link select__link"
                    >Мягкая мебель</NuxtLink
                  >
                </li>
                <li class="select__item">
                  <NuxtLink to="#" class="link select__link"
                    >Корпусная мебель</NuxtLink
                  >
                </li>
                <li class="select__item">
                  <NuxtLink to="#" class="link select__link"
                    >Обеденные группы</NuxtLink
                  >
                </li>
              </ul>
            </div>
          </li>
          <li class="nav__item">
            <NuxtLink to="#" class="link nav__link">3D-тур</NuxtLink>
          </li>
          <li class="nav__item">
            <NuxtLink to="#" class="link nav__link"
              >Онлайн-конструктор</NuxtLink
            >
          </li>
          <li class="nav__item">
            <NuxtLink to="#" class="link nav__link">О нас</NuxtLink>
          </li>
          <li class="nav__item">
            <NuxtLink to="#" class="link nav__link">Контакты</NuxtLink>
          </li>
        </ul>
        <Button
          @submit.prevent
          class="nav__button"
          outline
          :text="'Заказать проект'"
        >
          <template #icon>
            <IconBase
              class="button__icon-wrap"
              :width="22"
              :height="22"
              :iconColor="'var(--color-text)'"
              :iconName="'ArrowUpRight'"
            >
              <IconArrowUpRight class="button__icon"/>
            </IconBase>
          </template>
        </Button>
      </nav>
      <Button
        @submit.prevent
        outline
        :text="'Заказать проект'"
        class="header__button"
      >
        <template #icon>
          <IconBase
            class="button__icon-wrap header__button-icon"
            :width="22"
            :height="22"
            :iconColor="'var(--color-text)'"
            :iconName="'ArrowUpRight'"
          >
            <IconArrowUpRight class="button__icon"/>
          </IconBase>
        </template>
      </Button>
    </div>
  </header>
</template>

<script setup>

const state = reactive({
  menuActive: false,
});

const toggleMenu = () => {
  state.menuActive = !state.menuActive;
};

</script>

<style lang="scss">
.header {
  position: fixed;
  width: 100%;
  z-index: 2;
  background: linear-gradient(0deg, transparent, rgba(0, 0, 0, 0.5) 50%);

  &__container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    align-items: center;
    min-height: 78px;
  }

  &__logo-caption {
    margin: 0 0 0 10px;
  }

  &__button {
    display: none;
  }
}

.select {
  position: relative;
  display: flex;
  align-items: center;
  padding: 10px 0;

  &__icon-wrap {
    margin: 0 0 0 4px;
    transform: scale(1, -1);
    transition: 0.3s cubic-bezier(0.4, 0, 0.2, 1);
  }

  &__icon {
    fill: var(--color-text);
  }

  &__link:hover ~ &__icon-wrap {
    transition: 0.3s cubic-bezier(0.4, 0, 0.2, 1);
    transform: rotate(0deg);
  }

  &__link:hover ~ &__icon-wrap &__icon {
    fill: var(--color-secondary);
  }

  &:hover > &__list {
    opacity: 1;
    visibility: visible;
  }

  &__list {
    opacity: 0;
    visibility: hidden;
    position: absolute;
    top: 38px;
    left: -12px;
    list-style-type: none;
    border-radius: 8px;
    background-color: var(--color-filler);
    min-width: 252px;
    padding: 0;

    &:focus-visible {
      opacity: 1;
    }
  }

  &__item {
    padding: 8px 12px;
    cursor: pointer;

    &:hover,
    &:active {
      background-color: var(--color-secondary);
    }

    &:first-child {
      border-radius: 8px 8px 0 0;
    }
    &:last-child {
      border-radius: 0 0 8px 8px;
    }
  }
  &__link {
    color: var(--color-text);
  }

  &__item > &__link {
    &:hover,
    &:active {
      color: var(--color-text);

      &::before {
        display: none;
      }
    }
  }
}

.nav {
  display: flex;
  align-items: center;

  &__list {
    display: flex;
    align-items: center;
    margin: 0;
    padding: 0;
    list-style-type: none;
  }

  &__item:not(:last-child) {
    margin: 0 20px 0 0;
  }

  &__link {
    color: var(--color-text);
  }

  &__button {
    display: none;
  }
}

@media screen and (max-width: 1136px) {
  .header {
    &__container {
      padding-top: 12px;
      min-height: 60px;
    }

    &__nav {
      margin: 0;
      opacity: 0;
      visibility: hidden;
      position: fixed;
      top: 0;
      left: -100%;
      z-index: 2;
      width: 100%;
      height: 100%;
      display: flex;
      flex-direction: column;
      justify-content: space-between;
      align-items: center;
      transition: all 0.4s ease-in-out;

      &_mobile {
        opacity: 1;
        visibility: visible;
        left: 0;
        background-color: var(--color-primary);
      }
    }

    &__burger {
      display: block;
      z-index: 3;
    }

    &__logo {
      position: fixed;
      left: calc(50% - 23px);
      top: 12px;

      &-caption {
        display: none;
      }
    }

    &__button {
      display: block;
      padding: 8px 34px 8px 16px;
      min-height: 0;
    }

  }

  .nav {
    &__list {
      flex-direction: column;
      width: 100%;
      margin: 78px 0 30px;
    }

    &__item {
      border-top: 1px solid var(--color-text-elements);
      width: 100%;
      padding: 16px;

      &:not(:last-child) {
        margin: 0;
      }

      &:last-child {
        border-bottom: 1px solid var(--color-text-elements);
      }
    }

    &__link {
      color: var(--color-text);
    }

    &__button {
      display: block;
      max-width: 328px;
      width: 100%;
      margin: 0 0 30px;
      text-decoration: none;
    }
  }

  .select {
    flex-direction: column;
    align-items: start;
    padding: 0;

    &__icon-wrap {
      display: none;
    }

    &__list {
      width: 100%;
      position: static;
      opacity: 1;
      visibility: visible;
      background-color: inherit;
    }

    &__item {
      padding: 16px 12px 0;
      box-sizing: border-box;

      &:hover,
      &:active {
        background-color: inherit;
      }
    }
    &__item > &__link {
      color: var(--color-link-text);
    }
  }
}

@media screen and (max-width: 540px) {
  .header {
    &__button {
      border: none;
      padding: 0;

      &-icon {
        right: 0;
        top: -16px;
        width: 32px;
        height: 32px;
      }
    }

    &__button .button__text {
      display: none;
    }
  }
}
</style>
