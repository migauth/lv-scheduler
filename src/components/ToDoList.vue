<script setup>
import { computed, reactive, watch, defineEmits } from 'vue'

const post = () => {
  console.log(searchTerm.query);
}

const searchTerm = reactive({
  query: ''
})

const emit = defineEmits(['update:query'])

watch(searchTerm, (newVal) => {
  emit('update:query', newVal.query)
})

const clearInput = () => {
  searchTerm.query = ''
}
</script>

<template>
  <h1 class="text-4xl">To do list component</h1>
  <div class="border flex">
    <form @submit.prevent>
      <div class="w-full">
        <input id="textInput" type="text" placeholder="Type here" class=" bg-transparent" v-model="searchTerm.query" />
      </div>
    </form>
    <button @click="post" ><i class="fa-solid fa-plus"></i></button>
    
  </div>
</template>

<style scoped>
li {
  font-size: 2em;
  border: solid white;
}
</style>
