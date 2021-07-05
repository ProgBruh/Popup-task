<template>
  <div class="input">
    <span class="input__label">{{ label }}</span>
    <input
      type="text"
      class="input__field"
      :placeholder="placeholder"
      :class="{
        'input__field--disabled': disabled,
        'input__field--error': error,
      }"
      :value="value"
      @input="input"
      :disabled="disabled"
      ref="field"
    />
    <span class="input__error" v-if="error">
      Поле обязательно для заполнения
    </span>
  </div>
</template>

<script>
export default {
  name: 'Input',

  props: {
    label: {
      type: String,
    },
    placeholder: {
      type: String,
    },
    value: {
      type: String,
    },
    disabled: {
      type: Boolean,
    },
    error: {
      type: Boolean,
    },
  },

  methods: {
    input(e) {
      this.$emit('input', e.target.value);
    },
  },
};
</script>
