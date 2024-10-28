<script setup lang="ts">
import type { PropType } from "vue";
import { ArrowLongRightIcon, XMarkIcon } from "@heroicons/vue/24/outline";
import { ref } from "vue";

let input = ref("");
const props = defineProps({
  artworks: {
    type: Array as PropType<any[]> | PropType<null>,
    required: true,
  },
});
const { artworks } = props;

function filteredList() {
  return artworks!.filter(
    (artwork) =>
      (artwork.title.toLowerCase().includes(input.value.toLowerCase()) ||
        artwork.artist.toLowerCase().includes(input.value.toLowerCase()) ||
        artwork.date
          .toString()
          .toLowerCase()
          .includes(input.value.toLowerCase()) ||
        artwork.country.toLowerCase().includes(input.value.toLowerCase())) &&
      artwork.alt_text
  );
}

function handleClear() {
  input.value = "";
}
</script>

<template>
  <div>
    <div :class="input ? 'mb-4' : 'mb-[3.75rem]'">
      <div class="max-w-md mx-auto">
        <label
          for="default-search"
          class="mb-2 text-sm font-medium text-stone-900 sr-only dark:text-white"
          >Busca</label
        >
        <div class="relative">
          <div
            class="absolute inset-y-0 start-0 flex items-center ps-3 pointer-events-none"
          ></div>
          <button
            v-if="input"
            @click="handleClear()"
            type="button"
            class="absolute end-2.5 bottom-2.5 rounded-full p-1 dark:text-stone-400 text-stone-600 dark:hover:text-white hover:text-black focus:outline-none focus:ring-2 dark:focus:ring-white focus:ring-black focus:ring-offset-2 dark:focus:ring-offset-stone-800 focus:ring-offset-stone-200"
          >
            <XMarkIcon class="h-6 w-6" aria-hidden="true" />
          </button>
          <input
            type="search"
            v-model="input"
            id="default-search"
            class="block w-full p-4 ps-6 text-sm text-stone-900 border border-stone-300 rounded-lg bg-stone-50 focus:ring-red-500 focus:border-red-500 dark:bg-stone-900 dark:border-stone-600 dark:placeholder-stone-400 dark:text-white dark:focus:ring-red-500 dark:focus:border-red-500 focus:outline-none"
            placeholder="Encontre obras por título, autor, país ou data..."
          />
        </div>
      </div>
    </div>
    <div class="" v-for="artwork in filteredList()" :key="artwork.id"></div>
    <div class="h-full" v-if="input && !filteredList().length">
      <p class="text-xl text-center text-black dark:text-white">
        Nenhum resultado encontrado!
      </p>
    </div>
    <div class="h-full" v-if="input && filteredList().length">
      <p class="text-lg text-center text-black dark:text-white mb-4">
        {{ filteredList().length }} obras encontradas
      </p>
    </div>
    <div class="flex justify-center">
      <div
        class="columns-1 sm:columns-2 md:columns-3 lg:columns-4 gap-4 max-w-7xl space-y-4 mb-8"
      >
        <div
          v-for="artwork in filteredList()"
          :key="artwork.id"
          class="break-after-all break-inside-avoid-column"
        >
          <div
            v-if="artwork.alt_text"
            class="max-w-sm bg-white border border-stone-200 rounded-2xl overflow-hidden shadow dark:bg-stone-800 dark:border-stone-700"
          >
            <img
              class="rounded-t-lg w-full"
              :src="artwork.preferred_file_url"
              :alt="artwork.alt_text"
              :title="artwork.alt_text"
            />
            <div class="p-5 pt-3">
              <div
                class="flex flex-wrap justify-start gap-x-2 text-xs text-stone-700 dark:text-stone-300"
              >
                <p class="font-normal text-nowrap">
                  <span v-if="artwork.country == 'Argentina'">🇦🇷</span>
                  <span v-if="artwork.country == 'Bolívia'">🇧🇴</span>
                  <span v-if="artwork.country == 'Brasil'">🇧🇷</span>
                  <span v-if="artwork.country == 'Chile'"> 🇨🇱 </span>
                  <span v-if="artwork.country == 'Colômbia'">🇨🇴</span>
                  <span v-if="artwork.country == 'Costa Rica'">🇨🇷</span>
                  <span v-if="artwork.country == 'Cuba'">🇨🇺</span>
                  <span v-if="artwork.country == 'Equador'">🇪🇨</span>
                  <span v-if="artwork.country == 'El Salvador'">🇸🇻</span>
                  <span v-if="artwork.country == 'Guatemala'">🇬🇹</span>
                  <span v-if="artwork.country == 'Haiti'">🇭🇹</span>
                  <span v-if="artwork.country == 'Honduras'">🇭🇳</span>
                  <span v-if="artwork.country == 'México'">🇲🇽</span>
                  <span v-if="artwork.country == 'Nicarágua'">🇳🇮</span>
                  <span v-if="artwork.country == 'Panamá'">🇵🇦</span>
                  <span v-if="artwork.country == 'Paraguai'">🇵🇾</span>
                  <span v-if="artwork.country == 'Peru'">🇵🇪</span>
                  <span v-if="artwork.country == 'Porto Rico'">🇵🇷</span>
                  <span v-if="artwork.country == 'República Dominicana'"
                    >🇩🇴</span
                  >
                  <span v-if="artwork.country == 'Uruguai'">🇺🇾</span>
                  <span v-if="artwork.country == 'Venezuela'">🇻🇪</span>
                  {{ artwork.country }}
                </p>
                <p class="font-normal text-nowrap">
                  {{ artwork.date }}
                </p>
                <p class="font-normal text-ellipsis">
                  {{ artwork.medium }}
                </p>
              </div>
              <h5
                class="pt-0 mb-0 text-xl font-bold text-stone-900 dark:text-white"
              >
                {{ artwork.title }}
              </h5>
              <p class="text-md font-normal text-stone-700 dark:text-stone-300">
                {{ artwork.artist }}
              </p>
              <p
                class="text-sm font-normal text-stone-700 dark:text-stone-200 py-4"
              >
                {{ artwork.alt_text }}
              </p>

              <a
                :href="artwork.attribution_url"
                target="_blank"
                class="cursor-pointer inline-flex w-full justify-end text-sm font-medium text-stone-400 dark:text-stone-500 bg-transparent rounded-lg dark:bg-transparent hover:text-red-500"
              >
                Referência
                <ArrowLongRightIcon class="h-5" />
              </a>
            </div>
          </div>
        </div>
      </div>
    </div>
  </div>
</template>
