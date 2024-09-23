<template>
  <section class="showcase">
    <div class="showcase__container container">
      <h2 class="showcase__heading">Каждый проект – уникальное произведение</h2>
      <p class="showcase__description">
        Уделяя большое внимание деталям, мы обращаем ваши мысли и пожелания в
        реалистичную и атмосферную картину
      </p>
      <div class="showcase__articles">
        <Article
          v-for="article in articles"
          class="article showcase__card"
          :key="article.id"
          :img="article.img"
          :heading="article.heading"
          :text="article.text"
        />
      </div>
    </div>
  </section>
</template>

<script setup>

const articles = reactive([
  {
    id: 1,
    img: 'showcase_article_bg_1.png',
    heading: 'Флагманский фирменный салон компании MGS в городе Самара',
    text: `Уникальное пространство, где дизайн и функциональность сочетаются для создания уютной и стильной атмосферы.`,
  },
  {
    id: 2,
    img: 'showcase_article_bg_2.png',
    heading: 'Пространство света',
    text: ``,
  },
  {
    id: 3,
    img: 'showcase_article_bg_3.png',
    heading: 'Эко-стайл лайф: Жизнь в зеленом тандеме',
    text: ``,
  },
  {
    id: 4,
    img: 'showcase_article_bg_4.png',
    heading: 'Мягкость махагонового пламени',
    text: `Цвет дивана словно ласковый покров, обвивающий каждый контур, делает его местом не только для сидения, но и для мечтательного погружения в мир гармонии.`,
  },
  {
    id: 5,
    img: 'showcase_article_bg_5.png',
    heading: 'Концепции проекта торгового центра "Московский" в г. Кузнецк',
    text: ``,
  },
  {
    id: 6,
    img: 'showcase_article_bg_6.png',
    heading: 'Мир уюта и изысканности с нашим эксклюзивным каталогом диванов',
    text: ``,
  },
  {
    id: 7,
    img: 'showcase_article_bg_7.png',
    heading: 'Флагманский фирменный салон компании MGS в городе Самара',
    text: ``,
  },
]);

</script>

<style lang="scss">

.showcase {
  &__container {
    padding-bottom: 100px;
  }

  &__heading {
    margin: 0;
    @extend %h2;
    color: var(--color-text);
    text-align: center;
  }

  &__description {
    @extend %p3;
    color: var(--color-text);
    margin: 24px auto 38px;
    text-align: center;
    max-width: 667px;
  }

  &__articles {
    display: flex;
    flex-wrap: wrap;
    gap: 24px;
  }

  &__row {
    display: flex;
    justify-content: space-between;
    flex-wrap: wrap;
    gap: 24px;
    width: 100%;
  }

  &__card {
    width: calc(50% - 12px);

    // 1 и 2 карточки большие, 3, 4, 5 маленькие. Повторяется каждые 5 карточек
    &:nth-child(5n + 3),
    &:nth-child(5n + 4),
    &:nth-child(5n + 5) {
      width: calc(33% - 12px);
    }
  }
}

@media screen and (max-width: 1439px) {
  .showcase {
    &__card,
    &__card:nth-child(5n + 3),
    &__card:nth-child(5n + 4),
    &__card:nth-child(5n + 5) {
      width: calc(50% - 12px);
    }

    &__card:last-child {
      width: 100%;
    }
  }
}

@media screen and (max-width: 668px) {
  .showcase {
    &__card,
    &__card:nth-child(5n + 3),
    &__card:nth-child(5n + 4),
    &__card:nth-child(5n + 5) {
      width: 100%;
    }

    &__container {
      padding-bottom: 56px;
    }
  }
}

@media screen and (max-width: 360px) {
  .showcase {
    &__description {
      @extend %p3;
    }

    &__container {
      padding-bottom: 56px;
    }
  }
}
</style>
