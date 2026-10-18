<script setup lang="ts">
import { Icon } from '@iconify/vue';

const stages = [
  {
    step: '01',
    name: 'IDEATION',
    state: 'You have an idea.',
    solution: 'We help turn it into a structured opportunity.',
    icon: 'lucide:lightbulb',
  },
  {
    step: '02',
    name: 'EARLY STAGE',
    state: 'You have launched.',
    solution: 'We help establish your brand, market and digital foundation.',
    icon: 'lucide:rocket',
  },
  {
    step: '03',
    name: 'GROWTH STAGE',
    state: 'You have traction.',
    solution: 'We help strengthen your positioning, marketing and digital infrastructure.',
    icon: 'lucide:trending-up',
  },
  {
    step: '04',
    name: 'TRANSFORMATION',
    state: 'You have an established business.',
    solution: "We help reposition, modernize and build what's next.",
    icon: 'lucide:refresh-cw',
  },
];
</script>

<template>
  <section class="border-b border-gray-100 bg-white py-20 text-gray-900 lg:py-28">
    <div class="mx-auto w-5/6 max-w-7xl space-y-12 lg:space-y-16">
      <!-- Section Header -->
      <div v-reveal="'fade-up'" class="mx-auto max-w-3xl space-y-3 text-center">
        <h2
          class="font-serif text-3xl leading-tight font-normal tracking-tight text-gray-900 sm:text-4xl lg:text-5xl"
        >
          Who Is The Growth Lab For?
        </h2>
        <p class="font-serif text-xl font-normal text-[#04308F] sm:text-2xl">
          Built for Ventures at Every Growth Stage
        </p>
      </div>

      <!-- 4 Stages Grid -->
      <div class="grid grid-cols-1 gap-6 sm:grid-cols-2 lg:grid-cols-4 lg:gap-8">
        <div
          v-for="st in stages"
          :key="st.name"
          v-reveal="'fade-up'"
          class="flex flex-col justify-between rounded-2xl border border-gray-200/80 bg-[#FAFAFA] p-7 transition-all duration-300 hover:border-[#04308F]/30 hover:bg-white hover:shadow-lg sm:p-8"
        >
          <div class="space-y-4">
            <div class="flex items-center justify-between border-b border-gray-200 pb-3">
              <span class="font-mono text-xs font-bold text-[#04308F]">STAGE {{ st.step }}</span>
              <div
                class="flex size-8 items-center justify-center rounded-lg bg-white text-base text-[#04308F] shadow-2xs"
              >
                <Icon :icon="st.icon" />
              </div>
            </div>

            <h3 class="font-serif text-2xl font-bold tracking-tight text-gray-900">
              {{ st.name }}
            </h3>

            <p class="text-sm font-semibold text-[#04308F]">
              {{ st.state }}
            </p>

            <p class="text-sm leading-relaxed text-gray-600">
              {{ st.solution }}
            </p>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped lang="css"></style>
