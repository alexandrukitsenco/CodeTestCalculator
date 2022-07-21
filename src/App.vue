<template>
  <div class="main">
    <div class="output">{{ calculatorValue || 0 }}</div>
    <div class="buttons">
      <div
        class="button"
        v-for="n in btnArr"
        :key="n"
        :class="{ operator: ['C', '<=', '*', '/', '-', '+', '='].includes(n) }"
        >
        <div class="btn" @click="action(n)">
          {{ n }}
        </div>
      </div>
    </div>
  </div>
  
</template>

<script>
export default {
  data() {
    return {
      calculatorValue: "",
      btnArr: [
        "C",
        "<=",
        "*",
        "/",
        "7",
        "8",
        "9",
        "-",
        "4",
        "5",
        "6",
        "+",
        "1",
        "2",
        "3",
        "=",
        "0",
        ".",
      ],
      operator: null,
      previousCalculatorValue: ""
    }
  },
  methods: {
    action(n) {
      /* Append value */
      if (!isNaN(n) || n === ".") {
        this.calculatorValue += n + "";
      }
      /* Clear value */
      if (n === "C") {
        this.calculatorValue = "";
      }
      /* Substract */
      if (n === "<=") {
        this.calculatorValue = this.calculatorValue.slice(0, -1);
      }
      /* Operators */
      if (["/", "*", "-", "+"].includes(n)) {
        this.operator = n;
        this.previousCalculatorValue = this.calculatorValue;
        this.calculatorValue = "";
      }
      /* Calculate result using the eval function */
      if (n === "=") {
        this.calculatorValue = eval(
          this.previousCalculatorValue + this.operator + this.calculatorValue
        );
        this.previousCalculatorValue = "";
        this.operator = null;
      }
    },
  }
}
</script>

<style scoped>
@import url('http://fonts.cdnfonts.com/css/stencil-pixel-7');
.output {
  font-family: 'Stencil Pixel-7', sans-serif;
  color: green;
  background-color: rgb(109, 164, 121);
  border: 10px solid rgb(36, 81, 109);
  font-size: 40px;
  margin: 5px auto;
  padding: 5px;
  text-align: right;
  width: min(300px, 70%);
  border-radius: 3px;
}
.buttons {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  width: min(300px, 70%);
  border: 12px solid rgb(36, 81, 109);
  border-radius: 4px;
  align-items: center;
  background-color: rgb(177, 176, 176);
  justify-content: center;
  margin: 10px auto;
  padding: 5px;
  gap: 5px;
}
.button {
  font-family: sans-serif;
  color: black;
  background-color: rgb(231, 231, 231);
  padding: 6px;
  border-radius: 3px;
  margin: 4px;
  font-size: 1.5em;
  font-weight: bold;
  text-align: center;
  cursor: pointer;
  transition: all 0.2s ease-in-out;
}
.button:hover {
  background-color: rgb(108, 108, 108);
}
.operator {
  background-color: rgb(18, 68, 98);
}
.operator:hover {
  background-color: rgb(108, 177, 194);
}
</style>
