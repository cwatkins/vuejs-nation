<script setup>
import { ref, computed } from "vue";
import { formatter } from "../helpers.js";

const price = ref(null);

const props = defineProps({
  description: String,
  price: Number,
});

const formattedPrice = computed(() => {
  return formatter.format(props.price / 100);
});
</script>

<template>
  <div class="flex flex-row justify-between">
    <div>{{ props.description }}</div>
    <div>{{ formattedPrice }}</div>
  </div>
</template>
