<script>
export default {
  name: 'UiHeadline',
  props: {
    /**
      Available priorities
      <br/>
      `'1', '2', '3', '4', '5', '6'`
    */
    priority: {
      type: String,
      validator: (val) => ['1', '2', '3', '4', '5', '6'].includes(val),
      default: '1',
    },
    /**
      color of the text as a string <strong>check predefined colors</strong>
    */
    color: {
      type: String,
      default: 'tertiary',
    },
    isSelectable: {
      type: Boolean,
      default: false,
    },
  },
  data() {
    return {
      fontSize: this.buildFontSizeClassName(),
      textColor: this.buildTextColorClassName(),
    };
  },
  methods: {
    buildFontSizeClassName() {
      const { priority } = this;
      const fontSize = {
        1: 'lg:text-5xl text-4xl',
        2: 'text-3xl',
        3: 'text-2xl',
        4: 'text-xl',
        5: 'text-lg',
        6: 'text-base',
      };
      return fontSize[priority];
    },

    buildTextColorClassName() {
      const { color } = this;
      return color ? `text-${color}` : '';
    },
  },
  render: function(createElement) {
    const { priority, fontSize, textColor, largeText, $slots, isSelectable } = this;
    const attributes = {
      class: ['font-pr', fontSize, textColor, largeText, { 'select-none': !isSelectable }],
    };
    const tagName = `h${priority}`;
    return createElement(tagName, attributes, $slots.default);
  },
};
</script>