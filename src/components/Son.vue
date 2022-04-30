<script setup lang="ts">
import HelloWorld from "./HelloWorld.vue";
import { ref } from "vue";
const list = [1, 3, 5, 2, 9, 2, 4, 8, 6];
const hello = ref(null);
console.log(hello.value);
</script>
<template>
  <span>son</span>
  <HelloWorld ref="hello" />
</template>