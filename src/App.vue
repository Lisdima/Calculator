<template lang="pug">
.section
  .section-left
    RangeInput(
      :sum="sum"
      :error="error"
      :time="time"
      @on-focus="clearRubles"
      @on-blur="addRubles"
      @changeValue="change")
    Options.options-block
  .section-right
    Payments(:sum="sum"
    :time="time")

</template>

<script>
import RangeInput from "./components/RangeInput.vue";
import Options from "./components/AdditionalOptions.vue";
import Payments from "./components/UnnualPayments.vue";

export default {
  name: "App",
  components: {
    RangeInput,
    Options,
    Payments,
  },
  data() {
    return {
      sum: "120 000 ₽",
      error: false,
      time: 5,
    };
  },
  methods: {
    clearRubles(value) {
      this.sum = value.replace(/[^\d]/g, "");
    },
    addRubles(value) {
      const currentValue = value.replace(/[^\d]/g, "");
      if (currentValue < 100000 || currentValue > 5000000) {
        this.error = true;
        this.sum = currentValue;
      } else {
        this.error = false;
        this.sum = `${currentValue.replace(/(\d)(?=(\d\d\d)+([^\d]|$))/g, "$1 ")} ₽`;
      }
    },
    change(value) {
      const currentValue = value.replace(/[^\d]/g, "");
      this.sum = currentValue
    },
  },
};
</script>

<style lang="scss">
.options-block {
  margin-top: 32px;
  @media (max-width: 640px) {
    display: none;
  }
}
</style>
