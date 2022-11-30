<script>

export default {
  data() {
    return {
      previous: null,
      current: '0',
      operator: null,
      operatorClicked: false,
      newcal: false,
    }
  },
  methods: {
    clear() {
      this.current = '0';
      this.newcal = false;
    },
    sign() {
      this.current = (!this.current.includes('+') && !this.current.includes('x') && !this.current.includes('÷') && this.current.charAt(this.current.length - 1) !== '-')
        ? this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`
        : !this.sign();
    },
    percent() {
      this.current = this.current.charAt(0) !== '' && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '') ? `${(parseFloat(parseFloat(this.current) / 100).toFixed(4))}` : '';
      this.newcal = true;
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = (number === '+' || number === '-' || number === '÷' || number === 'x') ?
        `${this.current}` : '';
        this.operatorClicked = false;
      }
      this.current = (this.newcal) // new calculation starts
        ? (number === '+' || number === '-' || number === '÷' || number === 'x') // operators are clicked
          ? (`${this.current}${number}`) // the operators added to the current
          : (this.newcal = false, `${number}`) // when numeric value is clicked, new number alone is shown
        : ((this.current === '0' || this.current === '-0') && number !== '.' && number !== '+' && number !== '-' && number !== '÷' && number !== 'x') // when the current is zero and takes new numbers except for dot 
          ? (number === '.' ? `${this.current}${number}` : `${number}`)
          : `${this.current}${number}`; // if not new calculation i.e. when program starts, input value is added to the current
      if (this.current === "00") this.current = '';  //prevent double zero from being in front
      if (this.current === '-00') this.current = '-';
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
      this.current = this.current.charAt(0) !== '' && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '') ? `${parseFloat(Math.log(this.current).toFixed(4))}` : '';
      this.newcal = true;
    },
    exponent() {
      this.current = this.current.charAt(0) !== '' && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '') ? `${parseFloat(Math.pow(this.current, 2).toFixed(4))}` : '';
      this.newcal = true;
    },
    sqrt() {
      this.current = this.current.charAt(0) !== '' && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '') ? `${parseFloat(Math.sqrt(this.current).toFixed(4))}` : '';
      this.newcal = true;
    },
    reciprocal() {
      this.current = this.current.charAt(0) !== '' && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '') ? (1/`${(parseFloat(this.current))}`).toFixed(4) : '';
      this.newcal = true;
    },
    cubicX() {
      this.current = this.current.charAt(0) !== '' && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '') ? (`${(parseFloat(this.current))}`*`${(parseFloat(this.current))}`*`${(parseFloat(this.current))}`).toFixed(2) : '';
      this.newcal = true;
    },
    factorialCal(n) {
      let outcome = 1;
      for (let i = 1; i <= n; i++) {
        outcome *= i;
      }
      return outcome;
    },
    factorial() {
      this.current = this.current.charAt(0) !== '' && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '') ? `${this.factorialCal(parseFloat(this.current)).toFixed(0)}` : '';
      this.newcal = true;
    },
    naturalE() {
      this.current = this.current.charAt(0) !== '' && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '') ? '2.71828' : '';
      this.newcal = true;
    },
    divide() {
      this.append(
        !this.current.includes('÷') &&
          !this.current.includes('x') &&
          !this.current.includes('+') &&
          this.current.charAt(this.current.length - 1) !== '-'
          ? '÷' : this.current.operator = null)
      this.operator = (a, b) => a / b;
      this.setPrevious();
    },
    multiply() {
      this.append(
        !this.current.includes('÷') &&
          !this.current.includes('x') &&
          !this.current.includes('+') &&
          this.current.charAt(this.current.length - 1) !== '-'
          ? 'x' : this.current.operator = null)
      this.operator = (a, b) => a * b;
      this.setPrevious();
    },
    add() {
      this.append(
        !this.current.includes('÷') &&
          !this.current.includes('x') &&
          !this.current.includes('+') &&
          this.current.charAt(this.current.length - 1) !== '-'
          ? '+' : this.current.operator = null)
      this.operator = (a, b) => a + b;
      this.setPrevious();
    },
    subtract() {
      this.append(
        !this.current.includes('÷') &&
          !this.current.includes('x') &&
          !this.current.includes('+') &&
          this.current.charAt(this.current.length - 1) !== '-'
          ? '-' : this.current.operator = null)
      this.operator = (a, b) => a - b;
      this.setPrevious();
    },
    equal() {
      this.current = `${parseFloat(this.operator(
        parseFloat(this.previous),
        parseFloat(this.current)
      ).toFixed((!this.previous.includes(".") && !this.current.includes("."))
        ? (this.divide && (parseFloat(this.previous) / parseFloat(this.current)) % 1 === 0)
          ? 0 : 4 : 4))}`;
      this.previous = null;
      this.newcal = true;
    },
  }
}

</script>

<template>
  <div class="calculator">
    <div class="display">
      <div class="previous-operand">{{ previous }}</div>
      <div class="current-operand">{{ current || '0' }}</div>
    </div>
    <div @click="clear" class="btn function">AC</div>
    <div @click="logarithm" class="btn function">Log</div>
    <div @click="exponent" class="btn function">Exp</div>
    <div @click="del" class="btn function">Del</div>
    <div @click="reciprocal" class="btn function">1/n</div>
    <div @click="cubicX" class="btn function">n&#179</div>
    <div @click="factorial" class="btn function">n!</div>
    <div @click="naturalE" class="btn function">e</div>
    <div @click="percent" class="btn function">%</div>
    <div @click="sign" class="btn function">+/–</div>
    <div @click="sqrt" class="btn function">√</div>
    <div @click="divide" class="btn operator">&divide;</div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="multiply" class="btn operator">&times;</div>
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

.function {
  background-color: powderblue;
  color: black;
}
</style>
