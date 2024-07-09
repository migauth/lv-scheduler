<script setup>
import { computed, ref } from 'vue'
import { siteStyles } from './state.js'
import ToDoList from './components/ToDoList.vue';

// Site styles

const siteClass = computed(() => {
  return `${siteStyles.value.padding} ${siteStyles.value.border} ${siteStyles.value.text} ${siteStyles.value.background} ${siteStyles.value.layout}`
})

// Colour buttons

const showColorOptions = ref(false)

const toggleColorOptions = () => {
  showColorOptions.value = !showColorOptions.value
}

const buttonClass = computed(() => {
  return `${siteStyles.value.border} ${siteStyles.value.text} ${siteStyles.value.text} ${siteStyles.value.padding}`
})

// Date stuff

const daysOfWeek = ['Sunday', 'Monday', 'Tuesday', 'Wednesday', 'Thursday', 'Friday', 'Saturday']

const today = new Date();

const dayOfWeek = today.toLocaleDateString('en-US', { weekday: 'long' });
const month = today.toLocaleDateString('en-US', { month: 'long' });
const dayOfMonth = today.getDate();
const time = today.toLocaleTimeString('en-US');


</script>

<template>
  <main :class="siteClass" class="flex flex-col min-h-screen">
    <header class="border text-6xl p-4">
      LV Scheduler
    </header>
    <div class="flex  justify-between mt-3">
      <button @click="toggleColorOptions" :class="buttonClass"
        class="rounded-md p-2 text-3xl sm:text-2xl mb-3 mr-0 sm:mr-3 w-full sm:w-auto">
        <i class="fa-solid fa-caret-down" /> Color Options
      </button>
      <div class="text-3xl">
        {{ dayOfWeek }}, {{ month }} {{ dayOfMonth }} - {{ time }}
      </div>
    </div>
    <div class="flex-1 border p-4">
      <ToDoList />
    </div>
  </main>
</template>


<style scoped></style>
