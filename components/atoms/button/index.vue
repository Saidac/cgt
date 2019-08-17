<template>
  <button
    :disabled="isButtonDisabled"
    :class="[
      'text-center text-xl rounded-full my-12 py-4 px-8',
      fontColorClassName,
      backgroundColorClassName,
      hoverClassName,
      borderClassName,
      sizeClassNames,
      {
        'w-full': isFullWidth,
      },
      {
        'opacity-50 cursor-not-allowed': isButtonDisabled,
      },
    ]"
  >
    <slot />
  </button>
</template>

<script>
  export default {
    name: 'UiButton',
    props: {
      ghost: {
        type: Boolean,
        default: false,
      },
      color: {
        type: String,
        default: 'secondary',
      },
      size: {
        type: String,
        default: 'md',
      },
      isFullWidth: {
        type: Boolean,
        default: false,
      },
      isDisabled: {
      type: Boolean,
      default: false,
      },
    },
    data() {
      const backgroundColorClassName = this.buildBackgroundColorClassName();
      return {
        backgroundColorClassName,
        fontColorClassName: this.buildFontColorClassName(),
        borderClassName: this.buildBorderClassName(),
        sizeClassNames: this.buildSizeClassNames(),
      };
    },
    computed: {
      isButtonDisabled() {
      return this.isDisabled;
      },
      hoverClassName() {
        const { isButtonDisabled, backgroundColorClassName } = this;
        return !isButtonDisabled ? `hover:${backgroundColorClassName}-dark` : '';
      },
    },
     methods: {
    buildBackgroundColorClassName() {
      const color = this.ghost ? 'transparent' : this.color;
      return `bg-${color}`;
    },
    buildBorderClassName() {
      return this.ghost ? `border ${this.color}` : 'hover:border-transparent';
    },
    buildFontColorClassName() {
      const color = this.ghost ? this.color : 'white';
      return `text-${color}`;
    },
    buildSizeClassNames() {
      const sizes = {
        xs: 'px-6 py-1 text-xs',
        sm: 'px-6 py-2 text-sm',
        md: 'px-8 py-3 text-base',
        lg: 'py-3 px-8 lg:py-4 text-base',
      };
      return sizes[this.size];
    },
    handleClick(evt) {
      if (this.isButtonDisabled) return;
      this.$emit('after:click', evt);
    },
  },
  }
</script>

<style lang="postcss" scoped>
</style>
