<template lang="pug">
.payments-block
    .payments-block__title.title Ежегодные выплаты
    .payments-block__calculation
        .calculation-item.item
            .item-info
                span.item-info__time 1-й год
                span.item-info__bonus.best-bonus +{{checked ? Math.floor((currentSum * 0.30 + tax) / currentSum * 100) : Math.floor((currentSum * 0.30) / currentSum * 100)}}%
            span.item-money {{checked ? Math.floor(currentSum * 0.30 + tax) : Math.floor(currentSum * 0.30)}} ₽
        .calculation-item.item
            .item-info
                span.item-info__time 2-й год
                span.item-info__bonus +{{checked ? Math.floor((currentSum * 0.14 + tax) / currentSum * 100) : Math.floor((currentSum * 0.14) / currentSum * 100)}}%
            span.item-money {{checked ? Math.floor(currentSum * 0.14 + tax) : Math.floor(currentSum * 0.14)}} ₽
        .calculation-item.item
            .item-info
                span.item-info__time 3-й год
                span.item-info__bonus +{{checked ? Math.floor((currentSum * 0.08 + tax) / currentSum * 100) : Math.floor((currentSum * 0.08) / currentSum * 100)}}%
            span.item-money {{checked ? Math.floor(currentSum * 0.08 + tax) : Math.floor(currentSum * 0.08)}} ₽
        .calculation-item.item
            .item-info
                span.item-info__time 4-й год
                span.item-info__bonus +{{checked ? Math.floor((currentSum * 0.08 + tax) / currentSum * 100) : Math.floor((currentSum * 0.08) / currentSum * 100)}}%
            span.item-money {{checked ? Math.floor(currentSum * 0.08 + tax) : Math.floor(currentSum * 0.08)}} ₽
        .calculation-item.item
            .item-info
                span.item-info__time 5-й год
                span.item-info__bonus +{{checked ? Math.floor((currentSum * 0.08 + tax) / currentSum * 100) : Math.floor((currentSum * 0.08) / currentSum * 100)}}%
            span.item-money {{checked ? Math.floor(currentSum * 0.08 + tax) : Math.floor(currentSum * 0.08)}} ₽
        .calculation-item__opacity
    .dividing-line
    .block-deducation
        .deducation-checkbox
            label.block-checkbox.block-checkbox__deducation Получу налоговый вычет
                input(type="checkbox"
                v-model="checked"
                @change="chooseOption(checked)")
                span.checkmark
            .deducation-checkbox__description
                span +{{tax}} ₽ в год
                .deducation__question.question
                    p(@click.stop="$emit('onclick-tooltip-paymets')") ?
                    span(:class="{'tooltip-active': tooltipPayments}") Это возврат уплаченных вами в «казну» налогов.
                      a(href="#rec426212205")  Подробнее в ответах
        .deducation-total
            .deducation-total__name Взносы за {{time}} лет
            .deducation-total__sum {{(currentSum * time)}} ₽
    Options.deducation-options(
      :tooltipOptions="tooltipOptions"
      @onclick-tooltip-opts="$emit('onclick-tooltip-opts')")
    .payments-block__issue
      a(href="#popup:myform")
        button.btn.payments-block__btn(:disabled="disabled" :class="{'disabled': disabled}") Оформить

                     
</template>

<script>
import Options from "@/components/AdditionalOptions.vue";

export default {
  props: {
    sum: {
      type: String,
    },
    time: {
      type: Number,
    },
    tooltipPayments: {
      type: Boolean
    },
    tooltipOptions: Boolean,
  },
  components: {
    Options,
  },
  data() {
    return {
      bonus: 0,
      checked: false,
    };
  },
  methods: {
    chooseOption(value) {
      value === true ? (this.bonus = this.tax) : (this.bonus = 0);
      // Math.floor(this.bonus) > 15600 ? (this.bonus = 15600) : (this.bonus = Math.floor(this.bonus));
    },
  },
  computed: {
    disabled() {
      const sum = this.sum.replace(/\D/gi, "");
      if (sum < 100000 || sum > 5000000) {
        return true;
      }
      return false;
    },
    currentSum() {
      return this.sum.replace(/[^\d]/g, "");
    },
    profit(value) {
      if (value === 1) {
        return Math.floor(this.currentSum * 0.3 + this.tax);
      }
      if (value === 2) {
        return Math.floor(this.currentSum * 0.14 + this.tax);
      }
      return Math.floor(this.currentSum * 0.08 + this.tax);
    },
    tax() {
      let TAX = this.currentSum * 0.13;
      if (TAX >= 15600) {
        return (TAX = 15600);
      }
      return Math.floor(TAX);
    },
  },
};
</script>

<style lang="scss">
.payments-block {
  &__calculation {
    margin-top: 16px;
    display: flex;
    margin-bottom: 29px;
    @media (max-width: 960px) {
      flex-direction: column;
    }
    @media (max-width: 640px) {
      flex-direction: row;
      overflow-x: scroll;
      white-space: nowrap;
      &::-webkit-scrollbar {
        display: none;
      }
    }
    @media (max-width: 480px) {
      padding-right: 30px;
    }
    .calculation-item__opacity {
      display: none;
      @media (max-width: 480px) {
        display: block;
        position: absolute;
        right: 0;
        width: 40px;
        height: 50px;
        border-radius: 3px;
        background: #ffffff;
        opacity: 0.93;
      }
    }
  }
  .item {
    max-width: 98px;
    margin-right: 14px;
    &:last-child {
      margin-right: 0;
    }
  }
  .item-info {
    display: flex;
    align-items: baseline;
    &__time {
      font-size: 14px;
      line-height: 18px;
      font-weight: 300;
      margin-right: 10px;
    }
    &__bonus {
      padding: 2px 6px;
      font-size: 12px;
      background: #8c959e;
      color: #ffffff;
      border-radius: 24px;
      line-height: 14px;
    }
    .best-bonus {
      background: #0db089;
    }
  }
  &__issue {
    margin-top: 24px;
    .disabled {
      opacity: 0.8;
      &:hover {
        cursor: not-allowed;
      }
    }
  }
}
.block-deducation {
  display: flex;
  justify-content: space-between;
  align-items: center;
  @media (max-width: 960px) {
    flex-direction: column;
    align-items: flex-start;
  }
  @media (max-width: 640px) {
    flex-direction: row;
    align-items: center;
  }
  @media (max-width: 480px) {
    flex-direction: column;
    align-items: flex-start;
  }
  .deducation-checkbox {
    display: flex;
    @media (max-width: 960px) {
      flex-direction: column;
    }
    @media (max-width: 640px) {
      flex-direction: row;
    }
    @media (max-width: 480px) {
      flex-direction: column;
    }
    &__description {
      display: flex;
      font-weight: 300;
      color: #8c959e;
      font-size: 16px;
      line-height: 22px;
      margin-left: 8px;
      @media (max-width: 960px) {
        margin-left: 36px;
      }
      @media (max-width: 640px) {
        margin-left: 8px;
        font-size: 14px;
        line-height: 18px;
      }
      @media (max-width: 480px) {
        margin-left: 36px;
      }
    }
    .deducation__question {
      position: relative;
      margin-left: 8px;
      color: #28323c;
      .tooltip-active {
        a {
          color: #3E70BB
        }
        @media (max-width: 960px) {
          left: -500%;
        }
        @media (max-width: 640px) {
          left: -300%;
        }
      }
    }
  }
  .deducation-total {
    @media (max-width: 960px) {
      margin-top: 18px;
    }
    @media (max-width: 640px) {
      margin-top: 0;
    }
    @media (max-width: 480px) {
      margin-top: 20px;
    }
    &__name {
      font-size: 14px;
      line-height: 18px;
      font-weight: 300;
    }
  }
  .block-checkbox__deducation {
    margin-bottom: 0;
  }
}
.deducation-options {
  display: none;
  @media (max-width: 640px) {
    display: block;
    margin-top: 24px;
  }
}
</style>
