<script setup>

</script>

<template>
  <h1 class="text-4xl">To do list component</h1>
  <form @submit.prevent>
    <div class="w-full">
      <input
        id="textInput"
        type="text"
        placeholder="Type here"
        
      />
    </div>
  </form>
</template>

<style scoped>
  li {
    font-size: 2em;
    border: solid white;
  }
</style>
