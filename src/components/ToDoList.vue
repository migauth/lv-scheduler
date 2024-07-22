<script setup>
import { computed, reactive, watch, defineEmits } from 'vue'

// Reactive object query - https://vuejs.org/guide/essentials/reactivity-fundamentals.html
const inputTerm = reactive({
  query: ''
})

const toDoContent = reactive({
  content: ''
})

// This function will take the data from input and post it to the list
const post = (text) => {
  console.log(inputTerm.query);
  if (text) {
    toDoContent.content = inputTerm.query
  }
}

// const emit = defineEmits(['update:query'])

// watch(inputTerm, (newVal) => {
//   emit('update:query', newVal.query)
// })

// Clears the input field

const clearInput = () => {
  inputTerm.query = ''
}
</script>

<template>
  <h1 class="text-4xl">To do list component</h1>
  <div class="border flex">
    <form @submit.prevent>
      <div class="w-full">
        <input id="textInput" type="text" placeholder="Type here" class=" bg-transparent" v-model="inputTerm.query" />
      </div>
    </form>
    <button @click="post(inputTerm.query)" ><i class="fa-solid fa-plus"></i></button>
  </div>
  <div >
    {{ toDoContent.content }}
  </div>
</template>

<style scoped>
li {
  font-size: 2em;
  border: solid white;
}
</style>
