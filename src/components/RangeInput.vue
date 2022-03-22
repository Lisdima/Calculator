<template lang="pug">
.calculator
  .calculator--form
      h4.calculator--form__title.title Ежегодный взнос
      input#range-input(
        v-model="sum"
      )
      p.calculator__sub-title.sub-title от 100 000 ₽
  .calculator--info
    h4.info-title.title Срок программы
    .info-time
      p 5 лет

</template>

<script>
export default {
  data() {
    return {
      sum: "120 000 ₽",
    };
  },
  methods: {
    test() {
      console.log("Логика работает");
    },
  },
};
</script>

<style lang="scss">
.calculator {
  max-width: 512px;
  width: 100%;
  @media (max-width: 1200px) {
    max-width: 266px;
  }
  @media (max-width: 640px) {
    display: flex;
    max-width: none;
  }

  &--form {
    width: 100%;
    margin-bottom: 32px;
    @media (max-width: 640px) {
      width: 47%;
    }
    p {
      margin-top: 4px;
    }
  }
  &--form__title {
    margin-bottom: 4px;
  }
  &__subtitle {
    margin-top: 4px;
  }
  &--info {
    @media (max-width: 640px) {
      margin-left: 32px;
    }
    .info-time {
      margin-top: 6px;
    }
    p {
      font-size: 16px;
      line-height: 24px;
      max-width: 71px;
      border-radius: 6px;
      box-sizing: border-box;
      padding: 5px 6px 6px 15px;
      background: #28323c;
      color: #ffffff;
    }
  }
}
</style>
