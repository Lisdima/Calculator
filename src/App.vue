<template lang="pug">
.section
  .section-left
    RangeInput
    Options.options-block
  .section-right
    Payments

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
