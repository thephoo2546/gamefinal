<script setup>
import { ref } from 'vue'

defineProps({
  msg: String,
})

const count = ref(0)
let name = ref('Piriya')

let isOn = ref(false)
const statusText = ref('ปิด')

const toggleButtonState = () => {
  isOn.value = !isOn.value;
  statusText.value = isOn.value ? 'เปิด' : 'ปิด';
}
</script>

<template>
  <h1>{{ msg }}</h1>
  <h2>{{ name }}</h2>

  <div class="card">
    <button id="toggleButton" @click="toggleButtonState" :class="{ 'red-button': isOn }">ON/OFF</button>
    <p id="status">{{ statusText }}</p>

    <button type="button" @click="count++" style="margin-top: 10px;" >count is {{ count }}</button>
    <p>
      Edit
      <code>components/HelloWorld.vue</code> to test HMR
    </p>
  </div>

  <p>
    Check out
    <a href="https://vuejs.org/guide/quick-start.html#local" target="_blank"
      >create-vue</a
    >, the official Vue + Vite starter
  </p>
  <p>
    Install
    <a href="https://github.com/vuejs/language-tools" target="_blank">Volar</a>
    in your IDE for a better DX
  </p>
  <p class="read-the-docs">Click on the Vite and Vue logos to learn more</p>
</template>

<style scoped>
.read-the-docs {
  color: #888;
}

h2{
  color: orange;
  font-size: 40px;
}

h1{
  color: blue;
  font-size: 40px;
}
.red-button {
  background-color: red;
  color: white;
}
</style>
