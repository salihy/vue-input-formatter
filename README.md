# Vue Input Formatter

## Demo

![](https://github.com/salihy/vue-input-formatter/raw/main/screenshot.gif)

## Installation

Using npm:

```shell
$ npm i vue-input-formatter
```

Using yarn:
```
$ yarn add vue-input-formatter
```

## Usage

```
<script setup lang="ts">
import { VueInputFormatter } from "vue-input-formatter";
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
