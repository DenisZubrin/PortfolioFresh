<template>
  <section class="info">
    <div class="info__container container">
      <div class="info__card info__about-us">
        <h3 class="info__heading">Мы – студия <br />3D-визуализации 3D4U</h3>
        <p class="info__description">
          Наш основной принцип – индивидуальный подход к каждому клиенту.
          Огромный опыт работы позволяет нам воплощать проекты любой сложности –
          от небольших элементов интерьера до комплексного решения
          многофункциональных центров.
        </p>
        <Button
          class="button info__button"
          :text="'Узнать больше'" 
        >
          <template #icon>
            <IconBase
              class="button__icon-wrap"
              :width="22"
              :height="22"
              :iconName="'ArrowUpRight'"
            >
              <IconArrowUpRight class="button__icon-wrap"/>
            </IconBase>
          </template>
        </Button>
      </div>
      <div class="info__card info__achievments">
        <p class="info__row">
          <span class="info__number">17</span
          ><span class="info__text">лет опыта работы</span>
        </p>
        <p class="info__row">
          <span class="info__number">7000+</span
          ><span class="info__text">проектов разной степени сложности</span>
        </p>
        <p class="info__row">
          <span class="info__number">80+</span
          ><span class="info__text">клиентов в сфере производства мебели</span>
        </p>
      </div>
      <div class="info__card info__achievments">
        <p class="info__row">
          <span class="info__number">80+</span
          ><span class="info__text">клиентов в сфере производства мебели</span>
        </p>
        <p class="info__row">
          <span class="info__number">170</span
          ><span class="info__text">средний опыт сотрудника</span>
        </p>
        <p class="info__row">
          <span class="info__number">7000+</span
          ><span class="info__text">Мы входим в группу компаний ИНКОМ</span>
        </p>
      </div>
      <div class="info__card info__picture">
        <NuxtImg
          class="info__card-bg"
          src="./backgrounds/showcase_article_bg_3.png"
          alt="info card bg"
        />
      </div>
    </div>
  </section>
</template>

<script setup></script>

<style lang="scss">
.info {
  &__container {
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
    padding-top: 100px;
    padding-bottom: 100px;
    gap: 24px;
  }

  &__card {
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    border-radius: 8px;
    background-color: inherit;
    min-height: 422px;
    max-width: 322px;
    width: 100%;
    gap: 24px;
  }

  &__heading {
    @extend %h3;
    color: var(--color-text);
    margin: 0;
  }

  &__description {
    @extend %p3;
    color: var(--color-text);
    margin: 0;
  }

  &__achievments {
    background-color: var(--color-filler);
    padding: 44px 32px;
  }

  &__row {
    margin: 0;
  }

  &__text {
    @extend %p4;
    color: var(--color-text);
  }

  &__number {
    @extend %num;
    color: var(--color-text);
    display: block;
  }

  &__picture {
    position: relative;
  }

  &__card-bg {
    position: absolute;
    border-radius: 8px;
    width: 100%;
    height: 100%;
    top: 0;
    left: 0;
    object-fit: cover;
  }
}

@media screen and (max-width: 1439px) {
  .info {
    &__card {
      max-width: 31%;
    }

    &__picture {
      max-width: 100%;
    }
  }
}
@media screen and (max-width: 768px) {
  .info {
    &__container {
      justify-content: center;
      padding-top: 60px;
      padding-bottom: 56px;
    }

    &__card {
      max-width: calc(50% - 24px);
    }
  }
}

@media screen and (max-width: 600px) {
  .info {
    &__container {
      flex-direction: column;
    }

    &__heading {
      font-size: 24px;
    }

    &__description {
      margin: 0 0 16px;
    }

    &__card {
      max-width: 100%;
      min-height: 0;
    }

    &__row {
      display: flex;
      justify-content: center;
      margin: 0 0 16px;
      
      &:last-child {
        margin: 0;
      }
    }

    &__achievments {
      padding: 24px;
      gap: 0;
    }

    &__number {
      font-size: 28px;
      display: block;
      width: 40%;
    }

    &__text {
      width: 60%;
    }

    &__button {
      width: 100%;
      max-height: 48px;
    }
  }
}
</style>
