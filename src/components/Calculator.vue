<template>
  <div id="calculator">
    <div class="display">{{value || '0'}}</div>
    <div @click="clear" class="btn">C</div>
    <div @click="percent" class="btn">%</div>
    <div class="btn">^</div>
    <div @click="sign" class="btn operator">+/-</div>

    <div @click="append(7)" class="btn">7</div>
    <div @click="append(8)" class="btn">8</div>
    <div @click="append(9)" class="btn">9</div>
    <div @click="mul" class="btn operator">x</div>

    <div @click="append(4)" class="btn">4</div>
    <div @click="append(5)" class="btn">5</div>
    <div @click="append(6)" class="btn">6</div>
    <div @click="add" class="btn operator">+</div>

    <div @click="append(1)" class="btn">1</div>
    <div @click="append(2)" class="btn">2</div>
    <div @click="append(3)" class="btn">3</div>
    <div @click="sub" class="btn operator">-</div>

    <div @click="equal" class="btn">=</div>
    <div @click="append(0)" class="btn">0</div>
    <div @click="dot" class="btn">.</div>
    <div @click="divide" class="btn operator">/</div>
  </div>
</template>

<script>
export default {
  name: "#calculator",
  data() {
    return {
      previous: null,
      value: "",
      operator: null,
      operatorClicked: false
    };
  },
  methods: {
    clear() {
      this.value = "";
    },
    percent() {
      this.value = `${parseFloat(this.value / 100)}`;
    },
    sign() {
      this.value =
        this.value.charAt(0) === "-" ? this.value.slice(1) : `-${this.value}`;
    },
    dot() {
      if (this.value.indexOf(".") === "-1") {
        this.append(".");
      }
    },
    setPrevious() {
      this.previous = this.value;
      this.operatorClicked = true;
    },
    divide() {
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    mul() {
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    add() {
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    sub() {
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    equal() {
      this.value = `${this.operator(
        parseFloat(this.value),
        parseFloat(this.previous)
      )}`;
      this.previous = null;
    },
    append(num) {
      if (this.operatorClicked) {
        this.value = "";
        this.operatorClicked = false;
      }
      this.value = `${this.value}${num}`;
    }
  }
};
</script>

<style scoped>
#calculator {
  display: grid;
  width: 500px;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  margin: 10% auto;
  font-size: 2rem;
}
.btn {
  border: 1px solid #333;
  background-color: aliceblue;
  font-size: 2rem;
}
.display {
  grid-column: 1/5;
  background-color: #333;
  color: #ffffff;
  text-align: center;
}
.operator {
  background-color: tomato;
  color: white;
}
</style>