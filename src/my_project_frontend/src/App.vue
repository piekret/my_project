<script setup>
import { ref } from 'vue';
import { my_project_backend } from 'declarations/my_project_backend/index';
let chat = ref([]);

async function getChats() {
  chat.value = await my_project_backend.get_chat().then(response => chat.value = response)
}

async function handleSubmit(e) {
  e.preventDefault();
  const target = e.target
  const chats = target.querySelector('#name').value
  await my_project_backend.save_chat(chats)
  await getChats()
}

getChats()
</script>

<template>
  <main>
    <img src="/logo2.svg" alt="DFINITY logo" />
    <br />
    <br />
    <form action="#" @submit="handleSubmit">
      <label for="name">Enter your name: &nbsp;</label>
      <input id="name" alt="Name" type="text" />
      <button type="submit">Click Me!</button>
    </form>
    <section id="greeting">{{ chat }}</section>
  </main>
</template>
