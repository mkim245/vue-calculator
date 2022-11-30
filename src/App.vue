<script setup>
// import { RouterLink, RouterView } from 'vue-router'
import Calculator from './components/Calculator.vue'
</script>

<template>
  <header>
    <div class="wrapper">
      <Calculator />
    </div>
  </header>
  <!-- <RouterView /> -->
</template>

<style scoped>
  header .wrapper {
    display: flex;
    place-items: flex-start;
    flex-wrap: wrap;
  }

</style>
