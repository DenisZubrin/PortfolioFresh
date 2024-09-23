<template>
  <section class="contact-us">
    <NuxtImg
      class="contact-us__background"
      src="./backgrounds/contact_us_bg_wide.png"
      alt="bg"
    />
    <div class="contact-us__container container">
      <div class="contact-us__text">
        <h2 class="contact-us__heading">Свяжитесь с нами</h2>
        <p class="contact-us__description">
          Расскажите нам о своем проекте, мы рады сотрудничеству!
        </p>
      </div>
      <Form class="form contact-us__form" />
      <a class="contact-us__link-to-top" href="#main-screen">
        <IconBase
          :width="32"
          :height="32"
          :iconColor="'white'"
          :iconName="'ArrowUp'"
        >
          <IconArrowUp />
        </IconBase>
      </a>
    </div>
  </section>
</template>

<script setup></script>

<style lang="scss">

.contact-us {
  position: relative;

  &__background {
    position: absolute;
    top: 0;
    left: 0;
    object-fit: cover;
    width: 100%;
    height: 100%;
    z-index: 0;
    filter: brightness(30%);
  }

  &__container {
    padding-top: 85.5px;
    padding-bottom: 85.5px;
    display: flex;
    flex-direction: column;
    justify-content: center;
    position: relative;
  }

  &__text {
    z-index: 1;
  }

  &__heading {
    margin: 0 0 24px;
    @extend %h1;
    color: var(--color-text);
  }

  &__description {
    margin: 0 0 48px;
    @extend %p4;
    color: var(--color-text);
  }

  &__link-to-top {
    position: absolute;
    bottom: 24px;
    right: 40px;
  }

  &__arrow-top-icon {
    width: 32px;
    height: 32px;
    fill: var(--color-text);

    &:hover {
      fill: var(secondary);
    }
  }
}

@media screen and (max-width: 768px) {
  .contact-us {
    &__container {
      padding: 60px 32px;
    }

    &__link-to-top {
      right: 16px;
    }
  }
}
</style>
