<script setup lang="ts">
import { defineProps } from 'vue';
import type { IProduct } from '@/types.ts';

const props = defineProps<{
  product: IProduct;
}>();
</script>

<template>
  <div class="flex flex-col md:flex-row gap-4 p-4 rounded-md bg-indigo-100">
    <div class="md:basis-1/4">
      <img class="w-[180px] h-[180px] mx-auto object-contain" :src="product.images[0]"
           :alt="product.title" />
    </div>

    <div class="md:basis-3/4">
      <h2 class="mb-2 font-bold">{{ product.title }}</h2>

      <p class="mb-2 text-sm text-slate-500">{{ product.description }}</p>

      <div class="flex items-center space-x-4 mb-2">
        <span v-if="product.discountPercentage" class="text-xs font-bold text-red-500">
          Discount {{ product.discountPercentage }} %
        </span>

        <span v-if="product.brand" class="text-sm font-bold text-indigo-500">{{ product.brand
          }}</span>
      </div>

      <div class="flex items-center space-x-4">
        <span class="text-lg font-bold text-indigo-500">${{ product.price }}</span>

        <span v-if="product.rating"
              class="text-lg font-bold text-indigo-500">&#11088; {{ product.rating }}</span>

        <span v-if="product.brand"
              class="py-1 px-2 bg-indigo-500 font-bold text-indigo-100 text-xs rounded-full">{{ product.brand
          }}</span>
      </div>
    </div>
  </div>
</template>
