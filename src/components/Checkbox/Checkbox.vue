<template>
  <label
    class="checkbox"
    :class="{ 'checkbox--active': active, 'checkbox--disabled': disabled }"
  >
    <input
      type="checkbox"
      class="checkbox__field"
      :disabled="disabled"
      @input="input"
    />
    <span
      class="checkbox__label"
      :class="{ 'checkbox__label--active': active }"
    />
  </label>
</template>

<script>
export default {
  name: 'Checkbox',

  props: {
    disabled: {
      type: Boolean,
    },
  },

  data() {
    return {
      active: false,
    };
  },

  methods: {
    input(e) {
      this.active = e.target.checked;
    },
  },
};
</script>
