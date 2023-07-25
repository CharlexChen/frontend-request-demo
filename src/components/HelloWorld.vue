<script setup lang="ts">
import { onMounted, ref } from 'vue'
import axios from 'axios'
import queryString from 'query-string';

defineProps<{ msg: string }>()

const count = ref(0);
const formData = ref<FormData>();

onMounted(() => {
  const data = new FormData();  
  data.append('user_id', '10001');
  formData.value = data;
  paramRequest();
  queryRequest();
  urlencodedRequest();
  formDataRequest();
  jsonRequest();
});

const paramRequest = () => axios.get('http://example.com/user/10001');
const queryRequest = () => axios.get('http://example.com/user?user_id=10001');
const urlencodedRequest = () => axios.post('http://example.com/user', queryString.stringify({
  user_id: 10001,
}));
const formDataRequest = () => axios.post('http://example.com/user', formData.value, {  
  headers: {  
    'Content-Type': 'multipart/form-data'  
  }  
});
const jsonRequest = () => axios.post('http://example.com/user', {
  user_id: 10001,
}, {
  headers: {  
    'Content-Type': 'application/json'  
  }
});
</script>

<template>
  <h1>{{ msg }}</h1>

  <div class="card">
    <button type="button" @click="count++">count is {{ count }}</button>
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
</style>
