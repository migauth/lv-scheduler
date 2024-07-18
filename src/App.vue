<script setup>
import { computed, ref, onMounted, onUnmounted } from 'vue'
import { siteStyles } from './state.js'
import ToDoList from './components/ToDoList.vue';
import StyleButton from './components/StyleButton.vue';

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
const currentTime = ref(today.toLocaleTimeString('en-US', { hour: '2-digit', minute: '2-digit' }))

const updateClock = () => {
  const now = new Date()
  currentTime.value = now.toLocaleTimeString('en-US', { hour: '2-digit', minute: '2-digit' })
}

onMounted(() => {
  const interval = setInterval(updateClock, 1000)
  onUnmounted(() => {
    clearInterval(interval)
  })
})

</script>

<template>
  <main :class="siteClass" class="flex flex-col min-h-screen">
    <header :class="buttonClass" class="border text-6xl p-4">
      LV Scheduler
    </header>
    <div class="flex  justify-between mt-3 ">
        <!-- Colour buttons -->
        <button
        @click="toggleColorOptions"
        :class="buttonClass"
        class="rounded-md p-2 text-3xl sm:text-2xl mb-3 mr-0 sm:mr-3 w-full sm:w-auto "
      >
        <i class="fa-solid fa-caret-down" /> Color Options
      </button>
    <div v-if="showColorOptions" class="z-10 flex flex-wrap p-0 mb-4 animate-flip-down">
      <StyleButton></StyleButton>
    </div>
      <div class="text-4xl border  w-96">
        {{ dayOfWeek }}, {{ month }} {{ dayOfMonth }} - {{ currentTime }}
      </div>
    </div>
    <div class="flex-1 border p-4">
      <ToDoList />
    </div>
  </main>
</template>


<style scoped></style>
