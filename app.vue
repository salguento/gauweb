<script setup lang="ts">
import { createClient } from "@supabase/supabase-js";
const config = useRuntimeConfig();
const supabaseUrl = config.public.supabaseUrl;
const supabaseKey = config.public.supabaseKey;

const supabase = createClient(supabaseUrl, supabaseKey);

const { data: artwork, error } = await supabase.from("artwork").select("*");

function shuffle(a: any[] | null) {
  for (let i = a!.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [a![i], a![j]] = [a![j], a![i]];
  }
  return a;
}

shuffle(artwork);

useHead({
  title: "GAAAUU",
  meta: [{ name: "GAAAUU", content: "Galeria de Arte da URSAL" }],
});
</script>

<template>
  <NuxtLayout>
    <Navbar />
    <main class="min-h-full">
      <div class="mx-auto max-w-7xl px-4 py-6 sm:px-6 lg:px-8">
        <Hero />
        <client-only>
          <Card :artworks="artwork" />
        </client-only>
      </div>
    </main>
    <Footer />
  </NuxtLayout>
</template>
