<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue';

interface IndustryCluster {
  id: string;
  stepNumber: string;
  title: string;
  description: string;
  bullets: string[];
  cardTitle: string;
  image: string;
  imageBadge: string;
  sectors: string[];
  highlightText: string;
}

const clusters: IndustryCluster[] = [
  {
    id: 'tech-fintech',
    stepNumber: 'STEP 1',
    title: 'Technology & FinTech',
    description: 'Scalable software architectures, modern FinTech rails, and digital storefronts.',
    bullets: [
      'Enterprise software, AI applications, and SaaS platform engineering',
      'FinTech financial systems, compliance infrastructure, and user trust',
      'High-conversion E-Commerce storefronts and digital consumer journeys',
    ],
    cardTitle: 'Digital & Financial Ecosystems',
    image: '/images/pages/why/hero-4.png',
    imageBadge: 'High-Velocity Scale',
    sectors: ['Technology', 'FinTech', 'E-Commerce', 'Startups'],
    highlightText: 'Intelligent digital platforms engineered for rapid market adoption',
  },
  {
    id: 'healthcare-agri-edu',
    stepNumber: 'STEP 2',
    title: 'Healthcare, Agri & Education',
    description: 'Transforming foundational life-sciences, agrarian systems, and digital learning.',
    bullets: [
      'Digital healthcare platforms, patient journeys, and clinical trust',
      'AgriTech value chain systems, data intelligence, and market linkages',
      'EdTech platforms, institutional systems, and interactive learning',
    ],
    cardTitle: 'Foundational Sectors Architecture',
    image: '/images/pages/why/hero-2.png',
    imageBadge: 'Mission-Critical Systems',
    sectors: ['Healthcare', 'Agriculture', 'Education', 'NGOs'],
    highlightText: 'Mission-critical systems built for resilience, compliance, and human impact',
  },
  {
    id: 'real-estate-gov',
    stepNumber: 'STEP 3',
    title: 'Real Estate, Gov & Advisory',
    description: 'High-trust property development, civic governance, and professional advisory.',
    bullets: [
      'PropTech platforms, luxury development branding, and investor portals',
      'Government digital services, civic transparency, and public trust',
      'Strategic market positioning for professional services and corporate legal advisory',
    ],
    cardTitle: 'Institutional & Real Assets',
    image: '/images/pages/why/hero-3.png',
    imageBadge: 'Institutional Grade',
    sectors: ['Real Estate', 'Government', 'Professional Services', 'NGOs'],
    highlightText: 'Institutional-grade digital presence and civic engagement platforms',
  },
  {
    id: 'ventures-enterprise',
    stepNumber: 'STEP 4',
    title: 'Ventures, SMEs & Enterprise',
    description: 'Scaling creative economy innovators, high-growth SMEs, and corporate giants.',
    bullets: [
      'Creative Economy ecosystem acceleration and global audience monetization',
      'Startup venture building from validation to competitive market launch',
      'Scalable brand systems and digital transformation for SMEs & Corporates',
    ],
    cardTitle: 'Venture & Corporate Scale',
    image: '/images/works/lw-registry/showcase.webp',
    imageBadge: 'Market Acceleration',
    sectors: ['Creative Economy', 'Startups', 'SMEs', 'Corporate Organizations'],
    highlightText: 'End-to-end growth engines driving measurable enterprise revenue',
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
  const nextIdx = (activeIndex.value + direction + clusters.length) % clusters.length;
  activeIndex.value = nextIdx;
  const targetButton = document.getElementById(`industry-tab-${nextIdx}`);
  if (targetButton) targetButton.focus();
};

onMounted(() => {
  // Auto-play: advance every 6 seconds if user has not interacted
  autoPlayTimer = setInterval(() => {
    if (isAutoPlaying.value) {
      activeIndex.value = (activeIndex.value + 1) % clusters.length;
    }
  }, 6000);
});

onBeforeUnmount(() => {
  if (autoPlayTimer) clearInterval(autoPlayTimer);
  if (hoverTimeout) clearTimeout(hoverTimeout);
});
</script>

<template>
  <section class="border-b border-gray-100 bg-white py-20 text-gray-900 sm:py-24 lg:py-24">
    <div class="mx-auto w-5/6 max-w-7xl">
      <!-- Section Header (Centered, matching Matching Beyond Keywords) -->
      <div v-reveal="'fade-up'" class="mx-auto max-w-3xl text-center">
        <!-- Eyebrow Pill -->
        <span
          class="inline-block rounded-md bg-gray-100 px-3.5 py-1 text-[11px] font-semibold tracking-wider text-gray-600 uppercase"
        >
          Cross-Sector Growth • Proven Execution
        </span>

        <!-- Headline -->
        <h2
          class="mt-4 font-serif text-3xl leading-tight font-normal tracking-tight text-gray-900 sm:text-4xl lg:text-5xl"
        >
          Experience across <span class="text-[#04308F]">diverse industries</span>
        </h2>

        <!-- Subtitle -->
        <p
          class="font-open-sans mx-auto mt-4 max-w-2xl text-sm leading-relaxed font-normal text-gray-500 sm:text-base"
        >
          We partner with businesses across industries to deliver solutions built for growth.
        </p>

        <!-- CTA Button Under Header -->
        <div class="mt-7 flex justify-center">
          <NuxtLink
            to="https://app-deagensie-waitlist.vercel.app/"
            target="_blank"
            rel="noopener noreferrer"
            class="inline-flex items-center justify-center rounded-full bg-[#0F1E2E] px-8 py-3.5 text-sm font-medium text-white shadow-md shadow-gray-900/10 transition-all duration-300 hover:bg-[#04308F] hover:shadow-lg focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-[#04308F]"
          >
            Partner with Deagensie
          </NuxtLink>
        </div>
      </div>

      <!-- Main Layout: 2 Columns (~45% / ~55%), 40px gap, top aligned -->
      <div class="mt-14 grid grid-cols-1 items-start gap-10 lg:grid-cols-12 lg:gap-10">
        <!-- LEFT COLUMN: Accordion list (~45% width, lg:col-span-5) -->
        <div
          class="flex flex-col border-y border-gray-200 lg:col-span-5"
          role="tablist"
          aria-label="Deagensie Industry Sectors"
        >
          <div
            v-for="(st, idx) in clusters"
            :key="st.id"
            class="border-b border-gray-200 last:border-b-0"
          >
            <!-- Row Button Trigger -->
            <button
              :id="'industry-tab-' + idx"
              type="button"
              role="tab"
              :aria-selected="activeIndex === idx"
              :aria-controls="'industry-preview-' + idx"
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
                  <p class="font-open-sans text-sm leading-relaxed text-gray-500">
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

        <!-- RIGHT COLUMN: Large Rounded Panel (~55% width, lg:col-span-7) -->
        <div
          :id="'industry-preview-' + activeIndex"
          class="relative flex h-[560px] w-full items-center justify-center overflow-hidden rounded-[24px] border border-gray-200/80 bg-[#FAFAFA] p-6 shadow-xs sm:p-8 lg:col-span-7"
          role="tabpanel"
          :aria-labelledby="'industry-tab-' + activeIndex"
        >
          <!-- Animated Preview Card (Transition with slide + fade) -->
          <Transition name="card-slide" mode="out-in">
            <div
              :key="'panel-' + activeIndex"
              class="w-full max-w-[460px] rounded-[16px] border border-gray-200/90 bg-white p-5 shadow-[0_8px_30px_rgba(0,0,0,0.05)] sm:p-6"
            >
              <!-- Card Header Row -->
              <div class="flex items-center justify-between border-b border-gray-100 pb-3">
                <div class="flex items-center gap-2">
                  <span class="flex size-2 rounded-full bg-[#04308F]"></span>
                  <h4 class="text-sm font-semibold text-gray-900">
                    {{ clusters[activeIndex].cardTitle }}
                  </h4>
                </div>
                <span
                  class="rounded-full bg-[#04308F]/10 px-2 py-0.5 text-[10px] font-semibold text-[#04308F]"
                >
                  {{ clusters[activeIndex].sectors.length }} Sectors Featured
                </span>
              </div>

              <!-- Visual Photo Banner -->
              <div
                class="relative mt-3.5 h-24 w-full overflow-hidden rounded-xl border border-gray-100 bg-slate-100 sm:h-28"
              >
                <NuxtImg
                  :src="clusters[activeIndex].image"
                  :alt="clusters[activeIndex].cardTitle"
                  class="size-full object-cover object-center"
                />
                <div
                  class="absolute inset-0 bg-gradient-to-t from-gray-900/60 via-transparent to-transparent"
                ></div>
                <span
                  class="absolute bottom-2 left-2.5 rounded-md bg-white/95 px-2 py-0.5 text-[10px] font-semibold text-gray-800 shadow-xs"
                >
                  {{ clusters[activeIndex].imageBadge }}
                </span>
              </div>

              <!-- Body: Sector Tags Grid -->
              <div class="mt-3.5 space-y-3">
                <div>
                  <span class="text-[11px] font-bold tracking-wider text-gray-400 uppercase">
                    Active Industry Domains:
                  </span>
                  <div class="mt-2 grid grid-cols-2 gap-1.5 text-xs">
                    <div
                      v-for="sec in clusters[activeIndex].sectors"
                      :key="sec"
                      class="flex items-center gap-1.5 rounded-lg border border-gray-100 bg-[#FAFAFA] px-2.5 py-1.5 font-medium text-gray-800"
                    >
                      <svg
                        class="size-3.5 shrink-0 text-emerald-500"
                        viewBox="0 0 20 20"
                        fill="currentColor"
                      >
                        <path
                          fill-rule="evenodd"
                          d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z"
                          clip-rule="evenodd"
                        />
                      </svg>
                      <span>{{ sec }}</span>
                    </div>
                  </div>
                </div>

                <div
                  class="rounded-lg border border-gray-100 bg-gray-50/70 p-2 text-center text-[10px] text-gray-500 sm:text-[11px]"
                >
                  {{ clusters[activeIndex].highlightText }}
                </div>

                <!-- Action Button -->
                <div class="pt-1">
                  <NuxtLink
                    to="https://app-deagensie-waitlist.vercel.app/"
                    target="_blank"
                    rel="noopener noreferrer"
                    class="block w-full rounded-lg bg-[#0F1E2E] py-2.5 text-center text-xs font-semibold text-white transition-colors hover:bg-[#04308F]"
                  >
                    Build for Your Industry
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
