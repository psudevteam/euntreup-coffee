<script setup lang="ts">
import Logo from "../../../assets/img/logo/logo.svg";
</script>
<template>
  <nav
    class="flex z-50 md:sticky justify-center items-center top-0 w-full bg-white p-4 h-auto"
  >
    <div class="flex gap-x-2 justify-center items-center w-full">
      <img width="40" :src="Logo" alt="" />
      <span class="text-1xl font-bold text-black-900">Euntreup Coffee</span>
    </div>
    <div class="hidden flex w-full gap-x-4 items-center cursor-pointer">
      <span class="text-amber-700 hover:text-blue-600 font-medium">Home</span>
      <span class="text-amber-700 hover:text-blue-600 font-medium">About</span>
      <span class="text-amber-700 hover:text-blue-600 font-medium"
        >List Product</span
      >
    </div>
    <div class="hidden flex w-full gap-x-4 cursor-pointer">
      <span class="text-amber-700 hover:text-blue-600 font-medium"
        >Admin Panel</span
      >
    </div>
  </nav>
</template>
