<template>
  <div>
    <h2>Productes</h2>
    <ul>
      <li v-for="producte in productes" :key="producte.name">
        <span>{{ producte.name }} - {{ getPrice(producte.price) }}</span>
        <button class="add-to-cart" @click="afegirAlaCistella(producte)">Add to Cart</button>
      </li>
    </ul>
  </div>
</template>

<script setup>
import { inject, defineProps } from 'vue';

const props = defineProps({
  currency: {
    type: String,
    required: true
  }
});

const productes = [
  { name: "Hamburger 🍔", price: 5 },
  { name: "Cheeseburger 🧀", price: 6 },
  { name: "Impossible Burger 🥕", price: 7 },
  { name: "Fries 🍟", price: 2 }
];

const afegirAlaCistella = inject('afegirAlaCistella');

// Funció per formatar el preu segons la moneda
const getPrice = (price) => {
  return props.currency === 'EUR' ? `${price}€` : `${(price * 1.1).toFixed(2)}$`;
};
</script>
