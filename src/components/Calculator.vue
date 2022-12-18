<script>

export default {
  data() {
    return {
      previous: null,
      previousOperator: null,
      current: '0',
      operator: null,
      operatorClicked: false,
      newcal: false,
    }
  },
  methods: {
    clear() {
      this.current = '0';
      this.previous = null;
      this.newcal = false;
    },
    sign() {
      this.current = (!this.current.includes('+') && !this.current.includes('x') && !this.current.includes('÷') && this.current.charAt(this.current.length - 1) !== '-')
        ? this.current.charAt(0) === '-' ? this.current.slice(1) : `-${this.current}`
        : !this.sign();
    },
    percent() {
      this.current = this.current.charAt(0) !== '' && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '') && !this.current.includes('+') && this.current.charAt(this.current.length - 1) !== '-' && !this.current.includes('÷') && !this.current.includes('x') && !this.current.includes('^')
        ? `${Math.round(10000000000 * (parseFloat(parseFloat(this.current) / 100))) / 10000000000}`
        : `${this.current}`;
      this.newcal = true;
    },
    append(number) {
      if (this.operatorClicked) {
        this.current = (number === '+' || number === '-' || number === '÷' || number === 'x' || number === '^') ?
          `${this.current}` : ''; //when operators were clicked, other operators do not work. If it is number, this.current is emptied
        this.operatorClicked = false;
      }
      this.current = (this.newcal) // new calculation starts
        ? (number === '+' || number === '-' || number === '÷' || number === 'x' || number === '^') // operators are clicked
          ? (`${this.current}${number}`) // the operators added to the current
          : (this.newcal = false, `${number}`) // when numeric value is clicked, new number alone is shown
        : ((this.current === '0' || this.current === '-0') && number !== '.' && number !== '+' && number !== '-' && number !== '÷' && number !== 'x' && number !== '^') // when the current is zero and takes new numbers except for dot 
          ? (number === '.' ? `${this.current}${number}` : `${number}`)
          : `${this.current}${number}`; // if not new calculation i.e. when program starts, input value is added to the current
      if (this.current === "00") this.current = '0';
      if (this.current === '-00') this.current = '-';
    },
    dot() {
      if (this.current.indexOf('.') === -1 && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '')) {
        this.append('.')
      }
    },
    del() {
      this.current = this.current.slice(0, -1);
    },
    setPrevious(name) { //to make continuous calcuation on previous results
      if (this.operator && this.previous) {
        this.current = `${Math.round(10000000000 * parseFloat(this.previousOperator(
          parseFloat(this.previous),
          parseFloat(this.current)
        ))) / 10000000000}${name}`;
        this.previous = this.current;
        this.newcal = true;
      } else {
        this.previous = this.current; //after clicking operator, the previous values are same as the current
      }
      this.operatorClicked = true;
    },
    logarithm() {
      this.current = this.current.charAt(0) !== '' && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '') && !this.current.includes('+') && this.current.charAt(this.current.length - 1) !== '-' && !this.current.includes('÷') && !this.current.includes('x') && !this.current.includes('^')
        ? `${Math.round(10000000000 * Math.log(parseFloat(this.current))) / 10000000000}`
        : `${this.current}`;
      this.newcal = true;
    },
    logarithm10() {
      this.current = this.current.charAt(0) !== '' && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '') && !this.current.includes('+') && this.current.charAt(this.current.length - 1) !== '-' && !this.current.includes('÷') && !this.current.includes('x') && !this.current.includes('^')
        ? `${Math.round(10000000000 * Math.log10(parseFloat(this.current))) / 10000000000}`
        : `${this.current}`;
      this.newcal = true;
    },
    sqrt() {
      this.current = this.current.charAt(0) !== '' && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '') && !this.current.includes('+') && this.current.charAt(this.current.length - 1) !== '-' && !this.current.includes('÷') && !this.current.includes('x') && !this.current.includes('^')
        ? `${Math.round(10000000000 * Math.sqrt(parseFloat(this.current))) / 10000000000}`
        : `${this.current}`;
      this.newcal = true;
    },
    cubert() {
      this.current = this.current.charAt(0) !== '' && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '') && !this.current.includes('+') && this.current.charAt(this.current.length - 1) !== '-' && !this.current.includes('÷') && !this.current.includes('x') && !this.current.includes('^')
        ? `${Math.round(10000000000 * Math.cbrt(parseFloat(this.current))) / 10000000000}`
        : `${this.current}`;
      this.newcal = true;
    },
    reciprocal() {
      this.current = this.current.charAt(0) !== '' && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '') && !this.current.includes('+') && this.current.charAt(this.current.length - 1) !== '-' && !this.current.includes('÷') && !this.current.includes('x') && !this.current.includes('^')
        ? `${Math.round(10000000000 / (parseFloat(this.current))) / 10000000000}`
        : `${this.current}`;
      this.newcal = true;
    },
    power2() {
      this.current = this.current.charAt(0) !== '' && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '') && !this.current.includes('+') && this.current.charAt(this.current.length - 1) !== '-' && !this.current.includes('÷') && !this.current.includes('x') && !this.current.includes('^')
        ? (`${Math.round(10000000000 * parseFloat(this.current * this.current)) / 10000000000}`)
        : `${this.current}`;
      this.newcal = true;
    },
    cubicX() {
      this.current = this.current.charAt(0) !== '' && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '') && !this.current.includes('+') && this.current.charAt(this.current.length - 1) !== '-' && !this.current.includes('÷') && !this.current.includes('x') && !this.current.includes('^')
        ? (`${Math.round(10000000000 * parseFloat(this.current * this.current * this.current)) / 10000000000}`)
        : `${this.current}`;
      this.newcal = true;
    },
    epowerX() {
      this.current = this.current.charAt(0) !== '' && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '') && !this.current.includes('+') && this.current.charAt(this.current.length - 1) !== '-' && !this.current.includes('÷') && !this.current.includes('x') && !this.current.includes('^')
        ? `${Math.round(10000000000 * parseFloat(Math.pow(2.7182818284590452353602874713527, this.current))) / 10000000000}`
        : `${this.current}`;
      this.newcal = true;
    },
    twopowerX() {
      this.current = this.current.charAt(0) !== '' && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '') && !this.current.includes('+') && this.current.charAt(this.current.length - 1) !== '-' && !this.current.includes('÷') && !this.current.includes('x') && !this.current.includes('^')
        ? `${Math.round(10000000000 * parseFloat(Math.pow(2, this.current))) / 10000000000}`
        : `${this.current}`;
      this.newcal = true;
    },
    tenpower() {
      this.current = this.current.charAt(0) !== '' && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '') && !this.current.includes('+') && this.current.charAt(this.current.length - 1) !== '-' && !this.current.includes('÷') && !this.current.includes('x') && !this.current.includes('^')
        ? `${Math.round(10000000000 * parseFloat(Math.pow(10, this.current))) / 10000000000}`
        : `${this.current}`;
      this.newcal = true;
    },
    factorialCal(n) {
      let outcome = 1;
      if (n === 0) {
        return outcome = 0;
      } else {
        for (let i = 1; i <= n; i++) {
          outcome *= i;
        }
        return outcome;
      }
    },
    factorial() {
      this.current = this.current.charAt(0) !== '' && this.current.charAt(0) !== '-' && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '') && !this.current.includes('+') && this.current.charAt(this.current.length - 1) !== '-' && !this.current.includes('÷') && !this.current.includes('x') && !this.current.includes('^') && (parseFloat(this.current) % 2 === 0 || parseFloat(this.current) % 2 === 1)
        ? `${Math.round(10000000000 * this.factorialCal(parseFloat(this.current))) / 10000000000}`
        : `${this.current}`;
      this.newcal = true;
    },
    naturalE() {
      this.current = this.current.charAt(0) !== '' && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '') ? '2.7182818284590452353602874713527' : '';
      this.newcal = true;
    },
    pi() {
      this.current = this.current.charAt(0) !== '' && !(this.current.charAt(0) === '-' && this.current.charAt(1) === '') ? '3.1415926535897932384626433832795' : '';
      this.newcal = true;
    },
    pow() {
      this.append(
        !this.current.includes('^') &&
          !this.current.includes('÷') &&
          !this.current.includes('x') &&
          this.current.charAt(this.current.length - 1) !== '+' &&
          this.current.charAt(this.current.length - 1) !== '-'
          ? '^' : this.current.operator = '')
      this.previousOperator = this.operator;
      this.operator = (a, b) => Math.pow(a, b);
      this.setPrevious('^');
    },
    divide() {
      this.append(
        !this.current.includes('^') &&
          !this.current.includes('÷') &&
          !this.current.includes('x') &&
          this.current.charAt(this.current.length - 1) !== '+' &&
          this.current.charAt(this.current.length - 1) !== '-'
          ? '÷' : this.current.operator = '')
      this.previousOperator = this.operator;
      this.operator = (a, b) => a / b;
      this.setPrevious('÷');
    },
    multiply() {
      this.append(
        !this.current.includes('^') &&
          !this.current.includes('÷') &&
          !this.current.includes('x') &&
          this.current.charAt(this.current.length - 1) !== '+' &&
          this.current.charAt(this.current.length - 1) !== '-'
          ? 'x' : this.current.operator = '')
      this.previousOperator = this.operator;
      this.operator = (a, b) => a * b;
      this.setPrevious('x');
    },
    add() {
      this.append(
        !this.current.includes('^') &&
          !this.current.includes('÷') &&
          !this.current.includes('x') &&
          this.current.charAt(this.current.length - 1) !== '+' &&
          this.current.charAt(this.current.length - 1) !== '-'
          ? '+' : this.current.operator = '')
      this.previousOperator = this.operator;
      this.operator = (a, b) => a + b;
      this.setPrevious('+');
    },
    subtract() {
      this.append(
        !this.current.includes('^') &&
          !this.current.includes('÷') &&
          !this.current.includes('x') &&
          this.current.charAt(this.current.length - 1) !== '+' &&
          this.current.charAt(this.current.length - 1) !== '-'
          ? '-' : this.current.operator = '')
      this.previousOperator = this.operator;
      this.operator = (a, b) => a - b;
      this.setPrevious('-');
    },
    equal() {
      if (this.previous) {
        this.current = `${Math.round(10000000000 * parseFloat(this.operator(
          parseFloat(this.previous),
          parseFloat(this.current)
        ))) / 10000000000}`;
        this.previous = null;
        this.newcal = true;
      }
    },
  }
}

</script>

<template>
  <div class="calculator">
    <div class="display">
      <div class="title">{{ "Calculator Created by MGK Since Dec 2022, ver 1.2.0" }}</div>
      <div class="previous-operand">{{ previous }}</div>
      <div :class="current.length >= 20
      ? current.length >= 26
        ? 'current-operandsmaller'
        : 'current-operandsmall'
      : 'current-operand'">{{ current || '0' }}</div>
    </div>
    <div @click="clear" class="btn function">&#119860&#119862</div> <!--AC-->
    <div @click="logarithm" class="btn function">&#119897&#119899</div> <!--ln-->
    <div @click="logarithm10" class="btn function">&#119897&#119900&#119892</div> <!--log-->
    <div @click="pow" class="btn function">&#119909<sup>&#119910</sup></div> <!--x^y-->
    <div @click="del" class="btn function">&#119889&#119890&#119897</div> <!--del-->
    <div @click="pi" class="btn function"><i>π</i></div>
    <div @click="naturalE" class="btn function">&#120358</div> <!--e-->
    <div @click="epowerX" class="btn function">&#120358<sup>&#119909</sup></div> <!--e^x-->
    <div @click="twopowerX" class="btn function">&#120804<sup>&#119909</sup></div> <!--2^x-->
    <div @click="tenpower" class="btn function">10<sup>&#119909</sup></div> <!--10^x-->
    <div @click="power2" class="btn function">&#119909&sup2</div> <!--x^2-->
    <div @click="cubicX" class="btn function">&#119909&#179</div> <!--x^3-->
    <div @click="sqrt" class="btn function"><i>&sup2√</i></div> <!--2√-->
    <div @click="cubert" class="btn function"><i>&#179√</i></div> <!--3√-->
    <div @click="divide" class="btn operator">&divide;</div>
    <div @click="percent" class="btn function"><i>%</i></div>
    <div @click="append('7')" class="btn">7</div>
    <div @click="append('8')" class="btn">8</div>
    <div @click="append('9')" class="btn">9</div>
    <div @click="multiply" class="btn operator">&times;</div>
    <div @click="sign" class="btn function"><i>+/–</i></div>
    <div @click="append('4')" class="btn">4</div>
    <div @click="append('5')" class="btn">5</div>
    <div @click="append('6')" class="btn">6</div>
    <div @click="subtract" class="btn operator">–</div>
    <div @click="factorial" class="btn function">&#119909!</div> <!--x!-->
    <div @click="append('1')" class="btn">1</div>
    <div @click="append('2')" class="btn">2</div>
    <div @click="append('3')" class="btn">3</div>
    <div @click="add" class="btn operator">+</div>
    <div @click="reciprocal" class="btn function">1⁄&#119909</div> <!--1/x-->
    <div @click="append('0')" class="btn">0</div>
    <div @click="append('00')" class="btn">00</div>
    <div @click="dot" class="btn">.</div>
    <div @click="equal" class="btn operator">=</div>
    <div class="comments">
      <p>{{ 'version 1.2.0 - enable new calculation by clicking operators' }}</p>
      <p>{{ 'version 1.1.0 - enable simple calculations' }}</p>
    </div>
  </div>
</template>

<style scoped>
.calculator {
  margin: 0 auto;
  width: 300px;
  font-size: 25px;
  border-radius: 7%;
  display: grid;
  background-color: black;
  border-color: yellowgreen;
  border-width: 20px;
  grid-template-columns: repeat(5, 1fr);
  grid-auto-rows: minmax(30px, auto);
  text-align: center;
}

.display {
  grid-row: 1 / 7;
  color: white;
  border-radius: 20%;
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

.display .title {
  color: rgba(255, 255, 255, .75);
  font-size: 0.7rem;
  font-style: italic;
  height: 10px;
}

.display .previous-operand {
  color: rgba(255, 255, 255, .75);
  font-size: 1.0rem;
  height: 25px;
}

.display .current-operand {
  color: white;
  font-size: 1.5rem;
  height: 40px;
}

.display .current-operandsmall {
  color: white;
  font-size: 1.0rem;
  height: 40px;
}

.display .current-operandsmaller {
  color: white;
  font-size: 0.6rem;
  height: 40px;
}

.calculator .comments {
  padding-top: 30px;
  grid-column: 1 / -1;
  color: rgba(255, 255, 255, .75);
  font-size: 1rem;
  color: black;
  font-style: italic;
  height: 10px;
}

.btn {
  cursor: pointer;
  background-color: rgb(43, 17, 17);
  color: rgb(164, 191, 249);
  border: 1.5px solid rgb(79, 78, 78);
  /* border-radius: 60%; */
  text-align: center;
  font-size: 2rem;
}

.btn:hover {
  background-color: white;
  color: black
}

.operator {
  background-color: rgb(31, 20, 0);
  color: white;
}

.operator:hover {
  background-color: white;
  color: rgb(31, 20, 0)
}

.function {
  background-color: rgb(1, 40, 46);
  color: white;
}

.function:hover {
  background-color: grey;
  color: black
}
</style>
