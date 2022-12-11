<script setup>
  import {ref,computed} from 'vue'

  const name  = "dynamic vue"
  const counter = ref(0)
  const favoritesArray = ref([])

  const increment = () => counter.value++
  const decrement = () => counter.value--
  const resetCounter = () => counter.value = 0
  const add = () => {
    favoritesArray.value.push(counter.value)
  }

  const blockAddBtn = computed(() => {
    const numSearch = favoritesArray.value.find(num => num === counter.value)
    return numSearch || numSearch === 0
  })

  const classCounter = computed(() => {
    if(counter.value === 0){
      return 'zero'
    }else if (counter.value > 0){
      return 'positive'
    }else{
      return 'negative'
    }
  })
</script>

<template>
  <div class="container text-center mt-3">
    <h1>HELLO {{name.toUpperCase()}}</h1>
    <h2 :class="classCounter">{{counter}}</h2>
    <div class="btn-group">
      <button @click="increment" class="btn btn-success">Increase</button>
      <button @click="decrement" class="btn btn-danger">Decrease</button>
      <button @click="resetCounter" class="btn btn-secondary">Reset</button>
      <button @click="add" :disabled="blockAddBtn" class="btn btn-primary">Add</button>
    </div>
    <br>
    <ul class="list-group mt-4">
      <li
          class="list-group-item"
          v-for="(num,index) in favoritesArray" :key="index"
      >
        {{num}}
      </li>
    </ul>
  </div>
</template>

<style>
  .positive{
    color: green;
  }
  .negative{
    color: red
  }
  .zero{
    color: tan;
  }
</style>