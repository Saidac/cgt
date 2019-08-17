<script>
export default {
  name: 'UiSubTitle',
  props: {
    /**
     * Priority of the subtitle based on title value
     * Available priorities `'2', '3', '4', '5', '6'`
     */
    priority: {
      type: String,
      validator: (val) => ['2', '3', '4', '5', '6'].includes(val),
      default: '2',
    },
    /**
     * Text size
     */
    size: {
      type: String,
      default: 'base',
    },
    /**
     * Text color
     */
    color: {
      type: String,
      default: 'tertiary',
    },
  },
  data() {
    return {
      textSizeClassName: this.buildTextSizeClassName(),
      textColorClassName: this.buildTextColorClassName(),
    };
  },
  methods: {
    buildTextSizeClassName() {
      const { size } = this;
      return size ? `text-${size}` : '';
    },
    buildTextColorClassName() {
      const { color } = this;
      return color ? `text-${color}` : '';
    },
  },
  render: function(createElement) {
    const { priority, textSizeClassName, textColorClassName, $slots } = this;
    const tagName = `h${priority}`;
    const attributes = { class: ['font-pr font-light', textSizeClassName, textColorClassName] };
    return createElement(tagName, attributes, $slots.default);
  },
};
</script>