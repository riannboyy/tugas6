<script setup>
import { ref } from "vue";

const dataCallback = ref([]);
const dataPromise = ref([]);
const dataAsync = ref([]);

function getDataCallback(callback) {
  setTimeout(() => {
    const result = " Data Callback";
    console.log(result);
    callback(result);
  }, 2000);
}

function handleCallback() {
  const loadingText = " Mengambil data (Callback)...";
  console.log(loadingText);
  dataCallback.value.push(loadingText);
  getDataCallback((result) => {
    dataCallback.value[dataCallback.value.length - 1] = result;
  });
}

function getDataPromise() {
  return new Promise((resolve) => {
    setTimeout(() => {
      const result = " Data Promise";
      console.log(result);
      resolve(result);
    }, 2000);
  });
}

function handlePromise() {
  const loadingText = " Mengambil data (Promise)...";
  console.log(loadingText);
  dataPromise.value.push(loadingText);
  getDataPromise().then((result) => {
    dataPromise.value[dataPromise.value.length - 1] = result;
  });
}

async function handleAsync() {
  const loadingText = " Mengambil data (Async/Await)...";
  console.log(loadingText);
  dataAsync.value.push(loadingText);
  const result = await getDataPromise();
  dataAsync.value[dataAsync.value.length - 1] = result;
}
</script>

<template>
  <div>
    <button @click="handleCallback">Run Callback</button>
    <p>Callback:</p>
    <ul>
      <li v-for="(item, index) in dataCallback" :key="index">{{ item }}</li>
    </ul>

    <button @click="handlePromise">Run Promise</button>
    <p>Promise:</p>
    <ul>
      <li v-for="(item, index) in dataPromise" :key="index">{{ item }}</li>
    </ul>

    <button @click="handleAsync">Run Async/Await</button>
    <p>Async/Await:</p>
    <ul>
      <li v-for="(item, index) in dataAsync" :key="index">{{ item }}</li>
    </ul>
  </div>
</template>

<style scoped>
button {
  margin: 5px;
  padding: 8px 12px;
  border: none;
  background: #007bff;
  color: white;
  cursor: pointer;
  border-radius: 5px;
}

button:hover {
  background: #0056b3;
}

p {
  font-size: 16px;
  margin: 5px 0 5px;
  font-weight: bold;
}

ul {
  padding: 0;
  list-style: none;
}

li {
  font-size: 14px;
  background: #f4f4f4;
  padding: 5px;
  margin: 3px 0;
  border-radius: 5px;
}
</style>