<template>
  <footer class="footer">
    <div class="footer__container container">
      <div class="footer__info">
        <div class="footer__column footer__about-us">
          <NavLink to="/" class="logo footer__logo">
            <figure class="logo__container footer__logo-container">
              <IconBase
                class="logo__icon footer__logo-icon"
                :width="68"
                :height="75"
                :iconColor="'var(--color-text)'"
                :iconName="'3D4U logo with caption'"
              >
                <Icon3D4ULogoCaption />
              </IconBase>
              <figcaption class="logo__caption footer__logo-caption">
                Профессиональная <br />студия 3D-визуализации <br />3D FOR YOU
              </figcaption>
            </figure>
          </NavLink>
        </div>
        <nav class="footer__sitemap">
          <ul class="footer__column footer__list">
            <li class="footer__item footer__item_margin">
              <NavLink to="#" class="link footer__link footer__link_highlighted"
                >Визуализация мебели</NavLink
              >
            </li>
            <li class="footer__item">
              <NavLink to="#" class="link footer__link">Мягкая мебель</NavLink>
            </li>
            <li class="footer__item">
              <NavLink to="#" class="link footer__link"
                >Корпусная мебель</NavLink
              >
            </li>
            <li class="footer__item">
              <NavLink to="#" class="link footer__link"
                >Обеденные группые</NavLink
              >
            </li>
            <li class="footer__item">
              <NavLink to="#" class="link footer__link">Двери</NavLink>
            </li>
          </ul>
          <ul class="footer__column footer__list">
            <li class="footer__item footer__item_margin">
              <NavLink to="#" class="link footer__link footer__link_highlighted"
                >Дизайн-проекты</NavLink
              >
            </li>
            <li class="footer__item">
              <NavLink to="#" class="link footer__link">Интерьеры</NavLink>
            </li>
            <li class="footer__item">
              <NavLink to="#" class="link footer__link">Экстерьеры</NavLink>
            </li>
            <li class="footer__item">
              <NavLink to="#" class="link footer__link"
                >Торговые помещения</NavLink
              >
            </li>
            <li class="footer__item">
              <NavLink to="#" class="link footer__link">3D-туры</NavLink>
            </li>
          </ul>
          <ul class="footer__column footer__list">
            <li class="footer__item footer__item_margin">
              <NavLink to="#" class="link footer__link footer__link_highlighted"
                >Верстка каталогов</NavLink
              >
            </li>
            <li class="footer__item footer__item_margin">
              <NavLink to="#" class="link footer__link footer__link_highlighted"
                >Онлайн-конструктор</NavLink
              >
            </li>
            <li class="footer__item footer__item_margin">
              <NavLink to="#" class="link footer__link footer__link_highlighted"
                >О компании</NavLink
              >
            </li>
            <li class="footer__item footer__item_margin">
              <NavLink to="#" class="link footer__link footer__link_highlighted"
                >Контакты</NavLink
              >
            </li>
          </ul>
          <address class="footer__address footer__column footer__list">
            <a class="footer__phone" href="'tel:+79656369353'"
              >+7 (965) 63-69-353</a
            >
            <a class="footer__email" href="mailto:3d4u@bk.ru">3d4u@bk.ru</a>
            <p class="footer__office">
              <span class="footer__office-building"
                >г. Пенза, ул. Дружбы, 6<br /> (Технопарк "Яблочков"), оф. 415</span
              >
              <span class="footer__office-worktime">пн-пт с 9:00 до 17:00</span>
            </p>
          </address>
        </nav>
      </div>
      <div class="footer__terms">
        <ul class="footer__policies">
          <li class="footer__copyright">
            <span class="footer__link">© 2024 3D4U. Все права защищены</span>
          </li>
          <li class="footer__copyright">
            <NavLink to="#" class="link footer__link"
              >Пользовательское соглашение</NavLink
            >
          </li>
          <li class="footer__copyright">
            <NavLink to="#" class="link footer__link"
              >Политика конфиденциальности</NavLink
            >
          </li>
        </ul>
        <div class="footer__created-by">
          <a href="#" class="footer__company-link"
            ><NuxtImg
              class="footer__company-logo"
              src="/icons/INKOM_logo.png"
              alt="INKOM logo"
          /></a>
          <a href="#" class="footer__company-link"
            ><NuxtImg
              class="footer__company-logo"
              src="/icons/MATCH_logo.png"
              alt="MATCH logo"
          /></a>
        </div>
      </div>
    </div>
  </footer>
</template>

<script setup></script>

<style lang="scss">

.footer {
  background-color: var(--color-footer-bg);

  &__container {
    padding: 40px;
  }

  &__logo {
    &-container {
      flex-direction: column;
      align-items: start;
    }

    &-icon {
      width: 68px;
      height: 75px;
    }

    &-caption {
      @extend %p4;
      margin: 14px 0 0 0;
    }
  }

  &__info {
    display: flex;
    margin: 0 0 32px;
    gap: 24px;
  }

  &__column {
    max-width: 252px;
    width: 100%;
    min-height: 149px;
    display: flex;
    flex-direction: column;
  }

  &__sitemap {
    display: flex;
    justify-content: space-between;
    width: 100%;
    flex-wrap: wrap;
    gap: 24px;
  }

  &__list {
    margin: 0;
    padding: 0;
    list-style-type: none;
  }

  &__item {
    margin: 0 0 8px;

    &_margin {
      margin: 0 0 12px;
    }
  }

  &__link {
    color: var(--color-link-text);
    @extend %p4;

    &_highlighted {
      @extend %s4; 
      color: var(--color-text);
    }
  }

  &__address {
    font-style: normal;
  }

  &__phone,
  &__email {
    color: var(--color-text);
    display: inline-block;
    margin: 0 0 12px;

    &:hover {
      color: var(--color-secondary);
    }
  }

  &__phone {
    @extend %s2;
    text-decoration: none;
  }

  &__email {
    @extend %p4;
  }

  &__office {
    margin: 0;
    @extend %p4;

    &-building {
      color: var(--color-text);
      display: block;
      width: 100%;
    }

    &-worktime {
      color: var(--color-link-text);
    }
  }

  &__terms {
    border-top: 1px solid var(--color-link-text);
    padding: 32px 0 0 0;
    display: flex;
    flex-wrap: wrap;
    justify-content: space-between;
  }

  &__policies {
    list-style-type: none;
    display: flex;
    margin: 0;
    padding: 0;
    gap: 24px;
  }

  &__created-by {
    display: flex;
    align-items: center;
    gap: 24px;
  }

  &__company-logo {
    min-height: 24px;
    opacity: 0.7;
    cursor: pointer;

    &:hover {
      opacity: 1;
    }
  }
}

@media screen and (max-width: 1090px) {
  .footer {
    &__policies {
      justify-content: space-between;
      width: 100%;
      margin: 0 0 24px;
    }

    &__created-by {
      width: 100%;
      justify-content: end;
    }
  }
}

@media screen and (max-width: 885px) {
  .footer {
    &__about-us {
      max-width: 180px;
    }

    &__column {
      max-width: 200px;
    }
    &__list {
      max-width: calc(50% - 12px);
    }
  }
}

@media screen and (max-width: 885px) {
  .footer {
    &__container {
      padding: 60px 32px;
    }
  }
}

@media screen and (max-width: 610px) {
  .footer {
    &__sitemap {
      flex-direction: column;
    }

    &__list {
      max-width: 100%;
    }
  }
}

@media screen and (max-width: 540px) {
  .footer {
    &__container {
      padding: 40px 32px;
    }

    &__column {
      min-height: 0;
    }

    &__info {
      flex-direction: column;
    }
    &__about-us {
      max-width: 100%;
    }

    &__logo-container {
      flex-direction: row;
      align-items: center;
    }

    &__logo-caption {
      margin: 0 0 0 14px;

    }

    &__terms {
      padding: 24px 0 0 0;
    }

    &__terms,
    &__policies,
    &__created-by {
      flex-direction: column;
      gap: 12px;
    }

    &__policies {
      margin: 0;
    }

    &__created-by {
      align-items: start;
    }
  }
}

@media screen and (max-width: 360px) {
  .footer {
    &__container {
      padding: 40px 16px;
    }
  }
}
</style>
