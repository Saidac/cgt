<template>
  <picture>
    <source
      v-if="hasSmartphoneSrcset"
      :srcset="smartphoneSrcset"
      :sizes="smartphoneSizes"
      media="(max-width: 767px)"
    >
    <source
      v-if="hasTabletSrcset"
      :srcset="tabletSrcset"
      :sizes="tabletSizes"
      media="(min-width: 768px) and (max-width: 1023px)"
    >
    <img
      :src="defaultImage"
      :alt="alt"
      :srcset="srcset"
      :sizes="sizes"
      :class="['select-none', { 'w-full': stretch }]"
    >
  </picture>
</template>

<script>
import { omit } from 'lodash';
import screenBreakpoints from '../../../enums/screen-breakpoints';

export default {
  name: 'CgResponsiveImage',
  props: {
    /** The base URL to create images, with a width and height placeholder which will be replaced by the component. */
    imageUrl: {
      type: String,
      required: true,
    },
    /** Possible values: 'all', 'tablet', 'smartphone', 'mobile'. The desidered mode of operation for the main image. If only "mobile" is passed, then desktop sizes will not be generated, etc. */
    mode: {
      type: String,
      default: 'all',
      validator(value) {
        // The value must match one of these strings -  tablet means tablet portrait, tablet landscape uses desktop sizes
        return ['all', 'tablet', 'smartphone', 'mobile'].indexOf(value) !== -1;
      },
    },
    /** percentage of screen occupied by image */
    widthOnScreen: {
      type: Number,
      default: 100,
    },
    /** percentage of screen occupied by image on tablet portrait if not set it uses witdhOnScreen */

    widthOnScreenTablet: {
      type: Number,
      default: undefined,
    },
    /** percentage of screen occupied by image on smartphone, if not set it uses witdhOnScreen */
    widthOnScreenSmartphone: {
      type: Number,
      default: undefined,
    },
    /** ratio of height respective to width */
    imageRatio: {
      type: Number,
      default: 16 / 9,
    },
    alt: {
      type: String,
      default: '',
    },
    stretch: {
      type: Boolean,
      default: false,
    },
  },
  data: () => {
    const baseSizes = omit(screenBreakpoints, 'default');
    const { default: defaultWidth } = screenBreakpoints;

    return {
      fullScreenWidth: 100,
      widthPlaceholder: '%width%',
      heightPlaceholder: '%height%',
      baseSizes,
      defaultWidth,
    };
  },
  computed: {
    defaultImage() {
      const {
        getWidthAdaptedToWidthOnScreen,
        defaultWidth,
        widthOnScreen,
        getImageUrlWithWidthAndHeight,
        getHeightFromWidth,
      } = this;
      const finalWidth = getWidthAdaptedToWidthOnScreen(defaultWidth, widthOnScreen);

      return getImageUrlWithWidthAndHeight(finalWidth, getHeightFromWidth(finalWidth));
    },
    srcset() {
      const {
        hasTabletAndMobileDefined,
        srcsetSizes,
        widthOnScreen,
        getSrcsetSizes,
        getSrcsetString,
        widthOnScreenTablet,
      } = this;
      let currentSrcsetSizes = srcsetSizes;
      let currentWidthOnScreen = widthOnScreen;

      if (!hasTabletAndMobileDefined) {
        currentSrcsetSizes = getSrcsetSizes('desktop');
        currentWidthOnScreen = widthOnScreenTablet;
      }

      return getSrcsetString(currentSrcsetSizes, currentWidthOnScreen);
    },
    tabletSrcset() {
      const { getSrcsetSizes, getSrcsetString, widthOnScreenTablet } = this;
      const tabledSrcsetSizes = getSrcsetSizes('tablet');

      return getSrcsetString(tabledSrcsetSizes, widthOnScreenTablet);
    },
    smartphoneSrcset() {
      const { getSrcsetSizes, getSrcsetString, widthOnScreenSmartphone } = this;
      const smartphoneSrcsetSizes = getSrcsetSizes('smartphone');

      return getSrcsetString(smartphoneSrcsetSizes, widthOnScreenSmartphone);
    },
    hasTabletSrcset() {
      const { widthOnScreenTablet, widthOnScreen } = this;
      const isWidthOnScreenTabletDefined = typeof widthOnScreenTablet !== 'undefined';
      const isWidthEqual = widthOnScreenTablet !== widthOnScreen;

      return isWidthOnScreenTabletDefined && isWidthEqual;
    },
    hasTabletAndMobileDefined() {
      const { widthOnScreenTablet, widthOnScreenSmartphone } = this;
      const isWidthOnScreenTabletDefined = typeof widthOnScreenTablet === 'undefined';
      const isWidthOnScreenSmartphone = typeof widthOnScreenSmartphone === 'undefined';

      return isWidthOnScreenTabletDefined && isWidthOnScreenSmartphone;
    },
    hasSmartphoneSrcset() {
      const { widthOnScreenSmartphone, widthOnScreen } = this;
      const iswidthOnScreenSmartphoneDefined = typeof widthOnScreenSmartphone !== 'undefined';
      const isWidthEqual = widthOnScreenSmartphone !== widthOnScreen;

      return iswidthOnScreenSmartphoneDefined && isWidthEqual;
    },
    sizes() {
      return `${this.widthOnScreen}vw`;
    },
    tabletSizes() {
      return `${this.widthOnScreenTablet}vw`;
    },
    smartphoneSizes() {
      return `${this.widthOnScreenSmartphone}vw`;
    },
    srcsetSizes() {
      const { getSrcsetSizes, mode } = this;
      return getSrcsetSizes(mode);
    },
  },
  methods: {
    getSrcsetSizes(mode) {
      const {
        baseSizes: { tabletPortrait, smartphone, desktop },
      } = this;

      switch (mode) {
        case 'tablet':
          return tabletPortrait;
        case 'smartphone':
          return smartphone;
        case 'mobile':
          return [...new Set([...tabletPortrait, ...smartphone])];
        case 'desktop':
          return desktop;
        case 'all':
        default:
          return [...new Set([...desktop, ...tabletPortrait, ...smartphone])];
      }
    },
    getHeightFromWidth(width) {
      return Math.round(width / this.imageRatio);
    },
    getSrcsetString(srcSets, widthOnScreen) {
      return srcSets.map((width) => this.getScreenSrcset(width, widthOnScreen)).join(', ');
    },
    getScreenSrcset(width, deviceWidth) {
      const {
        getWidthAdaptedToWidthOnScreen,
        getImageUrlWithWidthAndHeight,
        getHeightFromWidth,
      } = this;
      const finalWidth = getWidthAdaptedToWidthOnScreen(width, deviceWidth);
      const imageUrlWithWidthAndHeight = getImageUrlWithWidthAndHeight(
        finalWidth,
        getHeightFromWidth(finalWidth)
      );

      return `${imageUrlWithWidthAndHeight} ${finalWidth}w`;
    },
    getWidthAdaptedToWidthOnScreen(width, widthOnScreen = this.fullScreenWidth) {
      const { fullScreenWidth } = this;
      if (widthOnScreen >= fullScreenWidth) return width;
      return Math.round((width / fullScreenWidth) * widthOnScreen);
    },
    getImageUrlWithWidthAndHeight(width, height) {
      const { imageUrl, widthPlaceholder, heightPlaceholder } = this;
      return imageUrl.replace(widthPlaceholder, width).replace(heightPlaceholder, height);
    },
  },
};
</script>