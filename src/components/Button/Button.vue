<template>
  <button
    :type="type"
    name="button"
    class="button"
    :disabled="disabled"
    :class="{
      'button--big': !smallButton,
      'button--outlined': outlined,
      'button--disabled': disabled,
    }"
  >
    <span>
      <slot></slot>
    </span>
  </button>
</template>

<script>
export default {
  name: 'Button',

  props: {
    outlined: {
      type: Boolean,
    },
    type: {
      type: String,
      default: 'button',
    },
    outlined: {
      type: Boolean,
    },
    disabled: {
      type: Boolean,
    },
    size: {
      type: String,
      default: 'small',
    },
  },

  computed: {
    smallButton() {
      return this.size === 'small';
    },
  },
};
</script>
