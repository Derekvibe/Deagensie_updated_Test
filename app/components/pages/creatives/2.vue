<!--
  ==============================================================================
  CONFIGURATION GUIDE:
  - Brand variables: Change accent color in CSS tokens (--brand-accent: #04308F, #05DED5, #0F1E2E).
  - Headline & Subtitle: Configured in the template section header below.
  - Steps, Bullets & Preview Content: Fully typed and configured in the `steps` array in <script setup>.
  - Images: Configured per step on the right preview panel.
  - Rules: Zero em dashes used anywhere in copy, comments or code.
  ==============================================================================
-->

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue';

interface StepItem {
  id: string;
  stepNumber: string;
  title: string;
  description: string;
  bullets: string[];
  cardTitle: string;
  image: string;
  imageBadge: string;
}

// Typed steps array with user-provided Deagensie TaaS content and image assets
const steps: StepItem[] = [
  {
    id: 'talent-signals',
    stepNumber: 'STEP 1',
    title: 'Talent Signals',
    description: 'Our predictive matching engine considers multiple dimensions of talent.',
    bullets: [
      'Skills, experience and portfolio depth',
      'Specialization and industry exposure',
      'Availability, career interests and performance history',
    ],
    cardTitle: 'Talent Signals Architecture',
    image: '/images/pages/creatives/hero-1.png',
    imageBadge: 'Verified Creative Profile',
  },
  {
    id: 'opportunity-signals',
    stepNumber: 'STEP 2',
    title: 'Opportunity Signals',
    description: 'Comprehensive parsing of business requirements and engagement models.',
    bullets: [
      'Role requirements and required skills',
      'Industry, experience level and project type',
      'Location, remote requirements, timeline and engagement model',
    ],
    cardTitle: 'Opportunity Signals Matrix',
    image: '/images/pages/creatives/hero-2.png',
    imageBadge: 'Venture Opportunity Scope',
  },
  {
    id: 'predictive-intelligence',
    stepNumber: 'STEP 3',
    title: 'Predictive Intelligence',
    description: 'Matching beyond job titles and keywords to identify deep potential fit.',
    bullets: [
      'Traditional recruitment matches on keywords; TaaS goes deeper',
      'Multi-dimensional evaluation across talent and opportunity',
      'Contextual fit scoring replacing conventional hiring guesswork',
    ],
    cardTitle: 'Predictive Match Engine',
    image: '/images/pages/business/growth-system-2.jpg',
    imageBadge: 'Multi-Signal Synthesis',
  },
  {
    id: 'the-result',
    stepNumber: 'STEP 4',
    title: 'The Result',
    description: 'Better matching leads to better outcomes for businesses and creative talent.',
    bullets: [
      'Talent -> Opportunity precision alignment',
      'Opportunity -> Talent verified matchmaking',
      'Better Matching -> Better Outcomes',
    ],
    cardTitle: 'Matched Engagement Result',
    image: '/images/works/lw-registry/showcase.webp',
    imageBadge: 'Global Engagement Confirmed',
  },
];

// Active step state
const activeIndex = ref<number>(0);
const isAutoPlaying = ref<boolean>(true);

// Timers
let autoPlayTimer: ReturnType<typeof setInterval> | null = null;
let hoverTimeout: ReturnType<typeof setTimeout> | null = null;

// Stop auto-play permanently on user interaction
const stopAutoPlay = () => {
  if (isAutoPlaying.value) {
    isAutoPlaying.value = false;
    if (autoPlayTimer) {
      clearInterval(autoPlayTimer);
      autoPlayTimer = null;
    }
  }
};

// Select step manually
const selectStep = (idx: number, stopAuto = true) => {
  if (stopAuto) stopAutoPlay();
  activeIndex.value = idx;
};

// Hover intent with 80ms delay to prevent flicker
const onRowMouseEnter = (idx: number) => {
  if (hoverTimeout) clearTimeout(hoverTimeout);
  hoverTimeout = setTimeout(() => {
    selectStep(idx, true);
  }, 80);
};

const onRowMouseLeave = () => {
  if (hoverTimeout) {
    clearTimeout(hoverTimeout);
    hoverTimeout = null;
  }
};

// Keyboard navigation (Arrow Up / Arrow Down)
const navigateStep = (direction: number) => {
  stopAutoPlay();
  const nextIdx = (activeIndex.value + direction + steps.length) % steps.length;
  activeIndex.value = nextIdx;
  const targetButton = document.getElementById(`step-tab-${nextIdx}`);
  if (targetButton) targetButton.focus();
};

onMounted(() => {
  // Auto-play: advance every 6 seconds if user has not interacted
  autoPlayTimer = setInterval(() => {
    if (isAutoPlaying.value) {
      activeIndex.value = (activeIndex.value + 1) % steps.length;
    }
  }, 6000);
});

onBeforeUnmount(() => {
  if (autoPlayTimer) clearInterval(autoPlayTimer);
  if (hoverTimeout) clearTimeout(hoverTimeout);
});
</script>

<template>
  <section class="border-b border-gray-100 bg-white py-20 text-gray-900 sm:py-24 lg:py-28">
    <div class="mx-auto w-5/6 max-w-7xl">
      <!-- Section Header (Centered, max-w-4xl) -->
      <div v-reveal="'fade-up'" class="mx-auto max-w-3xl text-center">
        <!-- Eyebrow: Tiny uppercase pill with light grey background -->
        <span
          class="inline-block rounded-md bg-gray-100 px-3.5 py-1 text-[11px] font-semibold tracking-wider text-gray-600 uppercase"
        >
          Deagensie TaaS Engine • Powered by Predictive Intelligence
        </span>

        <!-- Headline: Two lines, serif, large -->
        <h2
          class="mt-4 font-serif text-3xl leading-tight font-normal tracking-tight text-gray-900 sm:text-4xl lg:text-5xl"
        >
          Matching Beyond Keywords.
        </h2>

        <!-- Subtitle: Small muted, two lines -->
        <p
          class="mx-auto mt-4 max-w-2xl text-sm leading-relaxed font-normal text-gray-500 sm:text-base"
        >
          Traditional recruitment often matches people based on job titles and keywords. TaaS is
          designed to go deeper. Our predictive matching engine considers multiple dimensions of
          both talent and opportunity to identify potential fit.
        </p>

        <!-- CTA Button Under Header -->
        <div class="mt-7 flex justify-center">
          <NuxtLink
            to="https://app-deagensie-waitlist.vercel.app/"
            target="_blank"
            rel="noopener noreferrer"
            class="inline-flex items-center justify-center rounded-full bg-[#0F1E2E] px-8 py-3.5 text-sm font-medium text-white shadow-md shadow-gray-900/10 transition-all duration-300 hover:bg-[#04308F] hover:shadow-lg focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-[#04308F]"
          >
            Start your venture
          </NuxtLink>
        </div>
      </div>

      <!-- Main Layout: 2 Columns (~45% / ~55%), 40px gap, top aligned. Stack under 900px -->
      <div class="mt-14 grid grid-cols-1 items-start gap-10 lg:grid-cols-12 lg:gap-10">
        <!-- LEFT COLUMN: Accordion list (~45% width, lg:col-span-5) -->
        <div
          class="flex flex-col border-y border-gray-200 lg:col-span-5"
          role="tablist"
          aria-label="Deagensie TaaS Engine Stages"
        >
          <div
            v-for="(st, idx) in steps"
            :key="st.id"
            class="border-b border-gray-200 last:border-b-0"
          >
            <!-- Row Button Trigger -->
            <button
              :id="'step-tab-' + idx"
              type="button"
              role="tab"
              :aria-selected="activeIndex === idx"
              :aria-controls="'preview-panel-' + idx"
              class="group relative flex w-full items-center justify-between py-4.5 text-left transition-colors duration-200 focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-[#04308F]"
              @click="selectStep(idx, true)"
              @mouseenter="onRowMouseEnter(idx)"
              @mouseleave="onRowMouseLeave"
              @keydown.down.prevent="navigateStep(1)"
              @keydown.up.prevent="navigateStep(-1)"
              @keydown.enter.prevent="selectStep(idx, true)"
              @keydown.space.prevent="selectStep(idx, true)"
            >
              <div class="flex items-center gap-3.5">
                <!-- Step Chip with Auto-play Progress Line -->
                <div
                  class="relative overflow-hidden rounded-md px-2 py-0.5 transition-colors duration-200"
                  :class="
                    activeIndex === idx
                      ? 'bg-[#04308F]/10 text-[#04308F]'
                      : 'bg-gray-100 text-gray-500'
                  "
                >
                  <span class="font-mono text-[10px] font-semibold tracking-wider uppercase">
                    {{ st.stepNumber }}
                  </span>
                  <!-- Thin progress line during auto-play -->
                  <span
                    v-if="isAutoPlaying && activeIndex === idx"
                    class="autoplay-progress absolute bottom-0 left-0 h-[2px] w-full bg-[#04308F]"
                  ></span>
                </div>

                <!-- Step Title -->
                <span
                  class="text-lg font-medium transition-colors duration-200"
                  :class="
                    activeIndex === idx
                      ? 'font-semibold text-gray-900'
                      : 'text-gray-500 group-hover:text-gray-800'
                  "
                >
                  {{ st.title }}
                </span>
              </div>

              <!-- Chevron indicator -->
              <svg
                class="size-4 shrink-0 transition-transform duration-300"
                :class="
                  activeIndex === idx
                    ? 'rotate-180 text-gray-900'
                    : 'text-gray-400 group-hover:text-gray-600'
                "
                viewBox="0 0 20 20"
                fill="currentColor"
              >
                <path
                  fill-rule="evenodd"
                  d="M5.293 7.293a1 1 0 011.414 0L10 10.586l3.293-3.293a1 1 0 111.414 1.414l-4 4a1 1 0 01-1.414 0l-4-4a1 1 0 010-1.414z"
                  clip-rule="evenodd"
                />
              </svg>
            </button>

            <!-- Accordion Content (Smooth Grid Height Animation) -->
            <div class="accordion-content" :class="{ 'is-open': activeIndex === idx }">
              <div class="accordion-inner">
                <div class="pt-1 pr-2 pb-5 pl-1">
                  <!-- Description line -->
                  <p class="text-sm leading-relaxed text-gray-500">
                    {{ st.description }}
                  </p>

                  <!-- 3 Bullets with inline SVG check icons -->
                  <ul class="mt-3.5 space-y-2 text-xs text-gray-700">
                    <li
                      v-for="(bullet, bIdx) in st.bullets"
                      :key="bIdx"
                      class="flex items-start gap-2.5 leading-snug"
                    >
                      <svg
                        class="mt-0.5 size-4 shrink-0 text-[#04308F]"
                        viewBox="0 0 20 20"
                        fill="currentColor"
                      >
                        <path
                          fill-rule="evenodd"
                          d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z"
                          clip-rule="evenodd"
                        />
                      </svg>
                      <span>{{ bullet }}</span>
                    </li>
                  </ul>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- RIGHT COLUMN: Large Rounded Panel with Fixed Height (~55% width, lg:col-span-7) -->
        <div
          :id="'preview-panel-' + activeIndex"
          class="relative flex h-[560px] w-full items-center justify-center overflow-hidden rounded-[24px] border border-gray-200/80 bg-[#FAFAFA] p-6 shadow-xs sm:p-8 lg:col-span-7"
          role="tabpanel"
          :aria-labelledby="'step-tab-' + activeIndex"
        >
          <!-- Animated Preview Card (Transition with slide + fade) -->
          <Transition name="card-slide" mode="out-in">
            <!-- 01: Talent Signals Card (With Creative Image) -->
            <div
              v-if="activeIndex === 0"
              key="panel-0"
              class="w-full max-w-[460px] rounded-[16px] border border-gray-200/90 bg-white p-5 shadow-[0_8px_30px_rgba(0,0,0,0.05)] sm:p-6"
            >
              <!-- Card Header Row -->
              <div class="flex items-center justify-between border-b border-gray-100 pb-3">
                <div class="flex items-center gap-2">
                  <span class="flex size-2 rounded-full bg-[#04308F]"></span>
                  <h4 class="text-sm font-semibold text-gray-900">{{ steps[0].cardTitle }}</h4>
                </div>
                <span
                  class="rounded-full bg-[#04308F]/10 px-2 py-0.5 text-[10px] font-semibold text-[#04308F]"
                >
                  8 Signals Active
                </span>
              </div>

              <!-- Visual Photo Banner -->
              <div
                class="relative mt-3.5 h-24 w-full overflow-hidden rounded-xl border border-gray-100 bg-slate-100 sm:h-28"
              >
                <NuxtImg
                  :src="steps[0].image"
                  alt="Talent Signals Visual"
                  class="size-full object-cover object-[50%_15%]"
                />
                <div
                  class="absolute inset-0 bg-gradient-to-t from-gray-900/60 via-transparent to-transparent"
                ></div>
                <span
                  class="absolute bottom-2 left-2.5 rounded-md bg-white/95 px-2 py-0.5 text-[10px] font-semibold text-gray-800 shadow-xs"
                >
                  {{ steps[0].imageBadge }}
                </span>
              </div>

              <!-- Body: Talent Signals 8 Dimensions -->
              <div class="mt-3.5 space-y-2.5">
                <div class="grid grid-cols-2 gap-1.5 text-[11px] sm:text-xs">
                  <div
                    class="rounded-lg border border-gray-100 bg-[#FAFAFA] px-2.5 py-1.5 text-gray-800"
                  >
                    ✓ Skills
                  </div>
                  <div
                    class="rounded-lg border border-gray-100 bg-[#FAFAFA] px-2.5 py-1.5 text-gray-800"
                  >
                    ✓ Experience
                  </div>
                  <div
                    class="rounded-lg border border-gray-100 bg-[#FAFAFA] px-2.5 py-1.5 text-gray-800"
                  >
                    ✓ Portfolio
                  </div>
                  <div
                    class="rounded-lg border border-gray-100 bg-[#FAFAFA] px-2.5 py-1.5 text-gray-800"
                  >
                    ✓ Specialization
                  </div>
                  <div
                    class="rounded-lg border border-gray-100 bg-[#FAFAFA] px-2.5 py-1.5 text-gray-800"
                  >
                    ✓ Industry exposure
                  </div>
                  <div
                    class="rounded-lg border border-gray-100 bg-[#FAFAFA] px-2.5 py-1.5 text-gray-800"
                  >
                    ✓ Availability
                  </div>
                  <div
                    class="rounded-lg border border-gray-100 bg-[#FAFAFA] px-2.5 py-1.5 text-gray-800"
                  >
                    ✓ Career interests
                  </div>
                  <div
                    class="rounded-lg border border-gray-100 bg-[#FAFAFA] px-2.5 py-1.5 text-gray-800"
                  >
                    ✓ Performance history
                  </div>
                </div>

                <div
                  class="rounded-lg border border-gray-100 bg-gray-50/70 p-2 text-center text-[10px] text-gray-500 sm:text-[11px]"
                >
                  Comprehensive profile readiness index calculated
                </div>
              </div>
            </div>

            <!-- 02: Opportunity Signals Card (With Venture Image) -->
            <div
              v-else-if="activeIndex === 1"
              key="panel-1"
              class="w-full max-w-[460px] rounded-[16px] border border-gray-200/90 bg-white p-5 shadow-[0_8px_30px_rgba(0,0,0,0.05)] sm:p-6"
            >
              <!-- Card Header Row -->
              <div class="flex items-center justify-between border-b border-gray-100 pb-3">
                <div class="flex items-center gap-2">
                  <span class="flex size-2 rounded-full bg-[#04308F]"></span>
                  <h4 class="text-sm font-semibold text-gray-900">{{ steps[1].cardTitle }}</h4>
                </div>
                <span
                  class="rounded-full bg-[#04308F]/10 px-2 py-0.5 text-[10px] font-semibold text-[#04308F]"
                >
                  8 Criteria Scoped
                </span>
              </div>

              <!-- Visual Photo Banner -->
              <div
                class="relative mt-3.5 h-24 w-full overflow-hidden rounded-xl border border-gray-100 bg-slate-100 sm:h-28"
              >
                <NuxtImg
                  :src="steps[1].image"
                  alt="Opportunity Signals Visual"
                  class="size-full object-cover object-center"
                />
                <div
                  class="absolute inset-0 bg-gradient-to-t from-gray-900/60 via-transparent to-transparent"
                ></div>
                <span
                  class="absolute bottom-2 left-2.5 rounded-md bg-white/95 px-2 py-0.5 text-[10px] font-semibold text-gray-800 shadow-xs"
                >
                  {{ steps[1].imageBadge }}
                </span>
              </div>

              <!-- Body: Opportunity Signals 8 Dimensions -->
              <div class="mt-3.5 space-y-2.5">
                <div class="grid grid-cols-2 gap-1.5 text-[11px] sm:text-xs">
                  <div
                    class="rounded-lg border border-gray-100 bg-[#FAFAFA] px-2.5 py-1.5 text-gray-800"
                  >
                    Role requirements
                  </div>
                  <div
                    class="rounded-lg border border-gray-100 bg-[#FAFAFA] px-2.5 py-1.5 text-gray-800"
                  >
                    Required skills
                  </div>
                  <div
                    class="rounded-lg border border-gray-100 bg-[#FAFAFA] px-2.5 py-1.5 text-gray-800"
                  >
                    Industry domain
                  </div>
                  <div
                    class="rounded-lg border border-gray-100 bg-[#FAFAFA] px-2.5 py-1.5 text-gray-800"
                  >
                    Experience level
                  </div>
                  <div
                    class="rounded-lg border border-gray-100 bg-[#FAFAFA] px-2.5 py-1.5 text-gray-800"
                  >
                    Project type
                  </div>
                  <div
                    class="rounded-lg border border-gray-100 bg-[#FAFAFA] px-2.5 py-1.5 text-gray-800"
                  >
                    Remote requirements
                  </div>
                  <div
                    class="rounded-lg border border-gray-100 bg-[#FAFAFA] px-2.5 py-1.5 text-gray-800"
                  >
                    Timeline & sprints
                  </div>
                  <div
                    class="rounded-lg border border-gray-100 bg-[#FAFAFA] px-2.5 py-1.5 text-gray-800"
                  >
                    Engagement model
                  </div>
                </div>

                <div
                  class="rounded-lg border border-gray-100 bg-gray-50/70 p-2 text-center text-[10px] text-gray-500 sm:text-[11px]"
                >
                  Target criteria aligned to verified venture mandates
                </div>
              </div>
            </div>

            <!-- 03: Predictive Intelligence Card (With Neural Network Image) -->
            <div
              v-else-if="activeIndex === 2"
              key="panel-2"
              class="w-full max-w-[460px] rounded-[16px] border border-gray-200/90 bg-white p-5 shadow-[0_8px_30px_rgba(0,0,0,0.05)] sm:p-6"
            >
              <!-- Card Header Row -->
              <div class="flex items-center justify-between border-b border-gray-100 pb-3">
                <div class="flex items-center gap-2">
                  <span class="flex size-2 rounded-full bg-[#04308F]"></span>
                  <h4 class="text-sm font-semibold text-gray-900">{{ steps[2].cardTitle }}</h4>
                </div>
                <span
                  class="rounded-full bg-[#04308F]/10 px-2 py-0.5 text-[10px] font-semibold text-[#04308F]"
                >
                  Score: 98%
                </span>
              </div>

              <!-- Visual Neural Network Banner -->
              <div
                class="relative mt-3.5 h-24 w-full overflow-hidden rounded-xl border border-gray-100 bg-slate-900 sm:h-28"
              >
                <NuxtImg
                  :src="steps[2].image"
                  alt="Predictive Intelligence Visual"
                  class="size-full object-cover object-center opacity-85"
                />
                <div
                  class="absolute inset-0 bg-gradient-to-t from-gray-950/70 via-transparent to-transparent"
                ></div>
                <span
                  class="absolute bottom-2 left-2.5 rounded-md bg-white/95 px-2 py-0.5 text-[10px] font-semibold text-gray-800 shadow-xs"
                >
                  {{ steps[2].imageBadge }}
                </span>
              </div>

              <!-- Body: Matching Engine Score & Ring -->
              <div class="mt-3.5 space-y-3">
                <div
                  class="flex items-center justify-between rounded-xl border border-gray-100 bg-[#FAFAFA] p-3"
                >
                  <div>
                    <p class="text-[10px] font-semibold tracking-wider text-gray-400 uppercase">
                      Predictive Fit Index
                    </p>
                    <p class="mt-0.5 text-sm font-bold text-gray-900">High Confidence Match</p>
                  </div>
                  <!-- SVG Circular Score Ring -->
                  <div class="relative flex size-12 items-center justify-center">
                    <svg class="size-12 -rotate-90" viewBox="0 0 36 36">
                      <path
                        class="text-gray-200"
                        stroke-width="3.5"
                        stroke="currentColor"
                        fill="none"
                        d="M18 2.0845 a 15.9155 15.9155 0 0 1 0 31.831 a 15.9155 15.9155 0 0 1 0 -31.831"
                      />
                      <path
                        class="text-[#04308F]"
                        stroke-dasharray="98, 100"
                        stroke-width="3.5"
                        stroke-linecap="round"
                        stroke="currentColor"
                        fill="none"
                        d="M18 2.0845 a 15.9155 15.9155 0 0 1 0 31.831 a 15.9155 15.9155 0 0 1 0 -31.831"
                      />
                    </svg>
                    <span class="absolute text-[11px] font-bold text-gray-900">98%</span>
                  </div>
                </div>

                <div class="space-y-1.5 text-xs">
                  <div class="flex items-center justify-between text-[11px] text-gray-500">
                    <span>Keyword Matching</span>
                    <span class="font-mono text-gray-400">Surface Filters</span>
                  </div>
                  <div
                    class="flex items-center justify-between text-[11px] font-medium text-[#04308F]"
                  >
                    <span>TaaS Multi-Dimensional</span>
                    <span class="font-mono">Deep Contextual Fit</span>
                  </div>
                </div>
              </div>
            </div>

            <!-- 04: The Result Card (With Collaboration Image) -->
            <div
              v-else-if="activeIndex === 3"
              key="panel-3"
              class="w-full max-w-[460px] rounded-[16px] border border-gray-200/90 bg-white p-5 shadow-[0_8px_30px_rgba(0,0,0,0.05)] sm:p-6"
            >
              <!-- Card Header Row -->
              <div class="flex items-center justify-between border-b border-gray-100 pb-3">
                <div class="flex items-center gap-2">
                  <span class="flex size-2 rounded-full bg-[#04308F]"></span>
                  <h4 class="text-sm font-semibold text-gray-900">{{ steps[3].cardTitle }}</h4>
                </div>
                <span
                  class="rounded-full border border-emerald-200 bg-emerald-50 px-2 py-0.5 text-[10px] font-semibold text-emerald-700"
                >
                  Outcome Verified
                </span>
              </div>

              <!-- Visual Photo Banner -->
              <div
                class="relative mt-3.5 h-24 w-full overflow-hidden rounded-xl border border-gray-100 bg-slate-100 sm:h-28"
              >
                <NuxtImg
                  :src="steps[3].image"
                  alt="Engagement Outcome Visual"
                  class="size-full object-cover object-center"
                />
                <div
                  class="absolute inset-0 bg-gradient-to-t from-gray-900/60 via-transparent to-transparent"
                ></div>
                <span
                  class="absolute bottom-2 left-2.5 rounded-md bg-white/95 px-2 py-0.5 text-[10px] font-semibold text-gray-800 shadow-xs"
                >
                  {{ steps[3].imageBadge }}
                </span>
              </div>

              <!-- Body: Result outcome matching user copy -->
              <div class="mt-3.5 space-y-2.5">
                <!-- Two-Way Directional Results -->
                <div class="space-y-1.5 text-[11px] sm:text-xs">
                  <div
                    class="flex items-center justify-between rounded-lg border border-gray-100 bg-[#FAFAFA] px-2.5 py-1.5"
                  >
                    <span class="font-medium text-gray-800">Talent -> Opportunity</span>
                    <span class="font-semibold text-[#04308F]">Aligned</span>
                  </div>
                  <div
                    class="flex items-center justify-between rounded-lg border border-gray-100 bg-[#FAFAFA] px-2.5 py-1.5"
                  >
                    <span class="font-medium text-gray-800">Opportunity -> Talent</span>
                    <span class="font-semibold text-[#04308F]">Aligned</span>
                  </div>
                  <div
                    class="flex items-center justify-between rounded-lg border border-blue-100 bg-[#04308F]/5 px-2.5 py-1.5"
                  >
                    <span class="font-bold text-gray-900">Better Matching -> Better Outcomes</span>
                    <span class="font-bold text-[#04308F]">Verified</span>
                  </div>
                </div>

                <!-- Action Buttons -->
                <div class="flex gap-2 pt-1">
                  <NuxtLink
                    to="https://app-deagensie-waitlist.vercel.app/"
                    target="_blank"
                    rel="noopener noreferrer"
                    class="flex-1 rounded-lg bg-[#0F1E2E] py-2 text-center text-xs font-semibold text-white transition-colors hover:bg-[#04308F]"
                  >
                    Accept Engagement
                  </NuxtLink>
                  <NuxtLink
                    to="/business/taas"
                    class="rounded-lg border border-gray-200 bg-white px-3.5 py-2 text-center text-xs font-semibold text-gray-700 transition-colors hover:border-[#04308F] hover:text-[#04308F]"
                  >
                    View Details
                  </NuxtLink>
                </div>
              </div>
            </div>
          </Transition>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped>
/* Smooth Grid-Template-Rows Height Animation for Accordion */
.accordion-content {
  display: grid;
  grid-template-rows: 0fr;
  transition: grid-template-rows 350ms cubic-bezier(0.16, 1, 0.3, 1);
}

.accordion-content.is-open {
  grid-template-rows: 1fr;
}

.accordion-inner {
  overflow: hidden;
  min-height: 0;
  transition: opacity 300ms ease-out;
}

/* Auto-play progress bar */
@keyframes progressWidth {
  from {
    width: 0%;
  }
  to {
    width: 100%;
  }
}

.autoplay-progress {
  animation: progressWidth 6000ms linear infinite;
}

/* Preview Card Transitions (slide up 8px on leave, slide in from 12px below on enter) */
.card-slide-enter-active,
.card-slide-leave-active {
  transition:
    opacity 350ms ease-out,
    transform 350ms cubic-bezier(0.16, 1, 0.3, 1);
}

.card-slide-enter-from {
  opacity: 0;
  transform: translateY(12px);
}

.card-slide-leave-to {
  opacity: 0;
  transform: translateY(-8px);
}

/* Accessibility: Respect prefers-reduced-motion */
@media (prefers-reduced-motion: reduce) {
  .accordion-content {
    transition: none;
  }
  .card-slide-enter-active,
  .card-slide-leave-active {
    transition: opacity 200ms ease;
    transform: none !important;
  }
  .card-slide-enter-from,
  .card-slide-leave-to {
    opacity: 0;
    transform: none !important;
  }
  .autoplay-progress {
    animation: none;
  }
}
</style>
