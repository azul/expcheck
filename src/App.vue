<template>
  <input type="text" v-model="langName">
  <button @click="go">Submit</button>
  <br/>
  {{ message }}
</template>

<script lang="ts">
import { defineComponent, ref } from 'vue';

import hljs from 'highlight.js/lib/core'

export default defineComponent({
  name: 'App',
  setup() {
    const langName = ref('')
    const message = ref('')
    const go = async () => {
      const module = await import(
        `highlight.js/lib/languages/${langName.value}`
      )
      message.value = module.default.name
    }
    return {
      langName,
      go,
      message,
    }
  }
});
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
