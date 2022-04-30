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
let timer: number;
const doubleCount = computed((): number => count.value * 2);

const obj = ref({ age: 18 });

const flag = ref(true);
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

const emit = defineEmits(["changeMsg"]);
const edit = () => {
  emit("changeMsg", "hi vue");
};

// onMounted(sub);
// watch(count, (newVal, oldValue) => {
//   console.log(newVal);
//   console.log(oldValue);
// });

const popSort = (arr: Array<number>): Array<number> => {
  console.log("enter");
  for (let i = 0; i < arr.length; i++) {
    for (let j = i; j < arr.length; j++) {
      if (arr[i] < arr[j]) {
        let temp = arr[i];
        arr[i] = arr[j];
        arr[j] = temp;
      }
    }
  }
  return arr;
};
defineExpose({
  popSort,
});
</script>

<template>
  <div style="border: 1px solid">
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
  </div>
</template>

<style>
* {
  user-select: none;
}
</style>
