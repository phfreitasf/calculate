<template>
  <div class="calculator">
    <VDisplay v-bind:valor="displayValue" />
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
  data: function () {
    return {
      displayValue: "0",
      clearDisplay: true,
      operation: null,
      values: [0, 0, 0],
      current: 0,
      
    };
  },
  name: "VCalculator",
  components: { VButton, VDisplay },

  methods: {
    clearMemory() {
      Object.assign(this.$data, this.$options.data());
    },
    setOperation(operation) {
      if (this.current === 0) {
        this.operation = operation;
        this.current = 1;
        this.clearDisplay = true;
      } else {
        const equals = operation === "=";
        const currentOperation = this.operation;

        try {
          this.values[0] = eval(
            `${this.values[0]} ${currentOperation} ${this.values[1]}`
          );
        } catch (e) {
          this.$emit("onError", e);
        }

        this.values[1] = 0

        this.displayValue = this.values[0]
        this.operation = equals ? null : operation
        this.current = equals ? 0 : 1
        this.clearDisplay = !equals
      }
    },
    addDigit(n) {
      if (n === "." && this.displayValue.includes(".")) {
        return;
      }

      const clearDisplay = this.clearDisplay === "0" || this.clearDisplay;
      const currentValue = clearDisplay ? "" : this.displayValue;
      const displayValue = currentValue + n;

      this.displayValue = displayValue;
      this.clearDisplay = false;

      if (n !== ".") {
        const i = this.current;
        const newValue = parseFloat(displayValue);
        this.values[i] = newValue;
      }
    },


  },


  // mounted() {
  //   document
  //     .getElementById("app")
  //     .addEventListener("onkeydown", function (tecla) {
  //       this.addDigit(tecla.key);
  //     });
  // },
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