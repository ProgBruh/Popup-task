<template lang="html">
  <div class="app">
    <Button class="app__button" size="big" outlined @click.native="openPopup"
      >Налоговый вычет</Button
    >
    <Popup v-if="show" @close="closePopup" />
  </div>
</template>

<script>
import Button from './Button/Button.vue';
import Popup from './Popup/Popup.vue';

export default {
  name: 'App',

  components: {
    Button,
    Popup,
  },

  data() {
    return {
      show: false,
    };
  },

  methods: {
    openPopup() {
      this.show = true;
    },
    closePopup() {
      this.show = false;
    },
  },
};
</script>
