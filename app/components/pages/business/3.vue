<script setup lang="ts">
import { Icon } from '@iconify/vue';

interface GrowthCard {
  tag: string;
  bgColor: string;
  image: string;
  stat: string;
  statLabel: string;
  headline: string;
  description: string;
}

const cards: GrowthCard[] = [
  {
    tag: 'DEAGENSIE | STRATEGY & BRAND',
    bgColor: 'bg-[#3D6686]',
    image: '/images/pages/business/growth-system-1.jpg',
    stat: '01',
    statLabel: 'System Foundation',
    headline: 'A strategy that informs the brand.',
    description:
      'Most agencies solve problems in silos. We align commercial positioning, audience insight, and value architecture so every visual and verbal asset builds undeniable market presence.',
  },
  {
    tag: 'DEAGENSIE | MARKETING & DEMAND',
    bgColor: 'bg-[#8E4056]',
    image: '/images/pages/business/growth-system-2.jpg',
    stat: '02',
    statLabel: 'System Acceleration',
    headline: 'A brand that informs marketing. Marketing that drives demand.',
    description:
      'When marketing is guided by a sharp brand, every campaign resonates. We create multi-channel acquisition engines that reliably generate high-intent pipeline and customer traction.',
  },
  {
    tag: 'DEAGENSIE | PLATFORMS & DATA',
    bgColor: 'bg-[#3E6F5B]',
    image: '/images/pages/business/growth-system-3.jpg',
    stat: '03',
    statLabel: 'System Execution',
    headline: 'Digital platforms that deliver. And data that informs what happens next.',
    description:
      'High-velocity digital experiences engineered for conversion and operational delivery, coupled with telemetry that continuously reveals the next strategic opportunity.',
  },
];

const systemPillars = [
  { step: '01', title: 'Strategy', detail: 'Informs the brand' },
  { step: '02', title: 'Brand', detail: 'Informs marketing' },
  { step: '03', title: 'Marketing', detail: 'Drives demand' },
  { step: '04', title: 'Platforms', detail: 'Deliver the business' },
  { step: '05', title: 'Data', detail: 'Informs what is next' },
];
</script>

<template>
  <section class="border-b border-gray-100 bg-[#FAFAFA] py-20 text-gray-900 lg:py-28">
    <div class="mx-auto w-5/6 max-w-7xl space-y-16 lg:space-y-20">
      <!-- Section Header -->
      <div v-reveal="'fade-up'" class="mx-auto max-w-3xl space-y-4 text-center">
        <span
          class="inline-block rounded-full bg-[#04308F]/10 px-4 py-1.5 text-xs font-semibold tracking-widest text-[#04308F] uppercase"
        >
          The Venture System
        </span>

        <h2
          class="font-serif text-3xl leading-tight font-normal tracking-tight text-gray-900 sm:text-4xl lg:text-5xl"
        >
          More Than an Agency. <br class="hidden sm:inline" />
          <span class="text-[#04308F]">A Venture Growth System.</span>
        </h2>

        <p class="mx-auto max-w-2xl text-base leading-relaxed font-normal text-gray-600 lg:text-lg">
          Most agencies solve individual problems. You need the pieces to work together.
        </p>
      </div>

      <!-- 3-Column Illustrated Cards Grid (Style of Reference) -->
      <div class="grid grid-cols-1 gap-7 md:grid-cols-2 lg:grid-cols-3 lg:gap-8">
        <div
          v-for="(card, idx) in cards"
          :key="card.tag"
          v-reveal="{ animation: 'fade-up', delay: idx * 120 }"
          class="group relative flex min-h-[560px] flex-col justify-between overflow-hidden rounded-[26px] p-7 text-white shadow-xl transition-all duration-300 hover:-translate-y-1.5 hover:shadow-2xl sm:p-8"
          :class="[card.bgColor]"
        >
          <!-- Top Tag / Header -->
          <div class="flex items-center justify-between border-b border-white/20 pb-4">
            <span class="font-mono text-[11px] font-bold tracking-widest text-white/95 uppercase">
              {{ card.tag }}
            </span>
            <span class="size-2 rounded-full bg-[#05DED5]" />
          </div>

          <!-- Middle Conceptual Illustration Image with Seamless Radial Edge Blend -->
          <div class="my-auto flex items-center justify-center py-6 select-none">
            <div class="relative flex w-full items-center justify-center">
              <NuxtImg
                :src="card.image"
                :alt="card.headline"
                class="h-52 w-auto max-w-full object-contain transition-transform duration-500 group-hover:scale-105"
                style="
                  mask-image: radial-gradient(ellipse at center, black 65%, transparent 100%);
                  -webkit-mask-image: radial-gradient(
                    ellipse at center,
                    black 65%,
                    transparent 100%
                  );
                "
              />
            </div>
          </div>

          <!-- Bottom Metric & Copy -->
          <div class="space-y-3 pt-2">
            <!-- Big Stat & Stat Label -->
            <div>
              <div class="font-serif text-3xl font-bold tracking-tight text-white sm:text-4xl">
                {{ card.stat }}
              </div>
              <div class="text-xs font-semibold tracking-wide text-white/85">
                {{ card.statLabel }}
              </div>
            </div>

            <!-- Headline -->
            <h3 class="font-serif text-lg leading-snug font-normal text-white sm:text-xl">
              {{ card.headline }}
            </h3>

            <!-- Description -->
            <p class="text-xs leading-relaxed text-white/80 sm:text-sm">
              {{ card.description }}
            </p>
          </div>
        </div>
      </div>

      <!-- Growth Lab System Architecture Row -->
      <div
        v-reveal="'fade-up'"
        class="overflow-hidden rounded-3xl border border-gray-200 bg-white p-8 shadow-xs sm:p-12 lg:p-14"
      >
        <div class="mx-auto max-w-4xl space-y-8 text-center">
          <div class="space-y-3">
            <span
              class="inline-block rounded-full bg-[#04308F]/10 px-4 py-1.5 text-xs font-semibold tracking-widest text-[#04308F] uppercase"
            >
              The Interconnected Loop
            </span>

            <h3 class="font-serif text-3xl font-normal text-gray-900 sm:text-4xl">
              That's the <strong class="font-bold text-[#04308F]">Growth Lab.</strong>
            </h3>

            <p class="mx-auto max-w-2xl text-base leading-relaxed text-gray-600 sm:text-lg">
              Most agencies solve individual problems. You need the pieces to work together.
            </p>
          </div>

          <!-- 5 Steps Connected Visual Bar -->
          <div class="grid grid-cols-1 gap-4 pt-4 sm:grid-cols-2 md:grid-cols-3 lg:grid-cols-5">
            <div
              v-for="pillar in systemPillars"
              :key="pillar.title"
              class="group relative flex flex-col justify-between rounded-2xl border border-gray-100 bg-gray-50/70 p-5 text-left transition-all duration-300 hover:border-[#04308F]/30 hover:bg-white hover:shadow-md"
            >
              <div class="flex items-center justify-between pb-3">
                <span class="font-mono text-xs font-bold text-[#04308F]">
                  {{ pillar.step }}
                </span>
                <span class="size-1.5 rounded-full bg-[#05DED5]" />
              </div>
              <div class="space-y-1">
                <div
                  class="font-serif text-base font-semibold text-gray-900 group-hover:text-[#04308F]"
                >
                  {{ pillar.title }}
                </div>
                <div class="text-xs leading-relaxed text-gray-500">
                  {{ pillar.detail }}
                </div>
              </div>
            </div>
          </div>

          <!-- Bottom Callout Note & Action -->
          <div class="space-y-5 pt-4">
            <p class="mx-auto max-w-2xl text-sm leading-relaxed text-gray-500">
              A strategy that informs the brand. A brand that informs the marketing. Marketing that
              drives demand. Digital platforms that enable the business to deliver. And data that
              continuously informs what happens next.
            </p>

            <div>
              <NuxtLink
                to="/contact"
                class="inline-flex items-center gap-2 rounded-full bg-[#04308F] px-8 py-3.5 text-sm font-semibold text-white shadow-md shadow-[#04308F]/20 transition-all duration-300 hover:bg-[#05DED5] hover:text-gray-900"
              >
                Enter the Growth Lab <Icon icon="lucide:arrow-right" class="text-base" />
              </NuxtLink>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped lang="css"></style>
