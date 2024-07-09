<script setup>
import { computed, ref } from 'vue'
import { siteStyles } from './state.js'
import ToDoList from './components/ToDoList.vue';

const siteClass = computed(() => {
  return `${siteStyles.value.padding} ${siteStyles.value.border} ${siteStyles.value.text} ${siteStyles.value.background} ${siteStyles.value.layout}`
})

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
    <div class="text-center text-lg my-4">
      {{ dayOfWeek }}, {{ month }} {{ dayOfMonth }} - {{ time }}
    </div>
    <div class="flex-1 border p-4">
      <ToDoList />
    </div>
  </main>
</template>


<style scoped>

</style>
