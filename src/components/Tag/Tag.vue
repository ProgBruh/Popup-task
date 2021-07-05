<template>
  <div class="tag" :class="{ 'tag--active': active }">
    <slot />
  </div>
</template>

<script>
export default {
  name: 'Tag',

  props: {
    active: {
      type: Boolean,
    },
  },
};
</script>
