<template>
  <section class="border-b border-gray-100 bg-[#FAFAFA] py-20 text-gray-900 sm:py-24 lg:py-28">
    <div class="mx-auto w-5/6 max-w-7xl">
      <!-- Section Header: Centered in the middle, structured and formatted like other h2 tags -->
      <div v-reveal="'fade-up'" class="mx-auto max-w-4xl text-center">
        <span
          class="inline-block rounded-full bg-[#04308F]/10 px-4 py-1.5 text-xs font-semibold tracking-widest text-[#04308F] uppercase"
        >
          Continuous Flywheel
        </span>

        <h2
          class="mt-4 font-serif text-3xl leading-[1.15] font-normal tracking-tight text-gray-900 sm:text-4xl lg:text-5xl"
        >
          Deagensie TaaS Flywheel. <br class="hidden sm:inline" />
          <span class="text-[#04308F]">An Ecosystem That Gets Smarter.</span>
        </h2>

        <p
          class="mx-auto mt-6 max-w-3xl text-sm leading-relaxed font-normal text-gray-600 sm:text-base lg:text-lg"
        >
          A self-reinforcing network where every profile, project, and placement trains our
          predictive intelligence to generate increasingly precise matches.
        </p>
      </div>

      <!-- Main Flywheel Content: 9-Step Interactive Sequence on Left, Standard Circular Flywheel on Right -->
      <div class="mt-14 grid grid-cols-1 items-center gap-10 sm:mt-16 lg:grid-cols-12 lg:gap-14">
        <!-- LEFT COLUMN: 9-Step Interactive Flywheel List & CTA -->
        <div v-reveal="'fade-right'" class="space-y-4 lg:col-span-5">
          <div class="space-y-1">
            <h3 class="font-serif text-xl font-normal text-gray-900 sm:text-2xl">
              The 9-Phase Flywheel Cycle
            </h3>
            <p class="text-xs text-gray-500 sm:text-sm">
              Select any stage below to inspect its role within the self-reinforcing intelligence
              loop.
            </p>
          </div>

          <!-- The 9-Step Interactive Flywheel List with Expanding Details -->
          <div class="space-y-1.5 pt-1">
            <div
              v-for="(st, idx) in flywheelSteps"
              :key="st.id"
              class="group relative flex cursor-pointer flex-col justify-center rounded-xl px-3.5 py-2.5 transition-all duration-200"
              :class="
                activeStep === idx
                  ? 'border border-gray-200/90 bg-white shadow-xs'
                  : 'border border-transparent hover:bg-white/60'
              "
              @click="setActiveStep(idx, true)"
            >
              <div class="flex items-center justify-between">
                <div class="flex items-center gap-3">
                  <!-- Step Number Badge -->
                  <span
                    class="flex size-6 items-center justify-center rounded-md font-mono text-[11px] font-semibold transition-colors"
                    :class="
                      activeStep === idx
                        ? 'bg-[#04308F] text-white'
                        : 'bg-gray-100 text-gray-500 group-hover:text-gray-800'
                    "
                  >
                    {{ st.id }}
                  </span>

                  <!-- Title -->
                  <span
                    class="text-xs transition-colors sm:text-sm"
                    :class="
                      activeStep === idx
                        ? 'font-semibold text-gray-900'
                        : 'text-gray-600 group-hover:text-gray-900'
                    "
                  >
                    {{ st.title }}
                  </span>
                </div>

                <!-- Connecting Arrow / Active Indicator -->
                <div class="flex items-center text-xs">
                  <span
                    v-if="activeStep === idx"
                    class="rounded-full bg-[#04308F]/10 px-2 py-0.5 text-[10px] font-semibold text-[#04308F]"
                  >
                    Active Phase
                  </span>
                  <span v-else class="font-mono text-xs text-gray-400 group-hover:text-gray-600">
                    {{ idx === 8 ? '↺' : '↓' }}
                  </span>
                </div>
              </div>

              <!-- Expanded Detail Line on Active Step -->
              <div
                v-if="activeStep === idx"
                class="mt-2 pl-9 text-xs leading-relaxed text-gray-500 transition-opacity duration-300"
              >
                {{ st.detail }}
              </div>
            </div>
          </div>

          <!-- CTA Button -->
          <div class="pt-3">
            <NuxtLink
              to="https://app-deagensie-waitlist.vercel.app/"
              target="_blank"
              rel="noopener noreferrer"
              class="inline-flex items-center justify-center rounded-full bg-[#0F1E2E] px-8 py-3.5 text-sm font-medium text-white shadow-md shadow-gray-900/10 transition-all duration-300 hover:bg-[#04308F] hover:shadow-lg focus-visible:outline-2 focus-visible:outline-offset-2 focus-visible:outline-[#04308F]"
            >
              Join the network
            </NuxtLink>
          </div>
        </div>

        <!-- RIGHT COLUMN: Standard Aesthetic Circular Orbital Flywheel Graphic -->
        <div v-reveal="'fade-left'" class="flex justify-center lg:col-span-7">
          <div
            class="relative flex aspect-square w-full max-w-[580px] items-center justify-center overflow-visible rounded-[2.5rem] border border-gray-200/90 bg-white p-3 shadow-xs sm:p-6"
          >
            <!-- Background Soft Ambient Glow -->
            <div class="pointer-events-none absolute inset-0 flex items-center justify-center">
              <div class="size-[360px] rounded-full bg-[#04308F]/4 blur-3xl sm:size-[440px]"></div>
            </div>

            <!-- Concentric Orbital SVG Track & Directional Arrows -->
            <svg
              class="pointer-events-none absolute inset-0 size-full"
              viewBox="0 0 600 600"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
            >
              <defs>
                <linearGradient
                  id="activeRayGrad"
                  x1="300"
                  y1="300"
                  :x2="activeNodeCoords.x"
                  :y2="activeNodeCoords.y"
                  gradientUnits="userSpaceOnUse"
                >
                  <stop offset="0%" stop-color="#05DED5" stop-opacity="0.85" />
                  <stop offset="100%" stop-color="#04308F" stop-opacity="0.9" />
                </linearGradient>
              </defs>

              <!-- Outer Reference Orbit (r=275) -->
              <circle cx="300" cy="300" r="275" stroke="#F1F5F9" stroke-width="1" />

              <!-- Main Flywheel Orbital Path (r=205) -->
              <circle
                cx="300"
                cy="300"
                r="205"
                stroke="#CBD5E1"
                stroke-width="1.6"
                stroke-dasharray="5 7"
              />

              <!-- Inner Reference Orbit (r=135) -->
              <circle
                cx="300"
                cy="300"
                r="135"
                stroke="#E2E8F0"
                stroke-width="1"
                stroke-dasharray="3 5"
              />

              <!-- Clockwise Flywheel Flow Direction Chevrons -->
              <g
                v-for="(chev, cIdx) in flowChevrons"
                :key="'chev-' + cIdx"
                :transform="getChevronTransform(chev)"
              >
                <path
                  d="M-3 -4 L3 0 L-3 4"
                  stroke="#94A3B8"
                  stroke-width="1.6"
                  stroke-linecap="round"
                  stroke-linejoin="round"
                  fill="none"
                />
              </g>

              <!-- Active Energy Beam from Central TaaS AI Core to Active Stage Node -->
              <line
                x1="300"
                y1="300"
                :x2="activeNodeCoords.x"
                :y2="activeNodeCoords.y"
                stroke="url(#activeRayGrad)"
                stroke-width="2"
                stroke-dasharray="4 4"
                stroke-linecap="round"
                class="transition-all duration-500"
              />
            </svg>

            <!-- Center Core Hub: Talent-as-a-Service AI Image Emblem (No Beeping) -->
            <div
              class="group relative z-20 flex size-28 items-center justify-center overflow-hidden rounded-full border-4 border-white bg-slate-950 shadow-xl ring-2 ring-[#04308F]/20 select-none sm:size-36"
            >
              <!-- Center Neural Core Image Asset -->
              <NuxtImg
                src="/images/pages/creatives/taas-ai-core.jpg"
                alt="Talent-as-a-Service AI Core"
                class="size-full object-cover object-center transition-transform duration-700 group-hover:scale-105"
              />

              <!-- Elegant Gradient Vignette Overlay -->
              <div
                class="absolute inset-0 bg-gradient-to-t from-gray-950/85 via-gray-950/25 to-transparent"
              ></div>

              <!-- Center Label: Talent-as-a-Service AI -->
              <div
                class="absolute inset-x-2 bottom-2.5 flex flex-col items-center justify-center text-center sm:bottom-3"
              >
                <div class="flex items-center gap-1">
                  <span class="size-1.5 rounded-full bg-[#05DED5]"></span>
                  <span
                    class="font-mono text-[8px] font-bold tracking-widest text-[#05DED5] uppercase sm:text-[9px]"
                  >
                    TAAS AI
                  </span>
                </div>
                <span
                  class="mt-0.5 text-[9px] leading-tight font-medium text-white/95 sm:text-[10px]"
                >
                  Predictive Engine
                </span>
              </div>
            </div>

            <!-- Orbiting Circular Nodes: Exactly Spaced Around 360-Degree Circular Track (Zero Overlap) -->
            <div
              v-for="(st, idx) in flywheelSteps"
              :key="st.id"
              class="absolute z-10 transition-all duration-300"
              :class="
                activeStep === idx
                  ? 'z-30 scale-110'
                  : 'opacity-90 hover:scale-105 hover:opacity-100'
              "
              :style="getNodeStyle(st)"
              @click="setActiveStep(idx, true)"
            >
              <!-- Step Node 1: Creative Talent Avatar Pill -->
              <div
                v-if="st.iconType === 'avatar-talent'"
                class="flex cursor-pointer items-center gap-2 rounded-full border bg-white p-1 shadow-sm transition-all duration-200 sm:pr-2.5"
                :class="
                  activeStep === idx
                    ? 'border-[#04308F] bg-white shadow-md ring-4 ring-[#04308F]/15'
                    : 'border-gray-200/90'
                "
              >
                <div
                  class="relative size-7 shrink-0 overflow-hidden rounded-full bg-slate-100 sm:size-8"
                >
                  <NuxtImg
                    :src="st.image"
                    alt="Creative Talent"
                    class="size-full object-cover object-[50%_15%]"
                  />
                </div>
                <span
                  class="hidden text-[10px] font-semibold whitespace-nowrap text-gray-800 sm:inline sm:text-[11px]"
                >
                  {{ st.nodeLabel }}
                </span>
              </div>

              <!-- Step Node 6: Engagement Team Avatar Pill -->
              <div
                v-else-if="st.iconType === 'avatar-team'"
                class="flex cursor-pointer items-center gap-2 rounded-full border bg-white p-1 shadow-sm transition-all duration-200 sm:pr-2.5"
                :class="
                  activeStep === idx
                    ? 'border-[#04308F] bg-white shadow-md ring-4 ring-[#04308F]/15'
                    : 'border-gray-200/90'
                "
              >
                <div
                  class="relative size-7 shrink-0 overflow-hidden rounded-full bg-slate-100 sm:size-8"
                >
                  <NuxtImg :src="st.image" alt="Engagement Team" class="size-full object-cover" />
                </div>
                <span
                  class="hidden text-[10px] font-semibold whitespace-nowrap text-gray-800 sm:inline sm:text-[11px]"
                >
                  {{ st.nodeLabel }}
                </span>
              </div>

              <!-- Step Node 3: Venture GitHub Logo Pill -->
              <div
                v-else-if="st.iconType === 'github'"
                class="flex cursor-pointer items-center gap-2 rounded-full border bg-white p-1 shadow-sm transition-all duration-200 sm:pr-2.5"
                :class="
                  activeStep === idx
                    ? 'border-[#04308F] bg-white shadow-md ring-4 ring-[#04308F]/15'
                    : 'border-gray-200/90'
                "
              >
                <div
                  class="flex size-7 shrink-0 items-center justify-center rounded-full bg-[#0F1E2E] text-white sm:size-8"
                >
                  <svg class="size-3.5 fill-current sm:size-4" viewBox="0 0 24 24">
                    <path
                      d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0024 12c0-6.63-5.37-12-12-12z"
                    />
                  </svg>
                </div>
                <span
                  class="hidden text-[10px] font-semibold whitespace-nowrap text-gray-800 sm:inline sm:text-[11px]"
                >
                  {{ st.nodeLabel }}
                </span>
              </div>

              <!-- Step Node 4: AI Analyzes Fit Pill -->
              <div
                v-else-if="st.iconType === 'ai'"
                class="flex cursor-pointer items-center gap-1.5 rounded-full border bg-white p-1 shadow-sm transition-all duration-200 sm:px-2.5 sm:py-1.5"
                :class="
                  activeStep === idx
                    ? 'border-[#04308F] bg-white text-[#04308F] shadow-md ring-4 ring-[#04308F]/15'
                    : 'border-gray-200/90 text-gray-700'
                "
              >
                <div
                  class="flex size-7 shrink-0 items-center justify-center rounded-full bg-slate-100 text-[#04308F] sm:size-8"
                >
                  <span class="size-2 rounded-full bg-[#05DED5]"></span>
                </div>
                <span
                  class="hidden text-[10px] font-bold whitespace-nowrap sm:inline sm:text-[11px]"
                  >{{ st.nodeLabel }}</span
                >
              </div>

              <!-- General Icon Nodes (Profile, Check, Chart, Sparkle, Globe) -->
              <div
                v-else
                class="flex cursor-pointer items-center gap-2 rounded-full border bg-white p-1 shadow-sm transition-all duration-200 sm:pr-2.5"
                :class="
                  activeStep === idx
                    ? 'border-[#04308F] bg-white shadow-md ring-4 ring-[#04308F]/15'
                    : 'border-gray-200/90'
                "
              >
                <div
                  class="flex size-7 shrink-0 items-center justify-center rounded-full transition-colors sm:size-8"
                  :class="
                    activeStep === idx ? 'bg-[#04308F] text-white' : 'bg-gray-100 text-gray-700'
                  "
                >
                  <!-- Profile Icon -->
                  <svg
                    v-if="st.iconType === 'profile'"
                    class="size-3.5 sm:size-4"
                    viewBox="0 0 20 20"
                    fill="currentColor"
                  >
                    <path
                      fill-rule="evenodd"
                      d="M10 9a3 3 0 100-6 3 3 0 000 6zm-7 9a7 7 0 1114 0H3z"
                      clip-rule="evenodd"
                    />
                  </svg>
                  <!-- Check Icon -->
                  <svg
                    v-else-if="st.iconType === 'check'"
                    class="size-3.5 sm:size-4"
                    viewBox="0 0 20 20"
                    fill="currentColor"
                  >
                    <path
                      fill-rule="evenodd"
                      d="M16.707 5.293a1 1 0 010 1.414l-8 8a1 1 0 01-1.414 0l-4-4a1 1 0 011.414-1.414L8 12.586l7.293-7.293a1 1 0 011.414 0z"
                      clip-rule="evenodd"
                    />
                  </svg>
                  <!-- Chart Icon -->
                  <svg
                    v-else-if="st.iconType === 'chart'"
                    class="size-3.5 sm:size-4"
                    viewBox="0 0 20 20"
                    fill="currentColor"
                  >
                    <path
                      d="M2 11a1 1 0 011-1h2a1 1 0 011 1v5a1 1 0 01-1 1H3a1 1 0 01-1-1v-5zM8 7a1 1 0 011-1h2a1 1 0 011 1v9a1 1 0 01-1 1H9a1 1 0 01-1-1V7zM14 4a1 1 0 011-1h2a1 1 0 011 1v12a1 1 0 01-1 1h-2a1 1 0 01-1-1V4z"
                    />
                  </svg>
                  <!-- Sparkle Icon -->
                  <svg
                    v-else-if="st.iconType === 'sparkle'"
                    class="size-3.5 sm:size-4"
                    viewBox="0 0 20 20"
                    fill="currentColor"
                  >
                    <path
                      fill-rule="evenodd"
                      d="M11.3 1.046A1 1 0 0112 2v5h4a1 1 0 01.82 1.573l-7 10A1 1 0 018 18v-5H4a1 1 0 01-.82-1.573l7-10a1 1 0 011.12-.38z"
                      clip-rule="evenodd"
                    />
                  </svg>
                  <!-- Globe Icon -->
                  <svg
                    v-else-if="st.iconType === 'globe'"
                    class="size-3.5 sm:size-4"
                    viewBox="0 0 20 20"
                    fill="currentColor"
                  >
                    <path
                      d="M10.707 2.293a1 1 0 00-1.414 0l-7 7a1 1 0 001.414 1.414L4 10.414V17a1 1 0 001 1h2a1 1 0 001-1v-2a1 1 0 011-1h2a1 1 0 011 1v2a1 1 0 001 1h2a1 1 0 001-1v-6.586l.293.293a1 1 0 001.414-1.414l-7-7z"
                    />
                  </svg>
                </div>
                <span
                  class="hidden text-[10px] font-semibold whitespace-nowrap text-gray-800 sm:inline sm:text-[11px]"
                >
                  {{ st.nodeLabel }}
                </span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
interface FlywheelStep {
  id: number;
  title: string;
  detail: string;
  nodeLabel: string;
  iconType:
    | 'avatar-talent'
    | 'avatar-team'
    | 'profile'
    | 'github'
    | 'ai'
    | 'check'
    | 'chart'
    | 'sparkle'
    | 'globe';
  image?: string;
  posX: number;
  posY: number;
  svgX: number;
  svgY: number;
}

// 9 Flywheel steps strictly following user copy, mapped to 40-degree circular orbit (R=205, Center 300,300)
const flywheelSteps: FlywheelStep[] = [
  {
    id: 1,
    title: 'Talent joins',
    detail: 'Exceptional creative professionals enter the Deagensie talent ecosystem.',
    nodeLabel: 'Talent Joins',
    iconType: 'avatar-talent',
    image: '/images/pages/creatives/hero-1.png',
    posX: 50.0,
    posY: 15.8,
    svgX: 300,
    svgY: 95,
  },
  {
    id: 2,
    title: 'Talent builds profile',
    detail: 'Skills, experience, portfolio, specializations and availability are mapped.',
    nodeLabel: 'Profile Built',
    iconType: 'profile',
    posX: 72.0,
    posY: 23.8,
    svgX: 432,
    svgY: 143,
  },
  {
    id: 3,
    title: 'Businesses create opportunities',
    detail: 'Ventures define project scope, requirements, timeline and engagement model.',
    nodeLabel: 'Opportunities',
    iconType: 'github',
    posX: 83.6,
    posY: 44.1,
    svgX: 502,
    svgY: 264,
  },
  {
    id: 4,
    title: 'AI analyzes fit',
    detail: 'Predictive intelligence evaluates multi-dimensional criteria beyond keywords.',
    nodeLabel: 'AI Analyzes Fit',
    iconType: 'ai',
    posX: 79.6,
    posY: 67.1,
    svgX: 478,
    svgY: 403,
  },
  {
    id: 5,
    title: 'Talent is matched to opportunity',
    detail: 'High-confidence candidates are paired with relevant venture engagements.',
    nodeLabel: 'Talent Matched',
    iconType: 'check',
    posX: 61.7,
    posY: 82.1,
    svgX: 370,
    svgY: 493,
  },
  {
    id: 6,
    title: 'Business engages talent',
    detail: 'Seamless onboarding for project, contract, or dedicated creative support.',
    nodeLabel: 'Talent Engaged',
    iconType: 'avatar-team',
    image: '/images/works/lw-registry/showcase.webp',
    posX: 38.3,
    posY: 82.1,
    svgX: 230,
    svgY: 493,
  },
  {
    id: 7,
    title: 'Work creates experience & performance data',
    detail: 'Live delivery generates telemetry, milestone achievements and verified track records.',
    nodeLabel: 'Performance Data',
    iconType: 'chart',
    posX: 20.4,
    posY: 67.1,
    svgX: 122,
    svgY: 403,
  },
  {
    id: 8,
    title: 'Matching intelligence improves',
    detail: 'Feedback loops sharpen the predictive engine algorithms with every project.',
    nodeLabel: 'Intelligence Loop',
    iconType: 'sparkle',
    posX: 16.4,
    posY: 44.1,
    svgX: 98,
    svgY: 264,
  },
  {
    id: 9,
    title: 'More relevant opportunities',
    detail: 'Higher precision attracts more ventures, compounding growth across the network.',
    nodeLabel: 'More Opportunities',
    iconType: 'globe',
    posX: 28.0,
    posY: 23.8,
    svgX: 168,
    svgY: 143,
  },
];

// Midpoint chevrons along the flywheel track indicating continuous clockwise momentum
const flowChevrons = [
  { x: 370, y: 107, rot: 20 },
  { x: 478, y: 198, rot: 60 },
  { x: 502, y: 336, rot: 100 },
  { x: 432, y: 457, rot: 140 },
  { x: 300, y: 505, rot: 180 },
  { x: 168, y: 457, rot: 220 },
  { x: 98, y: 336, rot: 260 },
  { x: 122, y: 198, rot: 300 },
  { x: 230, y: 107, rot: 340 },
];

// Active step state in the loop
const activeStep = ref<number>(0);
const isAutoCycling = ref<boolean>(true);
let cycleTimer: ReturnType<typeof setInterval> | null = null;

const clearCycleTimer = () => {
  if (cycleTimer) {
    clearInterval(cycleTimer);
    cycleTimer = null;
  }
};

// Select step manually (pauses auto-cycle)
const setActiveStep = (idx: number, stopAuto = true) => {
  if (stopAuto) {
    isAutoCycling.value = false;
    clearCycleTimer();
  }
  activeStep.value = idx;
};

// Current active SVG coordinates for connector ray
const activeNodeCoords = computed(() => {
  const current = flywheelSteps[activeStep.value];
  return current ? { x: current.svgX, y: current.svgY } : { x: 300, y: 95 };
});

const getNodeStyle = (st: FlywheelStep) => {
  return {
    left: `${st.posX}%`,
    top: `${st.posY}%`,
    transform: 'translate(-50%, -50%)',
  };
};

const getChevronTransform = (chev: { x: number; y: number; rot: number }) => {
  return `translate(${chev.x}, ${chev.y}) rotate(${chev.rot})`;
};

onMounted(() => {
  cycleTimer = setInterval(() => {
    if (isAutoCycling.value) {
      activeStep.value = (activeStep.value + 1) % flywheelSteps.length;
    }
  }, 4500);
});

onBeforeUnmount(() => {
  clearCycleTimer();
});
</script>

<style scoped>
.flywheel-container {
  contain: layout;
}
</style>
