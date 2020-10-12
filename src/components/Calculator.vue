<template>
  <div class="body">
    <div class="body__prev_area">{{ prev || '' }}</div>
    <div class="body__result_area">{{ current || 'нулл' }}</div>
    <div class="body__buttons">
      <div class="body__button-symbol" @click="clear">AC</div>
      <div class="body__button-symbol" @click="revert">+/-</div>
      <div class="body__button-symbol" @click="sign('sqrt')">скврт</div>
      <div class="body__button-symbol" @click="sign('-')">-</div>
      <div class="body__button-number" @click="append(7)">7</div>
      <div class="body__button-number" @click="append(8)">8</div>
      <div class="body__button-number" @click="append(9)">9</div>
      <div class="body__button-symbol" @click="sign('%')">%</div>
      <div class="body__button-number" @click="append(4)">4</div>
      <div class="body__button-number" @click="append(5)">5</div>
      <div class="body__button-number" @click="append(6)">6</div>
      <div class="body__button-symbol" @click="sign('+')">+</div>
      <div class="body__button-number" @click="append(1)">1</div>
      <div class="body__button-number" @click="append(2)">2</div>
      <div class="body__button-number" @click="append(3)">3</div>
      <div class="body__button-symbol" @click="sign('*')">*</div>
      <div class="body__button-number" @click="append(0)">0</div>
      <div class="body__button-symbol" @click="dot">тчк</div>
      <div class="body__button-symbol" @click="calculate">=</div>
      <div class="body__button-symbol" @click="sign('/')">/</div>
    </div>
  </div>
</template>

<script>
export default {
  name: "Calculator.vue",
  data() {
    return {
      result: 0,
      current: "",
      operation: "",
      prev: ""
    }
  },
  methods: {
    clear() {
      this.result = 0;
      this.current = "";
      this.operation = "";
      this.prev = " ";
    },
    append(number) {
      if (this.current !== "0") {
        this.current = `${this.current}${number}`;
        this.prev += number;
      }
      if (this.operation === "=") {
        this.current = `${number}`;
        this.result = "";
        this.operation = "";
      }
    },
    dot() {
      if (this.current.indexOf('.') === (-1)) {
          this.current = `${this.current}.`;
          this.prev += '.';
        }
    },
    calculate() {
      this.compute("=");
    },
    compute(symbol) {
      this.result = parseFloat(this.result);
      this.current = parseFloat(this.current);
      switch (this.operation) {
        case "sqrt":
          this.prev = "";
          this.result = Math.sqrt(this.current);
          break;
        case "%":
          this.prev = "";
          this.result = this.current / 100;
          break;
        case "-":
          this.result = this.result - this.current;
          break;
        case "+":
          this.result = this.result + this.current;
          break;
        case "*":
          this.result = this.result * this.current;
          break;
        case "/":
          this.result = this.result / this.current;
          break;
        case "=":
          this.current = this.result;
          break;
      }
      this.operation = symbol;
      this.current = this.result;
    },
    revert() {
      this.current = parseFloat(this.current) * (-1);
    },
    sign(symbol) {
      this.prev += ' ' + symbol + ' ';
      if (symbol === "%" || symbol === "sqrt") {
        this.operation = symbol;
        this.compute(symbol);
        this.operation = "";
      } else if (!this.operation || this.operation === "=") {
        this.result = this.current;
        this.current = "";
        this.operation = symbol;
      } else {
        this.compute(symbol);
      }
    }
  }
}
</script>

<style lang="scss">
@mixin button-style($width:7vh,  $fontSize: 1.2em, $background: transparent) {
  display: flex;
  justify-content: center;
  align-items: center;

  width: $width;

  height: 7vh;
  margin: 0.5vh;

  font-size: $fontSize;
  font-weight: 600;
  color:#DADBDE ;

  border-radius: 50%;
  background-color: $background;
}

.body {
  width: 35vh;
  height: 45vh;

  margin: auto auto;
  padding: 5vh 1vh;

  border: 1px solid black;
  border-radius: 20px;
  background-color: rgb(28,28,30);

  &__result_area {
    width: 95%;
    height: 3vh;
    position: relative;
    margin-bottom: 3vh;

    font-size: 1.7em;
    font-weight: 400;

    color: #DADBDE;
    text-align: end;
  }
  &__result_area:after {
    position: absolute;
    top: 4.5vh;
    right: -0.5vh;
    content: "";
    width: 95%;
    height: 1.25px;
    background-image: linear-gradient(0.25turn,
      rgb(94,92,230), rgb(255,55,95));
  }

  &__prev_area {
    width: 95%;
    height: 3vh;

    font-size: 1.3em;
    color: #4c4e52;
    text-align: end;
  }
}
.body {
  &__buttons {
    display: flex;
    flex-wrap: wrap;
    justify-content: center;
    cursor: pointer;
  }
  &__button {
    @media (min-height: 890px) {
      &-number {
        @include button-style(7vh, 1.5em);
      }
      &-symbol {
        @include button-style(7vh, 1.2em, rgb(99,99,102));
      }
    }
    @media (max-height: 870px) {
      &-number {
        @include button-style(7vh, 1em);
      }
      &-symbol {
        @include button-style(7vh, 0.8em, rgb(99,99,102));
      }
    }
  }
  &__button:hover {
    cursor: pointer;
  }
}
</style>
