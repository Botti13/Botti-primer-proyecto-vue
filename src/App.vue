<script setup>
import { ref, computed } from 'vue';
const name = 'Vue Dinámico';
const counter = ref(0);
const colorRed = "color: red";
const colorGreen = "color: green";
const increment = () => {
  counter.value++;
};
const decrement = () => {
  counter.value--;
};
const reset = () => {
  counter.value = 0;
};

const classCounter = computed(() => {
  if(counter.value === 0){
    return 'zero';
  }
  if(counter.value > 0) {
    return 'positive';
  }
  if(counter.value < 0){
    return 'negative';
  }
});
const arrayNum = ref([]);
const addNum = () => {
  arrayNum.value.push(counter.value);
};

const bloquearBtnAdd = computed(() => {
  const numSearch = arrayNum.value.find(num => num === counter.value);
  console.log(numSearch);
  //if(numSearch === 0) return true;
  //return numSearch ? true : false;
  return numSearch || numSearch === 0;
})
</script>

<template>
  <div class="container text-center mt-3">
    <h1>Hola {{ name.toUpperCase() }}</h1>
  <h2 :class="classCounter">{{ counter }}</h2>
  <div class="btn-group">
    <button @click="increment" class="btn btn-success">Aumentar</button>
  <button @click="decrement" class="btn btn-danger">Disminuir</button>
  <button @click="reset" class="btn btn-sceondary">Reset</button>
  <button @click="addNum" :disabled="bloquearBtnAdd" class="btn btn-primary">Agregar</button>
  </div>
  
  <ul class="list-group mt-4">
    <li 
    class="list-group-item"
    v-for="(num, index) in arrayNum" 
    :key="index">
      {{num}}
    </li>
  </ul>
  </div>
 
 
</template>

<style>
h1 {
  color: red;
  
}
.positive {
  color: green;
}
.negative {
  color: red;
}
.zero {
  color: peru;
}
</style>