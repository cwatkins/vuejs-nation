<script setup>
import { ref } from "vue";
import CheckoutProduct from "../components/CheckoutProduct.vue";
import CheckoutTotals from "../components/CheckoutTotals.vue";
import CheckoutButton from "../components/CheckoutButton.vue";

const isLoading = ref(false);

const redirectToStripe = async () => {
  isLoading.value = true;

  const response = await fetch("/api/create-checkout-session", {
    method: "POST",
  });
  const { error, url } = await response.json();

  if (error) {
    isLoading.value = false;
    console.log(error.message);
  } else {
    window.location.href = url;
  }
};
</script>

<template>
  <h1 class="text-3xl uppercase pb-4">Checkout</h1>
  <section class="border">
    <h2 class="text-lg uppercase bg-zinc-100 py-2 px-12">In Your Bag</h2>
    <div class="px-12 pt-8 pb-4">
      <h3 class="font-semibold uppercase text-left">Arrives Feb 1, 2022</h3>
      <hr />
      <checkout-product
        image="https://fakestoreapi.com/img/81fPKd-2AYL._AC_SL1500_.jpg"
        title="Fjallraven - Foldsack No. 1 Backpack"
        description="Your perfect pack for everyday use and walks in the forest. Stash your laptop (up to 15 inches) in the padded sleeve, your everyday backpack."
        color="Navy"
        :quantity="1"
        :price="10955"
      />
      <hr />
      <checkout-totals
        :subtotal="10995"
        :estimatedShipping="0"
        :estimatedTax="0"
        :total="10955"
      />
    </div>
  </section>
  <checkout-button :isLoading="isLoading" @click="redirectToStripe" />
</template>
