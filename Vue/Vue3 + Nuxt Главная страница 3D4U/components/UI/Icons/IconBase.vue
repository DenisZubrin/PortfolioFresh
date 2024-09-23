<template>
  <svg
    :width="width"
    :height="height"
    viewBox="0 0 18 18"
    :aria-labelledby="iconName"
    role="presentation"
    xmlns="http://www.w3.org/2000/svg"
  >
    <title 
      :id="iconName" 
      lang="en"
    >
      {{ iconName }} icon
    </title>
    <g :fill="iconColor">
      <slot />
    </g>
  </svg>
</template>
<script setup>
defineProps({
  width: {
    type: [Number, String],
    default: 18,
  },
  height: {
    type: [Number, String],
    default: 18,
  },
  iconName: {
    type: String,
    default: 'Icon',
  },
  iconColor: {
    type: String,
    default: 'currentColor',
  },
});
</script>
<style lang="scss"></style>
