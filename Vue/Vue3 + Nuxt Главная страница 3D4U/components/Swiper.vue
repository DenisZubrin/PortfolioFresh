<template>
  <swiper
    :direction="'vertical'"
    :slides-per-view="1"
    :pagination="{ clickable: true }"
    :modules="modules"
    :mousewheel="{
      enabled: true,
      releaseOnEdges: true
    }"
    :watchSlidesProgress="true"
    :speed="1000"
  >
    <swiper-slide 
      v-for="(slide, index) in slides" 
      :key="index"
    >
      <Slide
        :image="slide.image"
        :links="slide.links"
        :heading="slide.heading"
        :description="slide.description"
      />
    </swiper-slide>
  </swiper>
</template>

<script setup>
import { Swiper, SwiperSlide } from 'swiper/vue';
import { Pagination, Mousewheel } from 'swiper/modules';
import 'swiper/scss';
import 'swiper/scss/pagination';
import 'swiper/scss/mousewheel';

const modules = [Pagination, Mousewheel];
const slides = reactive([
  {
    image: 'slider_bg_1.png',
    heading: 'Визуализация мебели',
    description:
      'Такой уровень реализма, что отличить смоделированную мебель от реальной смогут лишь профессионалы.',
    links: ['Корпусная мебель', 'Мягкая мебель', 'Обеденные группы', 'Двери'],
  },
  {
    image: 'slider_bg_2.png',
    heading: 'Верстка каталогов',
    description:
      'Профессиональная верстка каталогов подчеркнет все достоинства вашего товара и поможет грамотно его презентовать.',
    links: ['Смотреть проекты'],
  },
  {
    image: 'slider_bg_3.png',
    heading: 'Дизайн-проекты',
    description:
      'От квартиры-студии до торгового центра – реалистичная 3D-визуализация с максимальной точностью покажет будущее помещение.',
    links: ['Интерьеры', 'Экстерьеры', 'Торговые помещения'],
  },
  {
    image: 'slider_bg_4.png',
    heading: '3D-тур',
    description:
      'Современное решение для красочной и наглядной презентации помещения. Прогуляйтесь по виртуальному объекту, не выходя из дома.',
    links: ['Смотреть проекты'],
  },
  {
    image: 'slider_bg_5.png',
    heading: 'Онлайн-конструктор',
    description:
      'Удобный и функциональный инструмент для визуализации и расчета стоимости мебели в помещении.',
    links: ['Смотреть проекты'],
  },
]);

</script>

<style lang="scss">
@import '~/assets/styles/swiper.scss';
</style>
