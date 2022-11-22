<script>

export default {
  data() {
    return {
      previous: null,
      current: '',
      operator: null,
      operatorClicked: false,
    }
  },
  methods: {
    clear() {
      this.current = '';
    },
    sign() {
      this.current = this.current.charAt(0) === '-' ?
        this.current.slice(1) : `-${this.current}`;
    },
    percent() {
      this.current = this.current.charAt(0) !== '' && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '') ? `${(parseFloat(this.current) / 100).toFixed(2)}` : '';
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = '';
        this.operatorClicked = false;
      }
      this.current = `${this.current}${number}`;
      if (this.current === "00") this.current = '';  //prevent double zero from being in front
      if (this.current === '-00') this.current = '-';
      if (this.current === "0") this.current = '';   //prevent zero from being in front
    },
    dot() {
      if (this.current.indexOf('.') === -1 && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '')) {
        this.append(this.current === '' ? '0.' : '.');
      }
    },
    del() {
      this.current = this.current.slice(0, -1);
    },
    setPrevious() {
      this.previous = this.current;
      this.operatorClicked = true;
    },
    logarithm() {
      this.current = this.current.charAt(0) !== '' && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '') ? `${Math.log(this.current).toFixed(2)}` : '';
    },
    exponent() {
      this.current = this.current.charAt(0) !== '' && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '') ? `${Math.pow(this.current, 2).toFixed(2)}` : '';
    },
    sqrt() {
      this.current = this.current.charAt(0) !== '' && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '') ? `${Math.sqrt(this.current).toFixed(2)}` : '';
    },
    divide() {
      this.current.charAt(0) !== ''
        ? this.append(
          !this.current.includes('÷') &&
            !this.current.includes('x') &&
            !this.current.includes('+') &&
            !this.current.includes('-')
            ? '÷' : this.current.operator = null)
        : this.append('')
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    multiply() {
      this.current.charAt(0) !== ''
        ? this.append(
          !this.current.includes('÷') &&
            !this.current.includes('x') &&
            !this.current.includes('+') &&
            !this.current.includes('-')
            ? 'x' : this.current.operator = null)
        : this.append('')
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    add() {
      this.current.charAt(0) !== ''
        ? this.append(
          !this.current.includes('÷') &&
            !this.current.includes('x') &&
            !this.current.includes('+') &&
            !this.current.includes('-')
            ? '+' : this.current.operator = null)
        : this.append('')
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    subtract() {
      this.current.charAt(0) !== ''
        ? this.append(
          !this.current.includes('÷') &&
            !this.current.includes('x') &&
            !this.current.includes('+') &&
            !this.current.includes('-')
            ? '-' : this.current.operator = null)
        : this.append('')
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    equal() {
      this.current = `${this.operator(
        parseFloat(this.previous),
        parseFloat(this.current)
      ).toFixed((!this.previous.includes(".") && !this.current.includes("."))
        ? (this.divide && (parseFloat(this.previous) / parseFloat(this.current)) % 1 === 0)
          ? 0 : 2 : 2)}`;
      this.previous = null;
    },
  }
}

</script>

<template>
  <div class="calculator">
    <div class="display">
      <div class="previous-operand">{{ previous }}</div>
      <div class="current-operand">{{ current || 'Enter Your Number' }}</div>
    </div>
    <div @click="clear" class="btn">AC</div>
    <div @click="logarithm" class="btn">Log</div>
    <div @click="exponent" class="btn">Exp</div>
    <div @click="del" class="btn">Del</div>
    <div @click="percent" class="btn">%</div>
    <div @click="sign" class="btn">+/–</div>
    <div @click="sqrt" class="btn">√</div>
    <div @click="divide" class="btn operator">÷</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="multiply" class="btn operator">x</div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="subtract" class="btn operator">–</div>
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="append('0')" class="btn">0</div>
    <div @click="append('00')" class="btn">00</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
  </div>
</template>

<style scoped>
.calculator {
  margin: 0 auto;
  width: 400px;
  font-size: 50px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
  text-align: center;
}

.display {
  grid-row: 1 / 5;
  color: white;
  border-radius: 5%;
  grid-column: 1 / -1;
  background-color: rgba(0, 0, 0, .75);
  display: flex;
  align-items: flex-end;
  justify-content: space-around;
  flex-direction: column;
  padding: 10px;
  word-wrap: break-word;
  word-break: break-all;
}

.display .previous-operand {
  color: rgba(255, 255, 255, .75);
  font-size: 1.5rem;
}

.display .current-operand {
  color: white;
  font-size: 2.5rem;
}

.btn {
  cursor: pointer;
  background-color: #eee;
  border: 1px solid #333;
  border-radius: 30%;
  text-align: center;
}

.btn:hover {
  background-color: rgba(255, 255, 255, .9);
}

.operator {
  background-color: orange;
  color: black;
}
</style>
