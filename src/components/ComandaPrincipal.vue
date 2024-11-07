<template>
  <div>
    <h1>AlanTeixi's Burger</h1>
    <input v-model="nom_comanda" placeholder="AlanTeixi's Burger" />
    <button @click="placeOrder">Place Order</button>

    <!-- Botó per canviar de moneda -->
    <button class="currency-toggle" @click="toggleCurrency">Currency: {{ currencySymbol }}</button>

    <LlistaProductes :currency="currency" />
    <Cistella :cistella="cistella" :currency="currency" />
  </div>
</template>

<script setup>
import { ref, provide, computed } from 'vue';  // Afegim computed
import LlistaProductes from './LlistaProductes.vue';
import Cistella from './Cistella.vue';

const nom_comanda = ref('');
const cistella = ref([]);
const currency = ref('EUR');  // Inicialment en EUR

// Funció per alternar entre EUR i USD
const toggleCurrency = () => {
  currency.value = currency.value === 'EUR' ? 'USD' : 'EUR';
};

// Retorna el símbol de la moneda actual
const currencySymbol = computed(() => (currency.value === 'EUR' ? '€' : '$'));

// Funció per realitzar la comanda i buidar la cistella i el nom
const placeOrder = () => {
  if (cistella.value.length > 0 || nom_comanda.value) {
    alert(`Comanda realitzada per: ${nom_comanda.value}`);
    nom_comanda.value = '';  // Buidem el nom de la comanda
    cistella.value = [];     // Buidem la cistella
  } else {
    alert('No hi ha productes a la cistella o nom de comanda.');
  }
};

// Funció per afegir productes a la cistella
const afegirAlaCistella = (producte) => {
  const convertedProduct = {
    ...producte,
    price: currency.value === 'EUR' ? producte.price : (producte.price * 1.1).toFixed(2)
  };
  cistella.value.push(convertedProduct);
};

// Proveïm la funció i la moneda per a que altres components les utilitzin
provide('afegirAlaCistella', afegirAlaCistella);
provide('currency', currency);
</script>

<style scoped>
/* Estils addicionals si calen */
</style>
