<template>
  <div>
    <HeroBanner
      :title="heroTitle"
      :paragraph="heroParagraph"
      :call-to-action-name="heroCallToActionName"
      :call-to-action-name2="heroCallToActionName"
      :call-to-action-url="heroCallToActionUrl"
    />
  </div>
</template>

<script>
import HeroBanner from '@/components/HeroBanner.vue';

export default {
  components: {
    HeroBanner,
  },
  data() {
    return {
      heroTitle: 'Make a real impact',
      heroParagraph: 'Since the start of our journey, we have disrupted several markets by developing new solutions for the exchange of digital value.', // eslint-disable-line
      heroCallToActionName: 'Open positions',
      heroCallToActionName2: 'Our Tech',
      heroCallToActionUrl: 'hello from data index CTA URL'
    }
  },
}
</script>

<style>
</style>
