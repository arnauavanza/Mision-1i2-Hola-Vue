<script setup lang="ts">
function changeName() {
  let name: string = "Arnau"
  let welcome : string = "Hola, " + name + "!"
  let element = document.getElementById("welcome")
  element.textContent = welcome
}
</script>

<template>
  <h1 id="welcome">Hola, usuario!</h1>
  <button v-on:click="changeName()">Actualizar nombre</button>
</template>