<script setup>
import { ref, onMounted, computed } from "vue";
import { useRoute } from "vue-router";

const checkoutSession = ref("");

const currentRoute = computed(() => {
  return useRoute().query;
});

const getCheckout = async () => {
  const sessionId = currentRoute.value?.session_id;
  const response = await fetch(`/api/checkout-session?sessionId=${sessionId}`);
  const session = await response.json();

  return JSON.stringify(session, null, 2);
};

onMounted(async () => {
  checkoutSession.value = await getCheckout();
});
</script>

<template>
  <h1 class="text-3xl uppercase pb-4">Thank you</h1>
  <section class="border">
    <h2 class="text-lg uppercase bg-zinc-100 py-2 px-12">Your order</h2>
    <div class="px-12 pt-8 pb-4">
      <h3 class="font-semibold uppercase text-left">Arrives Feb 1, 2022</h3>
      <hr />
      <pre>
        <code class="text-left block whitespace-pre overflow-x-scroll">{{ checkoutSession }}</code>
      </pre>
    </div>
  </section>
</template>
