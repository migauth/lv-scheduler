<script setup>
import { reactive, ref, computed, onMounted, watch } from 'vue'
import { inputStyles } from '../state';

// Reactive object query - https://vuejs.org/guide/essentials/reactivity-fundamentals.html
const inputTerm = reactive({
  query: ''
})

// Reactive array to hold the list of to-do items
const toDoList = ref([])

// Load to-do list from localStorage on mount
onMounted(() => {
  const savedToDoList = localStorage.getItem('toDoList')
  console.log(savedToDoList);
  if (savedToDoList) {
    toDoList.value = JSON.parse(savedToDoList)
  }
})

// Watch toDoList and save changes to localStorage
watch(toDoList, (newList) => {
  localStorage.setItem('toDoList', JSON.stringify(newList))
}, { deep: true })

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

const inputClass = computed(() => {
  return `${inputStyles.value.width} ${inputStyles.value.border} ${inputStyles.value.background} ${inputStyles.value.rounded} ${inputStyles.value.placeholder} ${inputStyles.value.text} ${inputStyles.value.padding}`
})
</script>

<template>
  <div class="">
    <h1 class="text-4xl mb-3">Today's to do list:</h1>
    <ul>
      <li v-for="(item, index) in toDoList" :key="index">
        <div class="flex flex-col sm:flex-row mb-4">
          <button @click="removeFromList(index)" class="border rounded w-32 mr-4">
            <div class="hover:animate-wiggle">remove</div>
          </button>
          <div class="border w-full pl-2">
            ⦾
            {{ item }}
          </div>
        </div>
      </li>
    </ul>
    <div class="flex flex-col sm:flex-row">
      <div class="flex-shrink-0">
        <button @click="addToList" class="border rounded px-2 py-1 w-full sm:w-32 mb-2 sm:mb-0 sm:mr-2">
          Add item<i class="fa-solid fa-plus text-4xl hover:animate-jump"></i>
        </button>
      </div>
      <form @submit.prevent="addToList" class="flex-grow ml-2 sm:w-auto">
        <input id="textInput" type="text" placeholder="Type here" v-model="inputTerm.query" :class="inputClass" />
      </form>
    </div>
  </div>
</template>

<style scoped>
li {
  font-size: 2em;

}
</style>
