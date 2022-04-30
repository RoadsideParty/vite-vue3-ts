<script setup lang="ts">
import { ref, watch } from "vue";
import HelloWorld from "./components/HelloWorld.vue";
import Son from "./components/Son.vue";
const msg = ref("hello world");
const changeMsg = (data: string) => {
  msg.value = data;
};
watch(msg, (newVal) => {
  setTimeout(() => {
    msg.value = "hello world";
  }, 1000);
});
</script>

<template>
  <HelloWorld :msg="msg" @changeMsg="changeMsg" />
  <Son />
</template>

<style>
</style>
