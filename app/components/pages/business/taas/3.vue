<template>
  <section class="bg-[#04308F] py-20 text-white lg:py-28">
    <div v-reveal="'fade-up'" class="mx-auto w-5/6 max-w-5xl space-y-6 text-center">
      <h2
        class="mx-auto w-full max-w-3xl text-center font-serif text-2xl leading-tight font-normal tracking-tight text-white sm:text-4xl lg:text-5xl 2xl:text-5xl"
      >
        Ready to Find the Right Match?
      </h2>
      <p class="mx-auto max-w-2xl text-base leading-relaxed font-normal text-gray-200 sm:text-lg">
        TaaS helps businesses define what they need and connects them with relevant talent from our
        growing creative ecosystem.
      </p>
      <div class="flex flex-wrap items-center justify-center gap-4 pt-4">
        <NuxtLink
          to="/contact"
          class="inline-flex items-center gap-2 rounded-full bg-[#05DED5] px-8 py-4 text-base font-semibold text-gray-900 shadow-lg shadow-black/20 transition-all duration-300 hover:scale-105 hover:bg-white"
        >
          <span>Schedule Talent Scoping Call</span>
          <Icon icon="lucide:arrow-right" class="text-base" />
        </NuxtLink>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { Icon } from '@iconify/vue';
</script>

<style scoped lang="css"></style>
