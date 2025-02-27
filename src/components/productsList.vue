<script setup lang="ts">
import { ref, watchEffect } from 'vue';
import ProductItem from '@/components/productItem.vue';
import type { IProduct } from '@/types.ts';

const products = ref<IProduct[]>([]);
const searchQuery = ref<string>('');

const fetchProducts = async () => {
  try {
    const url = searchQuery.value
      ? `https://dummyjson.com/products/search?q=${searchQuery.value}&limit=30`
      : 'https://dummyjson.com/products?limit=30';

    const response = await fetch(url);

    if (!response.ok) {
      throw new Error('Network response was not ok');
    }

    const data = await response.json();

    products.value = data.products;
  } catch (e) {
    console.error(e);
  }
};

watchEffect(fetchProducts);
</script>

<template>
  <input
    type="text"
    v-model="searchQuery"
    placeholder="Search..."
    @input="fetchProducts"
    class="w-full max-w-3xl m-4 rounded-md bg-white p-2 mb-4 outline-none"
  />

  <div class="w-full max-w-3xl h-[600px] overflow-auto m-4 space-y-4 p-4 bg-white rounded-md">
    <ProductItem v-for="product in products" :key="product.id" :product="product" />
  </div>
</template>
