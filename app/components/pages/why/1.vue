<script setup lang="ts">
import { Icon } from '@iconify/vue';

interface GrowthLayer {
  number: string;
  title: string;
  tagline: string;
  description: string;
  deliverableType: string;
  deliverables: string[];
  footerNote?: string;
}

const layers: GrowthLayer[] = [
  {
    number: '/01',
    title: 'Brand Pillars',
    tagline: 'Transform ideas into profitable, technology-driven brands.',
    description:
      'We help ambitious businesses transform ideas into profitable, technology-driven brands through a disciplined strategic framework:',
    deliverableType: 'Core Pillars:',
    deliverables: [
      'Strategy First',
      'Human-Centered Design',
      'AI-Powered Innovation',
      'Technology & Automation',
      'Measurable Business Growth',
    ],
  },
  {
    number: '/02',
    title: 'AI-Powered Decision Making',
    tagline: 'Your brand continuously learns, evolves and grows.',
    description:
      'We embed artificial intelligence into your growth engine to inform decisions and optimize performance across every touchpoint:',
    deliverableType: 'We Leverage AI To:',
    deliverables: [
      'Predict customer behavior',
      'Analyze market trends',
      'Improve campaign performance',
      'Optimize brand positioning',
      'Generate actionable business insights',
    ],
    footerNote: 'Your brand continuously learns, evolves and grows.',
  },
];

// Active card index on desktop (null by default so all cards start closed in moderate height)
const activeIndex = ref<number | null>(null);

const selectLayer = (idx: number) => {
  activeIndex.value = activeIndex.value === idx ? null : idx;
};

// Split deliverables into two columns for desktop flex layout
const getCol1 = (items: string[]) => items.slice(0, Math.ceil(items.length / 2));
const getCol2 = (items: string[]) => items.slice(Math.ceil(items.length / 2));

// Mobile expanded card tracking
const mobileActiveIndex = ref<number | null>(null);

const toggleMobileExpand = (idx: number) => {
  mobileActiveIndex.value = mobileActiveIndex.value === idx ? null : idx;
};
</script>

<template>
  <section
    id="model"
    class="border-b border-gray-100 bg-white py-20 text-gray-900 sm:py-24 lg:py-24"
  >
    <div class="mx-auto w-5/6 max-w-7xl space-y-12 sm:space-y-16">
      <!-- Section Header -->
      <div v-reveal="'fade-up'" class="mx-auto max-w-3xl space-y-4 text-center">
        <p class="text-xs font-semibold tracking-widest text-[#04308F] uppercase sm:text-sm">
          Integrated Growth Ecosystem
        </p>
        <h2
          class="font-serif text-3xl leading-tight font-normal tracking-tight text-gray-900 sm:text-4xl lg:text-5xl"
        >
          What Makes <span class="text-[#04308F]">Us Different?</span>
        </h2>
        <p
          class="font-open-sans mx-auto max-w-2xl text-center text-base leading-relaxed font-normal text-gray-600 sm:text-lg"
        >
          Deagensie combines business strategy, brand development, AI-Driven marketing intelligence,
          digital innovation, and talent-as-a-service into one integrated growth ecosystem.
        </p>
      </div>

      <!-- ============================================================ -->
      <!-- DESKTOP SCREEN: Horizontal Row with Moderate Height & Expand -->
      <!-- ============================================================ -->
      <div class="hidden lg:flex lg:flex-row lg:items-stretch lg:gap-6">
        <div
          v-for="(layer, idx) in layers"
          :key="layer.title"
          v-reveal="{ animation: 'fade-up', delay: idx * 80 }"
          class="group relative flex min-h-[230px] flex-col justify-between rounded-2xl transition-all duration-500 ease-out"
          :class="[
            activeIndex === idx
              ? 'cursor-pointer bg-[#0F1E2E] p-8 text-white shadow-xl lg:flex-[1.6]'
              : 'cursor-pointer border border-gray-200/90 bg-white p-7 text-gray-900 shadow-2xs hover:border-gray-300 hover:shadow-md lg:flex-1',
          ]"
          @click="selectLayer(idx)"
        >
          <!-- Top Card Header & Content Area -->
          <div>
            <!-- Layer Index: /01, /02 -->
            <div
              class="font-mono text-xs font-normal tracking-wider sm:text-sm"
              :class="activeIndex === idx ? 'text-gray-400' : 'text-gray-400'"
            >
              {{ layer.number }}
            </div>

            <!-- Inactive / Closed State Layout: Moderate height, clean and compact -->
            <div v-if="activeIndex !== idx" class="space-y-3 pt-5">
              <h3
                class="font-serif text-2xl leading-snug font-normal text-gray-900 transition-colors group-hover:text-[#04308F] sm:text-3xl"
              >
                {{ layer.title }}
              </h3>
              <p class="text-xs leading-relaxed text-gray-500 sm:text-sm">
                {{ layer.tagline }}
              </p>
            </div>

            <!-- Active / Opened State Layout: 2-Column checklist -->
            <div v-else class="space-y-4 pt-3">
              <h3 class="font-serif text-2xl leading-snug font-bold text-white sm:text-3xl">
                {{ layer.title }}
              </h3>
              <p class="text-xs font-medium text-[#05DED5] sm:text-sm">
                {{ layer.tagline }}
              </p>
              <p class="pt-0.5 pb-2 text-xs leading-relaxed text-gray-300 sm:text-sm">
                {{ layer.description }}
              </p>

              <!-- Deliverables Checklist: 2 Columns -->
              <div class="space-y-3 border-t border-white/10 pt-4">
                <div class="text-[11px] font-bold tracking-wider text-gray-400 uppercase">
                  {{ layer.deliverableType }}
                </div>
                <div class="grid grid-cols-2 gap-x-6 gap-y-2">
                  <!-- Left Column -->
                  <ul class="space-y-2 text-xs text-gray-100 sm:text-sm">
                    <li
                      v-for="item in getCol1(layer.deliverables)"
                      :key="item"
                      class="flex items-start gap-2 leading-tight"
                    >
                      <Icon icon="lucide:check" class="mt-0.5 size-4 shrink-0 text-emerald-400" />
                      <span>{{ item }}</span>
                    </li>
                  </ul>
                  <!-- Right Column -->
                  <ul class="space-y-2 text-xs text-gray-100 sm:text-sm">
                    <li
                      v-for="item in getCol2(layer.deliverables)"
                      :key="item"
                      class="flex items-start gap-2 leading-tight"
                    >
                      <Icon icon="lucide:check" class="mt-0.5 size-4 shrink-0 text-emerald-400" />
                      <span>{{ item }}</span>
                    </li>
                  </ul>
                </div>
              </div>

              <!-- Footer Note -->
              <div
                v-if="layer.footerNote"
                class="mt-4 flex items-center gap-2 rounded-xl border border-white/10 bg-white/5 px-4 py-2.5 text-xs font-medium text-[#05DED5]"
              >
                <Icon icon="lucide:sparkles" class="size-4 shrink-0" />
                <span>{{ layer.footerNote }}</span>
              </div>
            </div>
          </div>

          <!-- Bottom Area: Plus/Minus Button Indicator -->
          <div class="pt-6">
            <div
              v-if="activeIndex !== idx"
              class="flex size-7 items-center justify-center rounded-full border border-gray-300 text-gray-700 transition-all duration-300 group-hover:scale-105 group-hover:border-gray-900 group-hover:text-gray-900"
            >
              <Icon icon="lucide:plus" class="size-4" />
            </div>
            <div
              v-else
              class="flex size-7 items-center justify-center rounded-full border border-white/30 text-white transition-all duration-300 group-hover:scale-105 group-hover:border-white"
            >
              <Icon icon="lucide:minus" class="size-4" />
            </div>
          </div>
        </div>
      </div>

      <!-- ============================================================ -->
      <!-- SMALLER SCREEN: Moderate Height Closed Cards & Tap to Open   -->
      <!-- ============================================================ -->
      <div class="flex flex-col gap-4 sm:gap-5 lg:hidden">
        <div
          v-for="(layer, idx) in layers"
          :key="layer.title"
          v-reveal="{ animation: 'fade-up', delay: idx * 60 }"
          class="group relative flex cursor-pointer flex-col justify-between rounded-2xl p-6 transition-all duration-300 sm:p-7"
          :class="[
            mobileActiveIndex === idx
              ? 'bg-[#0F1E2E] text-white shadow-xl ring-1 ring-white/10'
              : 'border border-gray-200/90 bg-white text-gray-900 shadow-2xs hover:border-gray-300 hover:shadow-md',
          ]"
          @click="toggleMobileExpand(idx)"
        >
          <!-- Card Content Area -->
          <div class="space-y-3">
            <!-- Index Tag -->
            <div
              class="font-mono text-xs font-normal tracking-wider sm:text-sm"
              :class="mobileActiveIndex === idx ? 'text-gray-400' : 'text-gray-400'"
            >
              {{ layer.number }}
            </div>

            <!-- Title & Tagline -->
            <div>
              <h3
                class="font-serif text-xl leading-snug font-bold sm:text-2xl"
                :class="mobileActiveIndex === idx ? 'text-white' : 'text-gray-900'"
              >
                {{ layer.title }}
              </h3>
              <p
                class="mt-1 text-xs font-medium sm:text-sm"
                :class="mobileActiveIndex === idx ? 'text-[#05DED5]' : 'text-[#04308F]'"
              >
                {{ layer.tagline }}
              </p>
            </div>

            <!-- Opened State: Description & Full Deliverables -->
            <div v-if="mobileActiveIndex === idx" class="space-y-3 pt-1">
              <!-- Narrative Description -->
              <p class="text-xs leading-relaxed text-gray-300 sm:text-sm">
                {{ layer.description }}
              </p>

              <!-- Deliverables Section -->
              <div class="space-y-2 border-t border-white/10 pt-3">
                <div class="text-[11px] font-bold tracking-wider text-gray-400 uppercase">
                  {{ layer.deliverableType }}
                </div>
                <div
                  class="grid grid-cols-1 gap-2 pt-1 text-xs text-gray-100 sm:grid-cols-2 sm:text-sm"
                >
                  <ul class="space-y-2">
                    <li
                      v-for="item in getCol1(layer.deliverables)"
                      :key="item"
                      class="flex items-start gap-2 leading-tight"
                    >
                      <Icon icon="lucide:check" class="mt-0.5 size-4 shrink-0 text-emerald-400" />
                      <span>{{ item }}</span>
                    </li>
                  </ul>
                  <ul class="space-y-2">
                    <li
                      v-for="item in getCol2(layer.deliverables)"
                      :key="item"
                      class="flex items-start gap-2 leading-tight"
                    >
                      <Icon icon="lucide:check" class="mt-0.5 size-4 shrink-0 text-emerald-400" />
                      <span>{{ item }}</span>
                    </li>
                  </ul>
                </div>
              </div>

              <!-- Footer Note -->
              <div
                v-if="layer.footerNote"
                class="mt-3 flex items-center gap-2 rounded-xl border border-white/10 bg-white/5 px-3 py-2 text-xs font-medium text-[#05DED5]"
              >
                <Icon icon="lucide:sparkles" class="size-4 shrink-0" />
                <span>{{ layer.footerNote }}</span>
              </div>
            </div>
          </div>

          <!-- Bottom Expand/Collapse Indicator Button -->
          <div class="flex items-center justify-between pt-5">
            <div
              v-if="mobileActiveIndex !== idx"
              class="flex size-7 items-center justify-center rounded-full border border-gray-300 text-gray-700 transition-transform group-hover:scale-105"
            >
              <Icon icon="lucide:plus" class="size-4" />
            </div>
            <div
              v-else
              class="flex size-7 items-center justify-center rounded-full border border-white/30 text-white transition-transform group-hover:scale-105"
            >
              <Icon icon="lucide:minus" class="size-4" />
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped lang="css"></style>
