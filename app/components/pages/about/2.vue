<script setup lang="ts">
import { Icon } from '@iconify/vue';
</script>

<template>
  <section
    id="mission-vision"
    class="border-b border-gray-100 bg-white py-20 text-gray-900 sm:py-24 lg:py-32"
  >
    <div class="mx-auto w-5/6 max-w-7xl space-y-12 sm:space-y-16">
      <!-- Section Header -->
      <div v-reveal="'fade-up'" class="mx-auto max-w-3xl space-y-4 text-center">
        <span
          class="inline-block rounded-full bg-[#04308F]/10 px-4 py-1.5 text-xs font-semibold tracking-widest text-[#04308F] uppercase"
        >
          Mission &amp; Vision
        </span>
        <h2
          class="mx-auto w-full max-w-3xl text-center font-serif text-2xl leading-tight font-normal tracking-tight text-gray-900 sm:text-4xl lg:text-5xl 2xl:text-6xl"
        >
          Driven by purpose, <br /><span class="text-[#04308F]">defined by impact</span>
        </h2>
        <p class="mx-auto max-w-2xl text-base leading-relaxed font-normal text-gray-500 sm:text-lg">
          Our mission and vision define how we partner with ambitious organizations to build
          enduring brands and shape Africa&apos;s digital future.
        </p>
      </div>

      <!-- Two-Column Standard Cards Grid -->
      <div class="grid grid-cols-1 gap-8 md:grid-cols-2 lg:gap-10">
        <!-- Our Mission Card -->
        <div
          v-reveal="'fade-right'"
          class="group relative flex flex-col justify-between rounded-3xl border border-gray-200/80 bg-[#F4F7FC]/60 p-8 transition-all duration-300 hover:-translate-y-1 hover:border-[#04308F]/30 hover:bg-[#F4F7FC] hover:shadow-lg sm:p-10 lg:p-12"
        >
          <div class="space-y-6">
            <div class="flex items-center justify-between border-b border-gray-200/70 pb-5">
              <span
                class="inline-flex items-center gap-2 rounded-full bg-[#04308F]/10 px-3.5 py-1 text-xs font-semibold tracking-wider text-[#04308F] uppercase"
              >
                <Icon icon="lucide:target" class="size-3.5" />
                Our Mission
              </span>
              <span class="font-mono text-xs font-medium text-gray-400">/ 01</span>
            </div>

            <h3 class="font-serif text-2xl font-normal tracking-tight text-gray-900 sm:text-3xl">
              Our Mission
            </h3>

            <p class="text-base leading-relaxed font-normal text-gray-600 sm:text-lg">
              We partner with startups, enterprises, governments agencies, and visionary founders to
              design brands, build digital products, automate operations, drive sustainable growth,
              unlock global creative talent, and expand the boundaries of Africa&apos;s digital
              economy.
            </p>
          </div>
        </div>

        <!-- Our Vision Card -->
        <div
          v-reveal="'fade-left'"
          class="group relative flex flex-col justify-between rounded-3xl border border-gray-200/80 bg-[#F4F7FC]/60 p-8 transition-all duration-300 hover:-translate-y-1 hover:border-[#04308F]/30 hover:bg-[#F4F7FC] hover:shadow-lg sm:p-10 lg:p-12"
        >
          <div class="space-y-6">
            <div class="flex items-center justify-between border-b border-gray-200/70 pb-5">
              <span
                class="inline-flex items-center gap-2 rounded-full bg-[#04308F]/10 px-3.5 py-1 text-xs font-semibold tracking-wider text-[#04308F] uppercase"
              >
                <Icon icon="lucide:eye" class="size-3.5" />
                Our Vision
              </span>
              <span class="font-mono text-xs font-medium text-gray-400">/ 02</span>
            </div>

            <h3 class="font-serif text-2xl font-normal tracking-tight text-gray-900 sm:text-3xl">
              Our Vision
            </h3>

            <p class="text-base leading-relaxed font-normal text-gray-600 sm:text-lg">
              Africa&apos;s leading AI-powered business transformation company, building brands that
              compete globally, and a borderless world where African creative talent collaborates
              with the world&apos;s leading businesses without limitations.
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped lang="css"></style>
