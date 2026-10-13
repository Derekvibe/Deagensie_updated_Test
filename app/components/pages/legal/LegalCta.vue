<script setup lang="ts">
import { Icon } from '@iconify/vue';
</script>

<template>
  <section class="border-t border-gray-100 bg-gray-50/70 py-16 lg:py-20">
    <div class="mx-auto w-5/6 max-w-7xl">
      <div
        class="relative overflow-hidden rounded-3xl bg-linear-to-br from-[#020B1E] via-[#041B48] to-[#04308F] p-8 text-white shadow-xl sm:p-12 lg:p-16"
      >
        <!-- Background subtle glow accents -->
        <div
          class="pointer-events-none absolute -top-24 -right-24 h-72 w-72 rounded-full bg-[#05DED5]/20 blur-3xl"
        />
        <div
          class="pointer-events-none absolute -bottom-24 -left-24 h-72 w-72 rounded-full bg-[#8F039C]/20 blur-3xl"
        />

        <div class="relative z-10 grid gap-8 lg:grid-cols-[1.5fr_1fr] lg:items-center">
          <div class="space-y-4">
            <span
              class="inline-flex items-center gap-1.5 rounded-full bg-white/10 px-3.5 py-1 text-xs font-semibold tracking-wider text-[#05DED5] uppercase backdrop-blur-xs"
            >
              <Icon icon="solar:shield-warning-bold" class="text-sm" />
              <span>Compliance & Inquiries</span>
            </span>

            <h2
              class="font-serif text-2xl font-normal tracking-tight text-white sm:text-3xl lg:text-4xl"
            >
              Have questions regarding our legal agreements?
            </h2>

            <p class="max-w-xl text-sm leading-relaxed text-gray-300 sm:text-base">
              Whether you are a venture founder needing a tailored Master Services Agreement (MSA)
              and mutual NDA, or a creative talent seeking clarification on IP rights and
              international payouts, our compliance team is here to assist.
            </p>

            <div class="flex flex-wrap items-center gap-4 pt-2 text-xs text-gray-300 sm:text-sm">
              <div class="flex items-center gap-1.5">
                <Icon icon="solar:letter-bold" class="text-[#05DED5]" />
                <a href="mailto:legal@deagensie.com" class="underline hover:text-white"
                  >legal@deagensie.com</a
                >
              </div>
              <span class="text-white/30">&bull;</span>
              <div class="flex items-center gap-1.5">
                <Icon icon="solar:lock-keyhole-bold" class="text-[#05DED5]" />
                <span>Enterprise Data Processing Available</span>
              </div>
            </div>
          </div>

          <div class="flex flex-col gap-3 sm:flex-row sm:items-center lg:flex-col lg:items-end">
            <NuxtLink
              to="/contact"
              class="inline-flex items-center justify-center gap-2 rounded-full bg-[#05DED5] px-6 py-3.5 text-sm font-semibold text-[#020B1E] shadow-lg shadow-[#05DED5]/20 transition-all duration-300 hover:scale-105 hover:bg-white"
            >
              <span>Contact Compliance Team</span>
              <Icon icon="solar:arrow-right-linear" class="text-base" />
            </NuxtLink>

            <NuxtLink
              to="/business"
              class="inline-flex items-center justify-center gap-2 rounded-full border border-white/20 bg-white/5 px-6 py-3.5 text-sm font-semibold text-white backdrop-blur-xs transition-all duration-300 hover:bg-white/10"
            >
              <span>Explore Growth Lab Solutions</span>
            </NuxtLink>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
