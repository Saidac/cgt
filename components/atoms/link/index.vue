<template>
  <a
    :href="url"
    :class="[
      'font-pr leading-normal no-underline text-lg inline mx-5 w-full',
      textColorClassName,
      displayClassName,
      spacingClassNames,
      underlineClassName,
      fontFamilyClassName
    ]"
    ,
    @click="onClick"
  >
    <slot />
  </a>
</template>
<script>
export default {
  name: 'UiLink',
  props: {
    /**
     * Link URL
     */
    url: {
      type: String,
      default: '#',
    },
    /**
     * Link Text Color
     */
    color: {
      type: String,
      default: '',
    },
    /**
     * Link display style,
     * posible variations: `block, inline-block, inline``
     */
    displayClassName: {
      type: String,
      default: 'inline-block',
      validate: (val) => val.includes('block', 'inline-block', 'inline'),
    },
    isUnderlined: {
      type: Boolean,
      default: false,
    },
    /**
       Spacing around the text, the value should be a spacing class.
    */
    spacingClassNames: {
      type: String,
      default: '',
    },

    fontFamilyClassName: {
      type: String,
      default: 'font-pr',
    },
  },
  data() {
    return {
      textColorClassName: this.buildTextColorClassName(),
      underlineClassName: this.buildUnderlinedClassName(),
    };
  },
  methods: {
    buildTextColorClassName() {
      const { color } = this;
      return color ? `text-${this.color}` : '';
    },
    buildUnderlinedClassName() {
      const { isUnderlined } = this;
      return isUnderlined ? 'underline' : 'no-underline';
    },
    /**
     * Gets called when the user clicks on the Link
     *
     * @param {SyntheticEvent} event The `SyntheticEvent`
     */
    onClick(evt) {
      /**
       * Click Event
       *  @property {object}`
       */
      this.$emit('after:click', evt);
    },
  },
};
</script>
<style lang="postcss" scoped>
/*
a:before {
  content: "";
  position: absolute;
  width: 100%;
  height: 2px;
  top: 1.875em;
  left: 0;
  background-color: #0991d0;
  visibility: hidden;
  -webkit-transform: scaleX(0);
  transform: scaleX(0);
  -webkit-transition: all 0.3s ease-in-out 0s;
  transition: all 0.3s ease-in-out 0s;
}

a:hover:before {
  visibility: visible;
  -webkit-transform: scaleX(1);
  transform: scaleX(1);
} */
</style>
