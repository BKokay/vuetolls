<script setup>
import {ref, watch} from 'vue'
const input = ref('')
const transformedInput = ref(null)

watch(input, (newValue, oldValue) => {
  console.log(`watch: old value was ${oldValue} and new value is ${newValue}`)
})

const transform = (inputData) => {
  transformedInput.value = inputData * 2
}
</script>

<template>
  <div class="container">
    <h1>Quizes</h1>
    <input type="text" v-model="input" @blur="transform(input)">
    <h5> {{input}}</h5>
    <h5> {{transformedInput }}</h5>
    <div class="cards-container">

    </div>
  </div>
</template>

<style scoped>
.container{
  max-width: 1000px;
  margin: 0 auto;
}
header{
  margin-bottom: 10px;
  margin-top: 30px;
  display: flex;
  align-items: center;
}
header h1 {
  font-weight: bold;
  margin-right: 30px;
}
input {
  border: none;
  background-color: aliceblue;
  padding: 10px;
  border-radius: 5px;
}
</style>