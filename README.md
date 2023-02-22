# Vue Input Formatter

```
<script setup lang="ts">
import VueNumberInput from "vue-input-formatter";
import { ref } from "vue";

const testModel = ref<number>(0);

function increase() {
  testModel.value += 1;
}
</script>

<template>
  <VueNumberInput v-model="testModel" />
  <div>{{ testModel }}</div>
  <div>
    <button @click="testModel = 1000">Set to 1000</button>
    <button @click="increase">Increase</button>
  </div>
</template>
```
