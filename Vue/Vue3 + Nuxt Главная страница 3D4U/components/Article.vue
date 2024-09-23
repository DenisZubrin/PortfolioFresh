<template>
  <NuxtLink to="#" class="article">
    <article class="article__container">
      <NuxtImg 
        class="article__bg" 
        :src="`./backgrounds/${img}`" 
        alt="bg" 
      />
      <div class="article__text">
        <h4 class="article__heading">
          {{ heading }}
        </h4>
        <div class="article__inner">
          <p class="article__description" v-if="text">
            {{ text }}
          </p>
          <span class="article__more-info">
            Подробнее
            <IconBase
              class="article__more-info-icon"
              :width="22"
              :height="22"
              :iconColor="'var(--color-text)'"
              :iconName="'Arrow Up Right'"
            >
              <IconArrowUpRight />
            </IconBase>
          </span>
        </div>
      </div>
    </article>
  </NuxtLink>
</template>

<script setup>

defineProps({
  img: {
    type: String,
  },
  heading: {
    type: String,
  },
  text: {
    type: String,
  },
});

</script>

<style lang="scss">

.article {
  text-decoration: none;
  overflow: hidden;
  border-radius: 8px;
  background: linear-gradient(
    to top right,
    var(--color-gradient-start),
    var(--color-gradient-end)
  );

  &__container {
    width: 100%;
    display: flex;
    padding: 24px;
    box-sizing: border-box;
    position: relative;
    justify-content: space-between;
    align-items: end;
    max-width: 668px;
    min-height: 560px;
  }

  // 1 и 2 карточки большие, 3, 4, 5 маленькие. Повторяется каждые 5 карточек
  &:nth-child(5n + 3) &__container,
  &:nth-child(5n + 4) &__container,
  &:nth-child(5n + 5) &__container {
    flex-direction: column;
    justify-content: end;
    align-items: center;
    max-width: 437px;
    min-height: 370px;
  }

  &__container:hover &__bg {
    transform: scale(1);
    filter: brightness(50%);
    transition: 0.3s;
  }

  &__bg {
    position: absolute;
    object-fit: cover;
    width: 100%;
    height: 100%;
    z-index: -1;
    top: 0;
    left: 0;
    transition: transform 0.3s;
    transform: scale(1.1);
  }

  &__text,
  &__external {
    z-index: 1;
    color: var(--color-text);
  }

  &__text {
    display: flex;
    flex-direction: column;
    width: 100%;
    
  }

  &:hover &__inner {
    max-height: 300px;
    transition: max-height 0.5s;
  }

  &__inner {
    max-height: 0;
    transition: max-height 0.3s;
    overflow: hidden;
    text-overflow: ellipsis;
    display: flex;
    justify-content: space-between;
  }

  &:nth-child(5n + 3) &__inner,
  &:nth-child(5n + 4) &__inner,
  &:nth-child(5n + 5) &__inner {
    flex-direction: column;
  }

  &__heading {
    @extend %s2;
    margin: 0;
    max-width: 467px;
  }

  &__description {
    @extend %p4;
    margin: 24px 0 0;
    color: var(--color-text);
    max-width: 467px;
  }

  &__more-info {
    display: flex;
    margin: 24px 0 0;

    &-icon {
      position: relative;
      top: -2px;
      left: 3px;
    }
  }
}

@media screen and (max-width: 1439px) {
  .article {
    &__container,
    &:nth-child(5n + 3) &__container,
    &:nth-child(5n + 4) &__container,
    &:nth-child(5n + 5) &__container {
      max-width: 100%;
      min-height: 560px;
    }

    &__inner {
      flex-direction: column;
    }

    &__text {
      width: 100%;
    }
  }
}

@media screen and (max-width: 1024px) {
  .article {
    &__container,
    &:nth-child(5n + 3) &__container,
    &:nth-child(5n + 4) &__container,
    &:nth-child(5n + 5) &__container {
      min-height: 470px;
    }
  }
}

@media screen and (max-width: 768px) {
  .article {
    &__container,
    &:nth-child(5n + 3) &__container,
    &:nth-child(5n + 4) &__container,
    &:nth-child(5n + 5) &__container {
      min-height: 370px;
    }
  }
}

@media screen and (max-width: 668px) {
  .article {
    &__container,
    &:nth-child(5n + 3) &__container,
    &:nth-child(5n + 4) &__container,
    &:nth-child(5n + 5) &__container {
      min-height: 460px;
    }
  }
}

@media screen and (max-width: 540px) {
  .article {
    &__container,
    &:nth-child(5n + 3) &__container,
    &:nth-child(5n + 4) &__container,
    &:nth-child(5n + 5) &__container {
      min-height: 370px;
    }
  }
}

@media screen and (max-width: 360px) {
  .article {
    &__container,
    &:nth-child(5n + 3) &__container,
    &:nth-child(5n + 4) &__container,
    &:nth-child(5n + 5) &__container {
      max-width: 100%;
      min-height: 274px;
    }
  }
}
</style>
