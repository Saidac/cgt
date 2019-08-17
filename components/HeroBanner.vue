<template>
  <div class="heroBannerBackground">
    <div class="mt-64 justify-center">
      <h1
        style="font-family: Poppins"
        class="text-5xl block"
      >
        {{ title }}
      </h1>
      <UiSubTitle
        size="xl"
        class="leading-relaxed mb-8 w-3/5 mx-auto"
      >
        {{ paragraph }}
      </UiSubTitle>
      <ui-button class="lg w-56 h-16 mx-1">
        {{ buttonTextOne }}
      </ui-button>
      <ui-button
        ghost
        class="lg w-56 h-16 mx-1"
      >
        {{ buttonTextTwo }}
      </ui-button>
    </div>
  </div>
</template>

<script>
import UiButton from '@/components/atoms/button/index.vue';
import UiSubTitle from '@/components/atoms/subtitle/index.vue';

export default {
  components: {
    UiSubTitle,
    UiButton
  },
  props: {
    title: {
      type: String,
      default: 'title'
    },
    paragraph: {
      type: String,
      default: 'paragraph'
    },
  },
  data() {
    return {
      buttonTextOne: 'Our Positions',
      buttonTextTwo: 'Our Tech',
    }
  },
}
</script>

<style lang="postcss" scoped>
.heroBannerBackground {
  @apply bg-primary text-dark text-center leading-normal inline-block w-screen;
  height: 640px;
  background: linear-gradient(
      0deg,
      rgba(242, 243, 245, 0.5) 20%,
      rgba(242, 243, 245, 0) 45%,
      rgba(255, 255, 255, 1) 78%
    ),
    url(~assets/bg.svg);
}
</style>
