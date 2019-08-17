<template>
  <button
    :disabled="isButtonDisabled"
    :class="[
      'text-center rounded-full',
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
        default: 'primary',
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
      hoverClassName() { // we want to change animate fade of background color on hover
        const { isButtonDisabled, ghost, backgroundColorClassName } = this;
        if(ghost === true) {
          return `hover:bg-${this.color} hover:border-transparent hover:text-white`
        } else if(!isButtonDisabled) {
          return `hover:${backgroundColorClassName}-dark` 
        } else {
          return '';
        }
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
        md: 'px-8 py-3 text-xl',
        lg: 'py-4 px-8 text-base',
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
