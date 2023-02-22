<template>
  <input
    type="string"
    v-model="innerStrValue"
    :placeholder="placeholder"
    @keydown="checkInput($event)"
    @keyup="formatInput($event)"
  />
</template>

<script lang="ts" setup>
import { onMounted, ref, watch } from "vue";

const props = defineProps({
  modelValue: Number,
});

const placeholder = ref("0.00");
const innerStrValue = ref<string>("");
const innerNumValue = ref<number | undefined>(props.modelValue);

const emit = defineEmits(["update:modelValue"]);

onMounted(() => {
  innerStrValue.value = new Intl.NumberFormat("en-US", {
    maximumFractionDigits: 2,
  }).format(innerNumValue.value ? innerNumValue.value : 0);
});

watch(innerNumValue, (newVal, oldVal) => {
  innerStrValue.value = new Intl.NumberFormat("en-US", {
    maximumFractionDigits: 2,
  }).format(innerNumValue.value ? innerNumValue.value : 0);
  emit("update:modelValue", innerNumValue.value);
});

watch(props, () => {
  innerNumValue.value = props.modelValue;
});

watch(innerStrValue, (newVal, oldVal) => {
  //emit("update:modelValue", newVal);
  console.log(newVal, oldVal);
  innerNumValue.value = parseLocaleNumber(newVal, "en-US");
});

//new Intl.NumberFormat("en-US", { maximumFractionDigits: 2 }).format(number)

function checkInput($event: KeyboardEvent) {
  if (
    ($event.key >= "0" && $event.key <= "9") ||
    $event.key === "." ||
    $event.key === "Backspace"
  ) {
  } else {
    $event.preventDefault();
  }
}

function formatInput($event: KeyboardEvent) {
  if (
    ($event.key >= "0" && $event.key <= "9") ||
    $event.key === "." ||
    $event.key === "Backspace"
  ) {
    var strNum = props.modelValue?.toString();
    if ($event.key !== ".") {
      if (innerStrValue.value.length === 0 && $event.key === "Backspace") {
        innerStrValue.value = "";
        innerNumValue.value = 0;
      } else {
        innerStrValue.value = new Intl.NumberFormat("en-US", {
          maximumFractionDigits: 2,
        }).format(innerNumValue.value ? innerNumValue.value : 0);
      }
    }
  } else {
    $event.preventDefault();
  }
}

function parseLocaleNumber(stringNumber: string, locale: string) {
  var thousandSeparator = Intl.NumberFormat(locale)
    .format(11111)
    .replace(/\p{Number}/gu, "");
  var decimalSeparator = Intl.NumberFormat(locale)
    .format(1.1)
    .replace(/\p{Number}/gu, "");

  return parseFloat(
    stringNumber
      .replace(new RegExp("\\" + thousandSeparator, "g"), "")
      .replace(new RegExp("\\" + decimalSeparator), ".")
  );
}
</script>
