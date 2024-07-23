<script setup>
import { reactive, ref } from 'vue'

// Reactive object query - https://vuejs.org/guide/essentials/reactivity-fundamentals.html
const inputTerm = reactive({
  query: ''
})

// Reactive array to hold the list of to-do items
const toDoList = ref([])

// This function will take the data from input and post it to the list
const addToList = () => {
  if (inputTerm.query) {
    toDoList.value.push(inputTerm.query)
    clearInput()
  }
}

const removeFromList = (index) => {
  toDoList.value.splice(index, 1)
}

const clearInput = () => {
  inputTerm.query = ''
}
</script>

<template>
  <h1 class="text-4xl mb-3">Today's to do list:</h1>
  <ul>
    <li v-for="(item, index) in toDoList" :key="index">
      <div>
        {{ item }}
        <button @click="removeFromList(index)" class="border">remove</button>
      </div>
    </li>
  </ul>
  <div class="flex">
  
    <form @submit.prevent class="flex-grow">
      <div class="w-full">
        <input id="textInput" type="text" placeholder="Type here" class="bg-transparent w-3/4 text-4xl" v-model="inputTerm.query" />
      </div>
    </form>
    <button @click="addToList" ><i class="fa-solid fa-plus"></i></button>
  </div>

</template>

<style scoped>
li {
  font-size: 2em;
  border: solid white;
}
</style>
