<template>
  <section class="bg-white pt-28 pb-8 text-gray-900 sm:pt-32 sm:pb-12 lg:pt-40 lg:pb-14">
    <div class="mx-auto w-5/6 max-w-7xl">
      <div v-reveal="'fade-up'" class="mx-auto max-w-3xl space-y-6 text-center">
        <!-- Top Badge -->
        <span
          class="inline-block rounded-full bg-[#04308F]/10 px-4 py-1.5 text-xs font-semibold tracking-widest text-[#04308F] uppercase"
        >
          TaaS for Ventures
        </span>

        <!-- Main Title from User Copy -->
        <h1
          class="font-serif text-3xl leading-tight font-normal tracking-tight text-gray-900 sm:text-4xl lg:text-6xl"
        >
          Don&apos;t Search for Talent. <br />
          <span class="text-[#04308F]">Find the Right Match.</span>
        </h1>

        <!-- Intro Paragraph structurally arranged like the reference style -->
        <p
          class="mx-auto max-w-2xl text-center text-base leading-relaxed font-normal text-gray-600 sm:text-lg"
        >
          Finding the right creative professional can be time-consuming. TaaS helps businesses
          define what they need and connects them with relevant talent from our growing creative
          ecosystem.
        </p>

        <!-- Action Buttons -->
        <div class="flex flex-wrap items-center justify-center gap-4 pt-2">
          <NuxtLink
            to="/contact"
            class="inline-flex items-center gap-2 rounded-full bg-[#04308F] px-8 py-3.5 text-sm font-semibold text-white shadow-lg shadow-[#04308F]/20 transition-all duration-300 hover:scale-105 hover:bg-[#05DED5] hover:text-gray-900"
          >
            <span>Define Your Requirements</span>
            <Icon icon="lucide:arrow-right" class="text-base" />
          </NuxtLink>

          <a
            href="#how-it-works"
            class="inline-flex items-center gap-2 rounded-full border border-gray-300 bg-white px-7 py-3.5 text-sm font-semibold text-gray-800 transition-all duration-300 hover:border-[#04308F] hover:bg-gray-50 hover:text-[#04308F]"
          >
            <span>How It Works</span>
            <Icon icon="lucide:arrow-down" class="text-base" />
          </a>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { Icon } from '@iconify/vue';
</script>

<style scoped lang="css"></style>
