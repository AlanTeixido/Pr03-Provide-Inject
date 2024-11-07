<template>
  <div class="cistella">
    <h2>Cistella</h2>
    <ul>
      <li v-for="producte in cistella" :key="producte.name">
        <span>{{ producte.name }}</span>
        <span>{{ getPrice(producte.price) }}</span>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { defineProps } from 'vue';

const props = defineProps({
  cistella: {
    type: Array,
    required: true
  },
  currency: {
    type: String,
    required: true
  }
});

// Funció per formatar el preu segons la moneda
const getPrice = (price) => {
  return props.currency === 'EUR' ? `${price}€` : `${(price * 1.1).toFixed(2)}$`;
};
</script>
