<template>
  <div class="heroBannerBackground">
    <div class="absolute z-10 w-full">
      <div class="float-right">
        <UiLink
          url="#"
          color="secondary"
        >
          About Us
        </UiLink>
        <UiLink
          url="#"
          color="secondary"
        >
          Tech
        </UiLink>
      </div>
    </div>
    <div class="mt-64 justify-center">
      <UiHeadline class="text-5xl"> {{ title }} </UiHeadline>
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
import UiHeadline from '@/components/atoms/headline/index.vue';
import UiSubTitle from '@/components/atoms/subtitle/index.vue';
import UiLink from '@/components/atoms/link/index.vue';


export default {
  components: {
    UiHeadline,
    UiSubTitle,
    UiButton,
    UiLink
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
