<template>
  <Swiper id="main-screen" />
  <Info />
  <Showcase />
  <ContactUs />
</template>
<script setup>
useHead({
  title: '3D4U - Главная страница',
  meta: [{ name: 'Главная страница' }],
  link: [{ rel: 'icon', type: 'image/x-icon', href: './icons/Ico3D4U.ico' }],
  htmlAttrs: {
    lang: 'ru'
  }
});
</script>
<style lang="scss"></style>
