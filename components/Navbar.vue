<template>
  <nav class="fixed w-full z-10">
    <Disclosure
      as="div"
      class="bg-stone-50/50 dark:bg-stone-950/50 backdrop-blur-xl"
      v-slot="{ open }"
    >
      <div class="mx-auto max-w-7xl px-4 sm:px-6 lg:px-8">
        <div class="flex h-16 items-center justify-between">
          <div class="flex items-center">
            <div class="flex-shrink-0">
              <a href="/#home">
                <img
                  class="h-6"
                  src="/gau-logo.svg"
                  alt="Logotipo GAU em cor vermelha"
                />
              </a>
            </div>
          </div>
          <div class="">
            <div class="ml-4 flex items-center md:ml-6">
              <button
                id="btn-dark"
                @click="handleTheme"
                type="button"
                class="relative rounded-full hover:bg-stone-200 dark:hover:bg-stone-800 p-1 dark:text-stone-400 text-stone-600 dark:hover:text-white hover:text-black"
              >
                <span class="absolute -inset-1.5" />
                <span class="sr-only">Mudar tema entre claro e escuro</span>
                <SunIcon
                  v-if="colorMode.value == 'dark'"
                  class="h-6 w-6"
                  aria-hidden="true"
                />
                <MoonIcon
                  v-if="colorMode.value == 'light'"
                  class="h-6 w-6"
                  aria-hidden="true"
                />
              </button>
            </div>
          </div>
        </div>
      </div>

      <DisclosurePanel class="md:hidden">
        <div class="space-y-1 px-2 pb-3 pt-2 sm:px-3">
          <!-- <DisclosureButton
            v-for="item in navigation"
            :key="item.name"
            as="a"
            :href="item.href"
            :class="[
              item.current
                ? 'bg-stone-900 text-white'
                : 'text-stone-300 hover:bg-stone-700 hover:text-white',
              'block rounded-md px-3 py-2 text-base font-medium',
            ]"
            :aria-current="item.current ? 'page' : undefined"
            >{{ item.name }}</DisclosureButton
          > -->
        </div>
        <div class="border-t border-stone-700 pb-3 pt-4">
          <div class="flex items-center px-5">
            <button
              id="btn-dark"
              @click="handleTheme"
              type="button"
              class="relative rounded-full bg-stone-800 p-1 text-stone-400 hover:text-white"
            >
              <span class="absolute -inset-1.5" />
              <span class="sr-only">View notifications</span>
              <SunIcon
                v-if="colorMode.value == 'dark'"
                class="h-6 w-6"
                aria-hidden="true"
              />
              <MoonIcon
                v-if="colorMode.value == 'light'"
                class="h-6 w-6"
                aria-hidden="true"
              />
            </button>
          </div>
        </div>
      </DisclosurePanel>
    </Disclosure>
  </nav>
</template>

<script setup>
import { Disclosure, DisclosurePanel } from "@headlessui/vue";
import { SunIcon, MoonIcon } from "@heroicons/vue/24/outline";

const colorMode = useColorMode();

const navigation = [
  { name: "Dashboard", href: "#", current: true },
  { name: "Team", href: "#", current: false },
  { name: "Projects", href: "#", current: false },
  { name: "Calendar", href: "#", current: false },
  { name: "Reports", href: "#", current: false },
];

const handleTheme = () => {
  console.log("oli");
  if (colorMode.value == "dark") colorMode.preference = "light";
  else colorMode.preference = "dark";
};
</script>
