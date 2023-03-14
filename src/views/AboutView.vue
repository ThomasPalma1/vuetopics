<script setup lang="ts">
import { ref } from "vue";

const name = ref("name");

const counter = ref(1);

function increment(){
  counter.value++;
}

</script>
<template>
  <div class="about">
    <h1>Welcome {{ name }}</h1>
    <p><input type="text" v-model="name"></p>
    <p v-if="name.length">Full name</p>
    <p v-else>Short name</p>
    <p> {{ counter }} <button @click="increment">Increment!</button></p>
  </div>
</template>
