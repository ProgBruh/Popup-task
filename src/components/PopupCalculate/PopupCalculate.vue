<template>
  <div class="popup-calculate">
    <span class="popup-calculate__title">
      Итого можете внести в качестве досрочных:
    </span>
    <div class="popup-calculate__list">
      <div
        class="popup-calculate__wrapper"
        v-for="(item, index) of items"
        :key="index"
      >
        <Checkbox class="popup-calculate__checkbox" />
        <span class="popup-calculate__tax">
          {{ separateThousands(item) }}
          <span class="popup-calculate__year">
            {{ byYear(index + 1) }}
          </span>
        </span>
      </div>
    </div>
  </div>
</template>

<script>
import Checkbox from '~/components/Checkbox/Checkbox.vue';

export default {
  name: 'PopupCalculate',

  components: {
    Checkbox,
  },

  props: {
    items: {
      type: Array,
    },
  },

  computed: {
    tax() {
      return `${this.taxDeduction} рублей`;
    },
  },

  data() {
    return {
      endings: {
        1: '-ый',
        2: '-ой',
        3: '-ий',
        4: '-ый',
        5: '-ый',
        6: '-ой',
        7: '-ой',
        8: '-ой',
        9: '-ый',
      },
    };
  },

  methods: {
    byYear(year) {
      return `в ${year}${this.endings[year]} год`;
    },
    separateThousands(num) {
      return num.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ' ') + ' рублей';
    },
  },
};
</script>
