<template>
  <div class="calculator">
    <VDisplay :valor="displayValue"></VDisplay>
    <VButton label="AC" triple @onClick="clearMemory" />
    <VButton label="/" operation @onClick="setOperation" />
    <VButton label="7" @onClick="addDigit" />
    <VButton label="8" @onClick="addDigit" />
    <VButton label="9" @onClick="addDigit" />
    <VButton label="*" operation @onClick="setOperation" />
    <VButton label="4" @onClick="addDigit" />
    <VButton label="5" @onClick="addDigit" />
    <VButton label="6" @onClick="addDigit" />
    <VButton label="-" operation @onClick="setOperation" />
    <VButton label="1" @onClick="addDigit" />
    <VButton label="2" @onClick="addDigit" />
    <VButton label="3" @onClick="addDigit" />
    <VButton label="+" operation @onClick="setOperation" />
    <VButton label="0" double @onClick="addDigit" />
    <VButton label="." @onClick="addDigit" />
    <VButton label="=" operation @onClick="setOperation" />
  </div>
</template>

<script>
import VDisplay from "../components/Display.vue";
import VButton from "../components/Button.vue";

export default {

  data: function() {
    return {
      displayValue: "0",
      clearDisplay: false,
      operation: null,
      values: [0,0],
      current: 0
    }
  },
  name: "VCalculator",
  components: { VButton, VDisplay },

  methods: {
    clearMemory() {
      Object.assign(this.$data,this.$options.data())
    },
    setOperation(operation) {
      
    },
    addDigit(n) {
      if (n === "." && this.displayValue.includes(".")) {
        return
      }
  
      const clearDisplay = this.clearDisplay === "0" || this.clearDisplay

    },
  },
};
</script>

<style>
.calculator {
  height: 320px;
  width: 235px;
  border-radius: 5px;
  overflow: hidden;

  display: grid;
  grid-template-columns: repeat(4, 25%);
  grid-template-rows: 1fr 48px 48px 48px 48px 48px;
}
</style>