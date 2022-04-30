<script setup lang="ts">
import { computed, onMounted, reactive, ref, StyleValue, watch } from "vue";

defineProps({
  msg: {
    type: String,
  },
});
// only typescript
// defineProps<{ msg: string }>();

const count = ref(0);
const obj = ref({ age: 18 });
const flag = ref(true);
let timer: number;
const emit = defineEmits(["changeMsg"]);

const add = () => {
  count.value++;
  timer = setInterval(() => {
    count.value++;
  }, 100);
};
const sub = () => {
  count.value--;
  timer = setInterval(() => {
    count.value--;
  }, 100);
};
window.addEventListener("mouseup", () => {
  if (timer) {
    clearInterval(timer);
  }
});

const edit = () => {
  emit("changeMsg", "hi vue");
};

// onMounted(sub);
// watch(count, (newVal, oldValue) => {
//   console.log(newVal);
//   console.log(oldValue);
// });

const doubleCount = computed((): number => count.value * 2);

const computedStyle = computed((): StyleValue => {
  if (flag.value) {
    return {
      color: "red",
      fontSize: "20px",
    };
  }
  return {
    fontWeight: "bold",
    color: "blue",
    fontSize: "40px",
  };
});
</script>

<template>
  <span @click="edit">{{ msg }}</span>
  <br />
  <button @mousedown="sub">-</button>
  {{ count }}
  <button @mousedown="add">+</button>
  <br />
  <span>computed:{{ doubleCount }}</span>
  <br />
  <span @click="obj.age++">obj:{{ obj.age }}</span>
  <br />
  <span @click="flag = !flag" :style="computedStyle">wow</span>
</template>

<style scoped>
* {
  user-select: none;
}
</style>
