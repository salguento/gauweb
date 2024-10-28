<template>
  <header class="" id="home">
    <div class="mx-auto max-w-2xl py-12 md:py-24 lg:py-32">
      <div class="hidden sm:flex sm:justify-center">
        <div
          class="relative rounded-full px-3 py-1 text-sm leading-6 text-gray-600 ring-1 ring-gray-900/30 dark:text-gray-300 dark:ring-gray-100/30"
        >
          Galeria de Arte da URSAL
        </div>
      </div>
      <div class="text-center">
        <h1
          class="font-display text-balance tracking-tighter text-red-500 dark:text-red-500 text-6xl sm:text-7xl md:text-8xl lg:text-9xl"
        >
          gaaauu
        </h1>
        <p class="m-6 text-lg leading-8 text-gray-800 dark:text-gray-200">
          Coleção de obras de arte latino-americas disponíveis na
          <em>Wikimedia</em> com descrição de imagem gerada com o modelo
          <em>Gemini Flash 1.5</em>
        </p>
        <a
          rel="me"
          href="https://ursal.zone/@gaaauu"
          target="_blank"
          class="text-stone-600 dark:text-stone-400 ring-1 px-4 py-2 ring-stone-600 dark:ring-stone-400 rounded-md hover:text-red-500 hover:ring-red-500"
          >Siga o bot no Mastodon</a
        >
      </div>
    </div>
  </header>
</template>

<script setup>
import { ref } from "vue";
import { Dialog, DialogPanel } from "@headlessui/vue";
import { Bars3Icon, XMarkIcon } from "@heroicons/vue/24/outline";

const navigation = [
  { name: "Product", href: "#" },
  { name: "Features", href: "#" },
  { name: "Marketplace", href: "#" },
  { name: "Company", href: "#" },
];

const mobileMenuOpen = ref(false);
</script>
