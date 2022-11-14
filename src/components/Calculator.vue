<script>
export default {
  data() {
    return {
      current: '123', 
    }
  },
  methods: {
    clear() {
      this.current = '';
    }
  }
}
</script>

<template>
  <div class="calculator">
    <div class="display">{{current || '0'}}</div>
    <div @click="clear" class="btn">AC</div>
    <div class="btn">+/–</div>
    <div class="btn">%</div>
    <div class="btn operator">÷</div>
    <div class="btn">7</div>
    <div class="btn">8</div>
    <div class="btn">9</div>
    <div class="btn operator">x</div>
    <div class="btn">4</div>
    <div class="btn">5</div>
    <div class="btn">6</div>
    <div class="btn operator">–</div>
    <div class="btn">1</div>
    <div class="btn">2</div>
    <div class="btn">3</div>
    <div class="btn operator">+</div>
    <div class="btn zero">0</div>
    <div class="btn">.</div>
    <div class="btn operator">=</div>
  </div>
</template>

<style scoped>
.calculator {
  margin: 0 auto;
  width: 400px;
  font-size:50px;
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  grid-auto-rows: minmax(50px, auto);
}
.display {
  grid-column: 1 / 5;
  background-color: green;
  color: white;
  font-weight: bold;
  border-radius: 20%;
  text-align: right;
}

.zero {
  grid-column: 1 / 3;
}

.btn {
  background-color: #eee;
  border: 1px solid #333;
  border-radius: 30%;
  text-align: center;
}
.operator {
  background-color: orange;
  color: white;
}
</style>
