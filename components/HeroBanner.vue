<template>
  <div
    style="height: 40rem;"
    class="bg-dark"
  >
    <div class="bg-fade">
      <img
        src="~/assets/bg.svg"
        style="position: fixed; top: 0px; left: 0px; z-index: -10;"
      >
      <h1 class="text-5xl block"> {{ title }} </h1>
      <p class="text-xl mx-auto w-3/5"> {{ paragraph }} </p>
      <ui-button
        outline
        type="primary"
        class="mt-4"
      >
        {{ buttonText }}
      </ui-button>
    </div>
  </div>
</template>

<script>
import UiButton from '@/components/atoms/button/index.vue';

export default {
  components: {
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
      buttonText: 'Hej',
    }
  },
}
</script>

<style lang="postcss" scoped>
.bg-fade {
  @apply bg-primary text-dark rounded-full my-12 py-4 w-48 inline-block text-white text-center leading-normal inline-block w-screen pt-64;

  position: fixed;
  z-index: 10;
  background: linear-gradient(
    to bottom,
    rgba(8, 22, 44, 0.65) 0%,
    rgba(0, 0, 0, 0.01) 99%,
    rgba(0, 0, 0, 0) 100%
  );
}
</style>
