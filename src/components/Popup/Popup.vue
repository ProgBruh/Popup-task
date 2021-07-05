<template>
  <div class="popup">
    <div class="popup__window">
      <button class="popup__close" @click="close" />
      <div>
        <span class="popup__title"> Налоговый вычет </span>
        <p class="popup__text">
          Используйте налоговый вычет чтобы погасить ипотеку досрочно. Размер
          налогового вычета составляет не более 13% от своего официального
          годового дохода.
        </p>
        <Input
          label="Ваша зарплата в месяц"
          ref="input"
          placeholder="Введите данные"
          v-model="salary"
        />
        <TextButton
          class="popup__calculate-button"
          :class="{ 'popup__calculate-button--active': calculated }"
          @click.native="calculate"
          >Рассчитать</TextButton
        >
        <PopupCalculate :items="items" v-if="calculated" />
        <div class="popup__wrapper">
          <span class="popup__question"> Что уменьшаем? </span>
          <Tag active class="popup__tag">Платеж</Tag>
          <Tag>Срок</Tag>
        </div>
      </div>
      <Button size="big" class="popup__button">Добавить</Button>
    </div>
  </div>
</template>

<script>
import Input from '~/components/Input/Input.vue';
import TextButton from '~/components/TextButton/TextButton.vue';
import Tag from '~/components/Tag/Tag.vue';
import Button from '~/components/Button/Button.vue';
import PopupCalculate from '~/components/PopupCalculate/PopupCalculate.vue';
import IMask from 'imask';

export default {
  name: 'Popup',

  components: {
    Input,
    TextButton,
    Tag,
    Button,
    PopupCalculate,
  },

  data() {
    return {
      salary: null,
      taxDeduction: null,
      calculated: false,
      items: [],
    };
  },

  methods: {
    close() {
      this.$emit('close');
    },
    calculate() {
      if (!this.salary) {
        return;
      }
      this.items = [];
      const border = 260000;
      const salary = this.salary.includes('₽')
        ? parseInt(this.salary.replace(/\s+/g, '').slice(0, -1))
        : parseInt(this.salary);
      const taxDeduction = salary * 12 * 0.13;
      let remainder;
      if (taxDeduction < border) {
        const count = parseInt(border / taxDeduction);
        for (let i = 0; i < count; i++) {
          this.items.push(taxDeduction);
        }
        remainder = border % taxDeduction;
      } else {
        remainder = border;
      }
      this.items.push(remainder);
      this.calculated = true;
    },
  },

  mounted() {
    IMask(this.$refs.input.$refs.field, {
      mask: [
        { mask: '' },
        {
          mask: 'num ₽',
          lazy: false,
          blocks: {
            num: {
              mask: Number,
              thousandsSeparator: ' ',
            },
          },
        },
      ],
    });
  },
};
</script>
