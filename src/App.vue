<script setup>
import { computed, ref } from 'vue'
import { siteStyles } from './state.js'
import ToDoList from './components/ToDoList.vue';

const siteClass = computed(() => {
  return `${siteStyles.value.padding} ${siteStyles.value.border} ${siteStyles.value.text} ${siteStyles.value.background} ${siteStyles.value.layout}`
})

</script>

<template>
  <main :class="siteClass">
    
    <header class="  border text-6xl">
      LV Scheduler
    </header>
    <ToDoList/>
  </main>
</template>

<style scoped>

</style>
