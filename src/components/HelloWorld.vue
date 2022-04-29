<script setup lang="ts">
import { computed, onMounted, reactive, ref, watch } from "vue";

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

const emit = defineEmits(["changeMsg"]);

const add = () => {
  count.value++;
};

const sub = () => {
  count.value--;
};

const edit = () => {
  emit("changeMsg", "hi vue");
};
// onMounted(sub);
// watch(count, (newVal, oldValue) => {
//   console.log(newVal);
//   console.log(oldValue);
// });

const doubleCount = ref(computed(() => count.value * 2));
// error
const computedStyle = computed(() => {
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
  <button @click="sub">-</button>
  {{ count }}
  <button @click="add">+</button>
  <br />
  <span>computed:{{ doubleCount }}</span>
  <br />
  <span @click="obj.age++">obj:{{ obj.age }}</span>
  <br />
  <span @click="flag = !flag" :class="computedStyle">wow</span>
</template>

<style scoped>
* {
  user-select: none;
}
</style>
