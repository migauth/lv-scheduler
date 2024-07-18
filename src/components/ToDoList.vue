<script setup>

</script>

<template>
  <h1 class="text-4xl">To do list component</h1>
  <div class="border flex">
    <form @submit.prevent>
      <div class="w-full">
        <input id="textInput" type="text" placeholder="Type here" class=" bg-transparent" />
      </div>
    </form>
    <button><i class="fa-solid fa-plus"></i></button>
    
  </div>
</template>

<style scoped>
li {
  font-size: 2em;
  border: solid white;
}
</style>
