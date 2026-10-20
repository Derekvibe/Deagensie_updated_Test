<script setup lang="ts">
/**
 * DEAGENSIE VENTURE FRAMEWORK - SPLIT-SCREEN HERO CARD
 *
 * QUICK CUSTOMIZATION GUIDE:
 * 1. LOGO: Change 'logoUrl' constant below or update fallback in sidebar logo slot.
 * 2. BRAND COLORS: Update 'brandColors' constant (deepBlue, cyan, dark) and stage 'tint' / 'hatch' properties.
 * 3. MEDIA URLS: Update 'media' and 'poster' properties in each object of the 'stages' array.
 * 4. COPY AND DELIVERABLES: Edit 'tagline', 'typedLines', 'deliverables', and 'terminalLines' in 'stages'.
 */

import { Icon } from '@iconify/vue';

// Brand color definitions
const _brandColors = {
  deepBlue: '#04308F',
  cyan: '#05DED5',
  dark: '#020B1E',
};

// Sidebar logo image path (fallback renders styled brand text wordmark)
const logoUrl = '/images/logo-dark.png';
const logoError = ref(false);

interface TerminalLines {
  command: string;
  progress: string[];
  checks: string[];
  final: string;
}

interface StageItem {
  id: string;
  number: string;
  name: string;
  tagline: string;
  tint: string;
  hatch: string;
  media: string;
  poster: string;
  typedLines: string[];
  deliverables: string[];
  bodyVariant: 'checklist' | 'terminal';
  terminalLines?: TerminalLines;
  badgeLabel: string;
}

const stages: StageItem[] = [
  {
    id: 'discover',
    number: '01',
    name: 'DISCOVER',
    tagline: 'Understand the business, market, customer and opportunity.',
    tint: '#F8FAFC',
    hatch: 'rgba(4, 48, 143, 0.08)',
    media:
      'https://images.unsplash.com/photo-1551836022-d5d88e9218df?auto=format&fit=crop&w=1200&q=80',
    poster:
      'https://images.unsplash.com/photo-1551836022-d5d88e9218df?auto=format&fit=crop&w=1200&q=80',
    typedLines: [
      'stage: discover',
      'focus: market, customer, opportunity',
      'output: validated opportunity map',
    ],
    deliverables: [
      'Market and competitor scan',
      'Customer research and personas',
      'Opportunity sizing',
    ],
    bodyVariant: 'checklist',
    badgeLabel: 'STAGE 01 / 06',
  },
  {
    id: 'strategize',
    number: '02',
    name: 'STRATEGIZE',
    tagline: 'Define the growth direction, positioning and roadmap.',
    tint: '#F8FAFC',
    hatch: 'rgba(4, 48, 143, 0.08)',
    media:
      'https://images.unsplash.com/photo-1531403009284-440f080d1e12?auto=format&fit=crop&w=1200&q=80',
    poster:
      'https://images.unsplash.com/photo-1531403009284-440f080d1e12?auto=format&fit=crop&w=1200&q=80',
    typedLines: [
      'stage: strategize',
      'focus: growth model, positioning, roadmap',
      'output: go-to-market direction',
    ],
    deliverables: ['Growth model and positioning', 'Go-to-market direction', 'Phased roadmap'],
    bodyVariant: 'checklist',
    badgeLabel: 'STAGE 02 / 06',
  },
  {
    id: 'brand',
    number: '03',
    name: 'BRAND',
    tagline: 'Build a distinctive identity and market position.',
    tint: '#F8FAFC',
    hatch: 'rgba(4, 48, 143, 0.08)',
    media:
      'https://images.unsplash.com/photo-1507238691740-187a5b1d37b8?auto=format&fit=crop&w=1200&q=80',
    poster:
      'https://images.unsplash.com/photo-1507238691740-187a5b1d37b8?auto=format&fit=crop&w=1200&q=80',
    typedLines: [
      'stage: brand',
      'focus: identity, messaging, authority',
      'output: distinctive brand system',
    ],
    deliverables: ['Identity and visual system', 'Messaging and voice', 'Market position'],
    bodyVariant: 'checklist',
    badgeLabel: 'STAGE 03 / 06',
  },
  {
    id: 'market',
    number: '04',
    name: 'MARKET',
    tagline: 'Create demand, acquire customers and establish market presence.',
    tint: '#F8FAFC',
    hatch: 'rgba(4, 48, 143, 0.08)',
    media:
      'https://images.unsplash.com/photo-1460925895917-afdab827c52f?auto=format&fit=crop&w=1200&q=80',
    poster:
      'https://images.unsplash.com/photo-1460925895917-afdab827c52f?auto=format&fit=crop&w=1200&q=80',
    typedLines: [
      'stage: market',
      'focus: demand generation, funnels, reach',
      'output: active customer acquisition',
    ],
    deliverables: [
      'Demand generation channels',
      'Customer acquisition funnels',
      'Launch and presence',
    ],
    bodyVariant: 'checklist',
    badgeLabel: 'STAGE 04 / 06',
  },
  {
    id: 'build',
    number: '05',
    name: 'BUILD',
    tagline: 'Design and develop the digital platforms required to operate and scale.',
    tint: '#F8FAFC',
    hatch: 'rgba(4, 48, 143, 0.08)',
    media:
      'https://images.unsplash.com/photo-1555066931-4365d14bab8c?auto=format&fit=crop&w=1200&q=80',
    poster:
      'https://images.unsplash.com/photo-1555066931-4365d14bab8c?auto=format&fit=crop&w=1200&q=80',
    typedLines: [
      'stage: build',
      'focus: digital platform, scale, architecture',
      'output: production web ecosystem',
    ],
    deliverables: [],
    bodyVariant: 'terminal',
    terminalLines: {
      command: '$ deagensie build --platform web',
      progress: ['Designing UX...', 'Developing platform...', 'Wiring analytics...'],
      checks: ['platform live', 'performance passed', 'ready to scale'],
      final: 'Ready for next stage',
    },
    badgeLabel: 'STAGE 05 / 06',
  },
  {
    id: 'grow',
    number: '06',
    name: 'GROW',
    tagline:
      'Continuously optimize the venture through data, experimentation and strategic execution.',
    tint: '#F8FAFC',
    hatch: 'rgba(4, 48, 143, 0.08)',
    media:
      'https://images.unsplash.com/photo-1551288049-bebda4e38f71?auto=format&fit=crop&w=1200&q=80',
    poster:
      'https://images.unsplash.com/photo-1551288049-bebda4e38f71?auto=format&fit=crop&w=1200&q=80',
    typedLines: [
      'stage: grow',
      'focus: data, experimentation, execution',
      'output: compounding venture scale',
    ],
    deliverables: [],
    bodyVariant: 'terminal',
    terminalLines: {
      command: '$ deagensie optimize --loop',
      progress: ['Reading performance data...', 'Running experiments...', 'Reallocating spend...'],
      checks: ['conversion up', 'CAC down', 'next sprint queued'],
      final: 'Ready for next stage',
    },
    badgeLabel: 'STAGE 06 / 06',
  },
];

// Active stage state
const activeStageIndex = ref(0);
const isPaused = ref(false);
const prefersReducedMotion = ref(false);

const currentStage = computed(() => stages[activeStageIndex.value]);

// Card CSS variables for current stage
const cardStyle = computed(() => ({
  '--stage-tint': currentStage.value.tint,
  '--stage-hatch': currentStage.value.hatch,
  backgroundColor: currentStage.value.tint,
}));

// Typewriter state for left code box
const typedOutput = ref<string[]>(['', '', '']);
const isTyping = ref(false);
const activeLineIdx = ref(0);
let typingTimer: ReturnType<typeof setTimeout> | null = null;
let runToken = 0;

// Checklist item resolution state
const checklistResolved = ref<boolean[]>([false, false, false]);
let checklistTimers: ReturnType<typeof setTimeout>[] = [];

// Terminal streaming step
const terminalStep = ref(0);
let terminalTimers: ReturnType<typeof setTimeout>[] = [];

// Auto-rotation timer (9 seconds per stage)
const STAGE_DURATION = 9000;
let rotationTimer: ReturnType<typeof setInterval> | null = null;

const formatTypedLine = (line: string) => {
  const colonIndex = line.indexOf(':');
  if (colonIndex === -1) {
    return { key: line, val: '' };
  }
  return {
    key: line.slice(0, colonIndex + 1),
    val: line.slice(colonIndex + 1),
  };
};

const startTypewriter = () => {
  if (typingTimer) clearTimeout(typingTimer);
  runToken++;
  const currentToken = runToken;
  const lines = currentStage.value.typedLines;

  if (prefersReducedMotion.value) {
    typedOutput.value = [...lines];
    isTyping.value = false;
    activeLineIdx.value = lines.length - 1;
    return;
  }

  typedOutput.value = ['', '', ''];
  isTyping.value = true;
  activeLineIdx.value = 0;

  let currentLineIndex = 0;
  let currentCharIndex = 0;

  const typeNextChar = () => {
    if (currentToken !== runToken) return;

    if (currentLineIndex >= lines.length) {
      isTyping.value = false;
      return;
    }

    activeLineIdx.value = currentLineIndex;
    const currentTargetLine = lines[currentLineIndex];

    if (currentCharIndex < currentTargetLine.length) {
      typedOutput.value[currentLineIndex] = currentTargetLine.slice(0, currentCharIndex + 1);
      currentCharIndex++;
      const jitter = 35 + Math.random() * 20;
      typingTimer = setTimeout(typeNextChar, jitter);
    } else {
      currentLineIndex++;
      currentCharIndex = 0;
      typingTimer = setTimeout(typeNextChar, 300);
    }
  };

  typingTimer = setTimeout(typeNextChar, 100);
};

const startChecklist = () => {
  checklistTimers.forEach((t) => clearTimeout(t));
  checklistTimers = [];

  const count = currentStage.value.deliverables.length;
  if (prefersReducedMotion.value) {
    checklistResolved.value = Array(count).fill(true);
    return;
  }

  checklistResolved.value = Array(count).fill(false);

  for (let i = 0; i < count; i++) {
    const delay = 120 + i * 160;
    const t = setTimeout(() => {
      checklistResolved.value[i] = true;
    }, delay);
    checklistTimers.push(t);
  }
};

const startTerminal = () => {
  terminalTimers.forEach((t) => clearTimeout(t));
  terminalTimers = [];

  if (!currentStage.value.terminalLines) return;

  if (prefersReducedMotion.value) {
    terminalStep.value = 999;
    return;
  }

  terminalStep.value = 0;
  const progressCount = currentStage.value.terminalLines.progress.length;
  const checksCount = currentStage.value.terminalLines.checks.length;
  const totalSteps = 1 + progressCount + checksCount + 1;

  for (let s = 1; s <= totalSteps; s++) {
    const delay = 140 + s * 190;
    const t = setTimeout(() => {
      terminalStep.value = s;
    }, delay);
    terminalTimers.push(t);
  }
};

const goToStage = (idx: number) => {
  activeStageIndex.value = idx;
  resetRotationTimer();
};

const nextStage = () => {
  activeStageIndex.value = (activeStageIndex.value + 1) % stages.length;
};

const resetRotationTimer = () => {
  if (rotationTimer) clearInterval(rotationTimer);
  rotationTimer = setInterval(() => {
    if (!isPaused.value) {
      nextStage();
    }
  }, STAGE_DURATION);
};

watch(activeStageIndex, () => {
  startTypewriter();
  if (currentStage.value.bodyVariant === 'checklist') {
    startChecklist();
  } else {
    startTerminal();
  }
});

onMounted(() => {
  if (typeof window !== 'undefined') {
    const mediaQuery = window.matchMedia('(prefers-reduced-motion: reduce)');
    prefersReducedMotion.value = mediaQuery.matches;
  }

  startTypewriter();
  if (currentStage.value.bodyVariant === 'checklist') {
    startChecklist();
  } else {
    startTerminal();
  }

  resetRotationTimer();
});

onBeforeUnmount(() => {
  if (rotationTimer) clearInterval(rotationTimer);
  if (typingTimer) clearTimeout(typingTimer);
  checklistTimers.forEach((t) => clearTimeout(t));
  terminalTimers.forEach((t) => clearTimeout(t));
});
</script>

<template>
  <section class="border-b border-gray-100 bg-white py-20 text-gray-900 lg:py-28">
    <div class="mx-auto w-5/6 max-w-7xl space-y-12 lg:space-y-16">
      <!-- Section Header -->
      <div v-reveal="'fade-up'" class="mx-auto max-w-3xl space-y-4 text-center">
        <!-- <span
          class="inline-block rounded-full bg-[#04308F]/10 px-4 py-1.5 text-xs font-semibold tracking-widest text-[#04308F] uppercase"
        >
          Venture Development System
        </span> -->
        <h2
          class="mx-auto w-full max-w-3xl text-center font-serif text-2xl leading-tight font-normal tracking-tight text-gray-900 sm:text-4xl lg:text-5xl 2xl:text-6xl"
        >
          From Idea to Market. <br class="hidden lg:inline" />
          <span class="text-[#04308F]"> From Market to Growth.</span>
        </h2>
        <p class="mx-auto max-w-3xl text-base leading-relaxed font-normal text-gray-500 lg:text-lg">
          Explore Deagensie venture development system designed to turn bold ideas into market-ready
          businesses through strategy, branding, marketing, and scalable digital solutions.
        </p>
      </div>

      <!-- Split-Screen Hero Card (Max Width 1200px, 16px Gap, Equal Height ~520px Desktop) -->
      <div
        v-reveal="'fade-up'"
        class="mx-auto w-full max-w-[1200px]"
        @mouseenter="isPaused = true"
        @mouseleave="isPaused = false"
        @focusin="isPaused = true"
        @focusout="isPaused = false"
      >
        <div class="grid grid-cols-1 gap-4 md:min-h-[520px] md:grid-cols-2">
          <!-- LEFT CARD: Media with Dark Translucent Code Box (Hidden on smaller screens) -->
          <div
            class="relative hidden h-[380px] w-full flex-col justify-end overflow-hidden rounded-[20px] bg-[#020B1E] p-6 shadow-sm md:flex md:h-auto md:min-h-[520px]"
          >
            <!-- Visual Media with CSS Gradient Fallback -->
            <div class="absolute inset-0">
              <Transition name="media-fade" mode="out-in">
                <div :key="currentStage.id" class="relative size-full">
                  <!-- Video background if video URL, otherwise responsive image -->
                  <video
                    v-if="currentStage.media.endsWith('.mp4')"
                    :src="currentStage.media"
                    :poster="currentStage.poster"
                    autoplay
                    muted
                    loop
                    playsinline
                    class="size-full object-cover"
                  />
                  <img
                    v-else
                    :src="currentStage.media"
                    :alt="currentStage.name"
                    class="size-full object-cover"
                    loading="lazy"
                  />
                  <!-- Subtle gradient overlay for contrast -->
                  <div
                    class="absolute inset-0 bg-gradient-to-t from-[#020B1E]/80 via-black/25 to-transparent"
                  />
                </div>
              </Transition>
            </div>

            <!-- Overlaid Dark Translucent Code Box (rgba(2, 11, 30, 0.88), 8px radius, 16px padding, ~55% width) -->
            <div
              class="relative z-10 w-[92%] rounded-[8px] border border-white/10 p-4 font-mono text-[13px] leading-relaxed shadow-2xl backdrop-blur-md sm:w-[60%]"
              style="background-color: rgba(2, 11, 30, 0.88)"
              aria-live="off"
            >
              <div
                class="mb-2 flex items-center gap-1.5 border-b border-white/10 pb-2 font-mono text-[10px] tracking-widest text-gray-400 uppercase"
              >
                <span class="size-1.5 rounded-full bg-[#05DED5]" />
                <span>brief // {{ currentStage.id }}</span>
              </div>
              <div class="space-y-1">
                <div
                  v-for="(line, lIdx) in typedOutput"
                  :key="lIdx"
                  class="min-h-[20px] font-mono text-[12px] leading-relaxed sm:text-[13px]"
                >
                  <span class="font-semibold text-[#05DED5]">{{ formatTypedLine(line).key }}</span>
                  <span class="text-white">{{ formatTypedLine(line).val }}</span>
                  <span
                    v-if="isTyping && lIdx === activeLineIdx"
                    class="ml-0.5 inline-block h-3.5 w-1.5 animate-pulse bg-[#05DED5] align-middle"
                  />
                </div>
              </div>
            </div>
          </div>

          <!-- RIGHT CARD: Dynamic Soft Pastel Background with Mock App Window -->
          <div
            class="relative flex min-h-[480px] w-full flex-col justify-between overflow-hidden rounded-[20px] p-5 transition-colors duration-600 sm:p-6 md:min-h-[520px] lg:p-7"
            :style="cardStyle"
          >
            <!-- Decorative Diagonal-Hatch Stripes in Corners (clipped by overflow-hidden) -->
            <div
              class="pointer-events-none absolute -bottom-8 -left-8 size-44 rounded-full opacity-80"
              style="
                background: repeating-linear-gradient(
                  45deg,
                  var(--stage-hatch) 0,
                  var(--stage-hatch) 2px,
                  transparent 2px,
                  transparent 10px
                );
              "
            />
            <div
              class="pointer-events-none absolute -top-8 -right-8 size-48 rounded-full opacity-80"
              style="
                background: repeating-linear-gradient(
                  45deg,
                  var(--stage-hatch) 0,
                  var(--stage-hatch) 2px,
                  transparent 2px,
                  transparent 10px
                );
              "
            />

            <!-- Top Row: Label and Stage Tracker Dots -->
            <div class="relative z-10 flex items-center justify-between pb-3">
              <span class="text-xs font-semibold tracking-wider text-gray-600 uppercase">
                The Deagensie Venture Framework:
              </span>
              <div class="flex items-center gap-1.5" role="tablist">
                <button
                  v-for="(st, sIdx) in stages"
                  :key="st.id"
                  type="button"
                  role="tab"
                  :aria-selected="activeStageIndex === sIdx"
                  :class="[
                    'size-2 rounded-full transition-all duration-300 focus:ring-1 focus:ring-[#04308F] focus:outline-none',
                    activeStageIndex === sIdx
                      ? 'w-4.5 bg-[#04308F]'
                      : 'bg-gray-300 hover:bg-gray-400',
                  ]"
                  :aria-label="'Jump to stage ' + st.number + ' ' + st.name"
                  @click="goToStage(sIdx)"
                />
              </div>
            </div>

            <!-- Mock App Window: Soft Shadow, 1px Border, Sidebar and Main Pane -->
            <div
              class="relative z-10 flex flex-1 flex-col overflow-hidden rounded-2xl border border-gray-200/70 bg-white shadow-[0_10px_40px_rgba(0,0,0,0.06)]"
            >
              <!-- Window Title Bar -->
              <div
                class="flex h-9 items-center justify-between border-b border-gray-100 bg-gray-50/70 px-4"
              >
                <!-- Three Small Grey Dots -->
                <div class="flex items-center gap-1.5">
                  <span class="size-2.5 rounded-full bg-gray-300" />
                  <span class="size-2.5 rounded-full bg-gray-300" />
                  <span class="size-2.5 rounded-full bg-gray-300" />
                </div>
                <!-- Tiny Centered Title -->
                <span class="font-mono text-[11px] font-medium tracking-wider text-gray-400">
                  Deagensie Studio
                </span>
                <span class="w-10" />
              </div>

              <!-- Window Body: Sidebar and Main Pane -->
              <div class="flex flex-1 flex-col sm:flex-row">
                <!-- Sidebar Pane -->
                <aside
                  class="flex w-full shrink-0 flex-row items-center justify-between border-b border-gray-100 bg-gray-50/40 p-3 sm:w-[190px] sm:flex-col sm:items-stretch sm:border-r sm:border-b-0 sm:p-4"
                >
                  <!-- Logo Slot (Wide, Bold, Prominent and Responsive) -->
                  <div
                    class="mb-1 flex h-8 w-32 shrink-0 items-center overflow-hidden sm:mb-3 sm:h-10 sm:w-40 lg:w-44"
                  >
                    <img
                      v-if="!logoError"
                      :src="logoUrl"
                      alt="Deagensie"
                      class="w-full origin-center scale-[0.9] object-contain sm:scale-[1.0]"
                      @error="logoError = true"
                    />
                    <span
                      v-else
                      class="text-base font-bold tracking-tight text-gray-900 sm:text-lg"
                    >
                      deagens<span class="text-[#05DED5]">i</span>e
                    </span>
                  </div>

                  <!-- Stage Nav Items -->
                  <nav
                    class="no-scrollbar flex gap-1 overflow-x-auto py-1 sm:flex-col sm:space-y-1 sm:overflow-visible sm:pt-2"
                    role="tablist"
                  >
                    <button
                      v-for="(st, idx) in stages"
                      :key="st.id"
                      type="button"
                      role="tab"
                      :aria-selected="activeStageIndex === idx"
                      class="flex shrink-0 items-center justify-between rounded-lg px-2.5 py-1.5 text-[11px] transition-all duration-300 focus:ring-1 focus:ring-[#04308F] focus:outline-none sm:text-xs"
                      :class="[
                        activeStageIndex === idx
                          ? 'bg-[#04308F]/10 font-semibold text-[#04308F]'
                          : idx < activeStageIndex
                            ? 'font-medium text-gray-700 hover:bg-gray-100/70'
                            : 'font-normal text-gray-400 hover:bg-gray-100/40',
                      ]"
                      @click="goToStage(idx)"
                    >
                      <span class="truncate">{{ st.number }} {{ st.name }}</span>
                      <!-- Completed stage: standard brand cyan tick -->
                      <Icon
                        v-if="idx < activeStageIndex"
                        icon="lucide:check"
                        class="ml-1.5 shrink-0 text-xs font-bold text-[#05DED5]"
                      />
                      <!-- Active stage: filled square indicator -->
                      <span
                        v-else-if="activeStageIndex === idx"
                        class="ml-1.5 size-1.5 shrink-0 rounded-xs bg-[#04308F]"
                      />
                      <!-- Upcoming stage: subtle spacer -->
                      <span v-else class="ml-1.5 size-1.5 shrink-0 rounded-full bg-transparent" />
                    </button>
                  </nav>

                  <!-- Bottom spacer in sidebar -->
                  <div class="hidden px-1 pt-2 font-mono text-[10px] text-gray-400 sm:block">
                    v2.6 // framework
                  </div>
                </aside>

                <!-- Main Pane: Fixed Height ~360px to Prevent Layout Shift -->
                <main
                  class="flex min-h-[340px] flex-1 flex-col justify-between p-4 sm:min-h-[380px] sm:p-5"
                >
                  <div>
                    <!-- Main Pane Header -->
                    <div class="flex items-start justify-between gap-3">
                      <div class="space-y-0.5">
                        <h3
                          class="font-serif text-lg font-semibold tracking-wide text-gray-900 uppercase"
                        >
                          {{ currentStage.name }}
                        </h3>
                        <p class="text-xs leading-relaxed text-gray-500">
                          {{ currentStage.tagline }}
                        </p>
                      </div>
                      <span
                        class="shrink-0 rounded-full border border-gray-200/80 bg-gray-50 px-2.5 py-1 font-mono text-[10px] font-bold text-gray-600"
                      >
                        {{ currentStage.badgeLabel }}
                      </span>
                    </div>

                    <!-- Thin Divider -->
                    <div class="my-3.5 h-px w-full bg-gray-100" />

                    <!-- Section Title -->
                    <div class="mb-3">
                      <span class="text-[11px] font-bold tracking-wider text-gray-400 uppercase">
                        {{
                          currentStage.bodyVariant === 'checklist'
                            ? 'Key deliverables'
                            : 'Live output'
                        }}
                      </span>
                    </div>

                    <!-- BODY VARIANT 1: Checklist -->
                    <div v-if="currentStage.bodyVariant === 'checklist'" class="space-y-3">
                      <div
                        v-for="(deliv, dIdx) in currentStage.deliverables"
                        :key="deliv"
                        class="flex items-center gap-3 transition-all duration-300"
                      >
                        <!-- Resolving Icon Circle -->
                        <div
                          class="flex size-5 shrink-0 items-center justify-center rounded-full transition-colors duration-300"
                          :class="
                            checklistResolved[dIdx]
                              ? 'bg-[#04308F] text-[#05DED5]'
                              : 'border border-gray-300 bg-white'
                          "
                        >
                          <Icon
                            v-if="checklistResolved[dIdx]"
                            icon="lucide:check"
                            class="text-xs font-bold"
                          />
                        </div>

                        <!-- Resolved Text vs Shimmer Skeleton -->
                        <div class="flex-1">
                          <span
                            v-if="checklistResolved[dIdx]"
                            class="text-xs font-medium text-gray-800 transition-opacity duration-300 sm:text-sm"
                          >
                            {{ deliv }}
                          </span>
                          <div v-else class="h-4 w-4/5 animate-pulse rounded bg-gray-200/80" />
                        </div>
                      </div>
                    </div>

                    <!-- BODY VARIANT 2: Terminal -->
                    <div
                      v-else-if="
                        currentStage.bodyVariant === 'terminal' && currentStage.terminalLines
                      "
                      class="space-y-2 rounded-xl border border-white/10 bg-[#020B1E] p-3 font-mono text-[11px] text-white shadow-inner sm:p-3.5 sm:text-xs"
                    >
                      <!-- Command Line -->
                      <div class="flex items-center gap-2 text-cyan-300">
                        <span class="text-gray-500 select-none">></span>
                        <span class="font-semibold">{{ currentStage.terminalLines.command }}</span>
                      </div>

                      <!-- Progress Lines -->
                      <div class="space-y-1 pl-3 text-gray-300">
                        <div
                          v-for="(pLine, pIdx) in currentStage.terminalLines.progress"
                          v-show="terminalStep >= pIdx + 1"
                          :key="pLine"
                          class="flex items-center gap-2 text-gray-300 transition-opacity duration-200"
                        >
                          <span class="text-blue-400">→</span>
                          <span>{{ pLine }}</span>
                        </div>
                      </div>

                      <!-- Check Result Lines -->
                      <div class="space-y-1 pl-3">
                        <div
                          v-for="(cLine, cIdx) in currentStage.terminalLines.checks"
                          v-show="
                            terminalStep >= currentStage.terminalLines.progress.length + cIdx + 1
                          "
                          :key="cLine"
                          class="flex items-center gap-2 font-medium text-[#05DED5] transition-opacity duration-200"
                        >
                          <Icon icon="lucide:check" class="text-xs font-bold" />
                          <span>{{ cLine }}</span>
                        </div>
                      </div>

                      <!-- Final Dim Line -->
                      <div
                        v-show="
                          terminalStep >=
                          currentStage.terminalLines.progress.length +
                            currentStage.terminalLines.checks.length +
                            1
                        "
                        class="pt-0.5 pl-3 text-[10px] text-gray-500 italic sm:text-[11px]"
                      >
                        {{ currentStage.terminalLines.final }}
                      </div>
                    </div>
                  </div>

                  <!-- Checklist Bottom Journey Progress Bar -->
                  <div
                    v-if="currentStage.bodyVariant === 'checklist'"
                    class="space-y-2 border-t border-gray-100 pt-4"
                  >
                    <div class="flex items-center justify-between text-[11px] text-gray-500">
                      <span class="font-medium">Journey progress</span>
                      <span class="font-mono font-bold text-gray-800">
                        {{ currentStage.number }} / 06
                      </span>
                    </div>
                    <div class="flex w-full items-center gap-1.5">
                      <div
                        v-for="seg in 6"
                        :key="seg"
                        :class="[
                          'h-1.5 flex-1 rounded-full transition-all duration-500',
                          seg <= activeStageIndex + 1 ? 'bg-[#04308F]' : 'bg-gray-200',
                        ]"
                      />
                    </div>
                  </div>

                  <!-- Terminal Bottom Status Bar -->
                  <div
                    v-else
                    class="flex items-center justify-between border-t border-gray-100 pt-3 text-[11px] text-gray-500"
                  >
                    <span class="flex items-center gap-1.5">
                      <span class="size-2 animate-pulse rounded-full bg-[#05DED5]" />
                      Execution pipeline active
                    </span>
                    <span class="font-mono font-bold text-gray-800">
                      {{ currentStage.number }} / 06
                    </span>
                  </div>
                </main>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Clickable Keyboard-Focusable Dot Indicators under the card -->
      <div class="flex items-center justify-center gap-2.5 pt-2" role="tablist">
        <button
          v-for="(st, idx) in stages"
          :key="st.id"
          type="button"
          role="tab"
          :aria-selected="activeStageIndex === idx"
          :class="[
            'rounded-full transition-all duration-300 focus:ring-2 focus:ring-[#04308F] focus:ring-offset-2 focus:outline-none',
            activeStageIndex === idx
              ? 'h-2.5 w-8 bg-[#04308F]'
              : 'h-2.5 w-2.5 bg-gray-300 hover:bg-gray-400',
          ]"
          :aria-label="'Switch to stage ' + st.number + ' ' + st.name"
          @click="goToStage(idx)"
        />
      </div>
    </div>
  </section>
</template>

<style scoped>
/* Media crossfade transition */
.media-fade-enter-active,
.media-fade-leave-active {
  transition: opacity 0.6s ease;
}

.media-fade-enter-from,
.media-fade-leave-to {
  opacity: 0;
}

/* Reduced motion accessibility */
@media (prefers-reduced-motion: reduce) {
  *,
  ::before,
  ::after {
    animation-duration: 0.01ms !important;
    animation-iteration-count: 1 !important;
    transition-duration: 0.01ms !important;
  }
}
</style>
