<template>
  <div class="about">
    <h1>Welcome {{ name }}</h1>
    <p><input type="text" v-model="name" /></p>
    <p><input type="password" v-model="password" /></p>
    <button @click="cadastrar">Register</button>
    <p v-if="name.length > 5">Full Name</p>
    <p v-else>Short name</p>
    <p>{{ counter }} <button @click="incrementar">Incrementar</button></p>
    <button @click="update">Update</button>
    <p v-if="error">{{ error }}</p>
    <table>
      <thead>
        <td>ID</td>
        <td>Name</td>
      </thead>
      <tr v-for="user in users" :key="user.id">
        <td>{{ user.id }}</td>
        <td>{{ user.name }}</td>
      </tr>
    </table>
  </div>
</template>

<script setup lang="ts">
import { ref, onMounted } from "vue";
import axios from "axios";
const name = ref("Name");
const password = ref("123");
const counter = ref(1);
const users = ref();
const error = ref("");
function incrementar() {
  counter.value++;
}
async function update() {
  try {
    users.value = (await axios.get("user")).data;
    error.value = "";
  } catch (ex) {
    error.value = (ex as Error).message;
  }
}
async function cadastrar() {
  try {
    await axios.post("user", {
      name: name.value,
      password: password.value,
    });
    error.value = "";
    update();
  } catch (ex) {
    error.value = (ex as Error).message;
  }
}
onMounted(() => {
  update();
});
</script>
