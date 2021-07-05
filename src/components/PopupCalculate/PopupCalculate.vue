<template>
  <div class="popup-calculate">
    <span class="popup-calculate__title">
      Итого можете внести в качестве досрочных:
    </span>
    <div class="popup-calculate__wrapper" v-for="n in 4" :key="n">
      <Checkbox class="popup-calculate__checkbox" />
      <span class="popup-calculate__tax">
        {{ separateThousands(tax) }}
        <span class="popup-calculate__year">
          {{ byYear(n) }}
        </span>
      </span>
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
    taxDeduction: {
      type: [Number, String],
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
      },
    };
  },

  methods: {
    byYear(year) {
      return `в ${year}${this.endings[year]} год`;
    },
    separateThousands(num) {
      return num.toString().replace(/\B(?=(\d{3})+(?!\d))/g, ' ');
    },
  },
};
</script>
