<!--
=============================================================================
DEAGENSIE CORE VALUES COMPONENT (ICE IOCCR)

QUICK CUSTOMIZATION DIRECTORY:
1. Brand Variables: Defined at top of <style scoped> (--brand-primary, --brand-accent, etc.)
2. Values Array: The typed 'values' array below in <script setup> (letter, title, summary, note, detail)
3. Section Heading Copy: Lines in template (eyebrow, title, subtitle)
4. Sequence Timing Constants: ENTRANCE_STAGGER_MS, ENTRANCE_PAUSE_MS, VALUE_DURATION_MS, RESUME_DELAY_MS below
5. Cube Size: Controlled by CSS variable --cube-size in <style scoped> (desktop, 900px, 640px)
=============================================================================
-->

<script setup lang="ts">
import { ref, computed, onMounted, onBeforeUnmount, nextTick } from 'vue';

// ---------------------------------------------------------------------------
// TIMING CONSTANTS (Milliseconds)
// ---------------------------------------------------------------------------
const ENTRANCE_STAGGER_MS = 110;
const ENTRANCE_PAUSE_MS = 600;
const VALUE_DURATION_MS = 2800;
const RESUME_DELAY_MS = 1500;

// ---------------------------------------------------------------------------
// CORE VALUES DATA MODEL
// ---------------------------------------------------------------------------
interface CoreValue {
  letter: string;
  title: string;
  summary: string;
  note: string;
  detail: string[];
}

// Editable placeholder copy for summary, note, and detail for each value
const values: CoreValue[] = [
  {
    letter: 'I',
    title: 'Integrity',
    summary:
      'We deliver on our commitments with uncompromised honesty, accountability, and transparency in every engagement.',
    note: 'Integrity is the anchor of every client partnership and internal process at Deagensie. We do what is right, even when no one is watching.',
    detail: [
      'Integrity is foundational to everything we build at Deagensie. In an industry often clouded by hype and overpromising, we ground our work in radical transparency, objective data, and steadfast reliability.',
      'From governance and pricing to algorithmic ethics and intellectual property protection, we hold ourselves to the highest global standards. Our clients trust us with their core business assets because our word is our bond.',
    ],
  },
  {
    letter: 'C',
    title: 'Creativity',
    summary:
      'We merge artistic vision with strategic discipline to design bold, original solutions that capture global markets.',
    note: 'Creativity transforms complex business challenges into competitive market advantages. We build expressive, unforgettable brand experiences.',
    detail: [
      'Creativity at Deagensie is not merely aesthetic ornamentation; it is our primary problem-solving engine. We combine cross-disciplinary thinking with fearless imagination to unlock unexpected market positioning.',
      'By connecting African creative excellence with enterprise technology, we craft products, identities, and campaigns that cut through saturated digital noise and command global respect.',
    ],
  },
  {
    letter: 'E',
    title: 'Excellence Without Compromise',
    summary:
      'We hold our craft to the most exacting international benchmarks, accepting nothing short of world-class quality.',
    note: 'Excellence is an uncompromising standard applied to every line of code, design asset, and client interaction we deliver.',
    detail: [
      'We reject the notion that good enough is sufficient. Every deliverable produced by our venture teams undergoes rigorous testing, refinement, and review before it reaches the market.',
      'Excellence without compromise means sweating the smallest details, obsessing over performance metrics, and continually raising the bar for what digital craftsmanship from Africa looks like.',
    ],
  },
  {
    letter: 'I',
    title: 'Innovation as a Habit',
    summary:
      'We continuously experiment, automate, and pioneer modern workflows through artificial intelligence and modern tooling.',
    note: 'Innovation is not a sporadic event for us; it is a daily discipline that powers predictive strategy and operational velocity.',
    detail: [
      'True innovation is institutional, not accidental. At Deagensie, we systematically evaluate and adopt emerging AI systems, automation frameworks, and product design methodologies.',
      'We empower our teams and partner businesses to question legacy assumptions, prototype at high speed, and transform technological shifts into durable economic value.',
    ],
  },
  {
    letter: 'O',
    title: 'Ownership',
    summary:
      'We take total personal accountability for outcomes, treating every client venture as if it were our very own.',
    note: 'We act as co-founders and venture stewards, taking full responsibility from ideation all the way through commercial scale.',
    detail: [
      'We operate with an owner mindset. We do not pass blame or hide behind scope limits when obstacles arise; instead, we proactively solve problems and protect client capital.',
      'This depth of ownership creates true alignment of incentives. When our partners succeed, we celebrate real business growth, not merely vanity deliverables.',
    ],
  },
  {
    letter: 'C',
    title: 'Client Success First',
    summary:
      'We measure our ultimate achievement exclusively through the measurable growth and longevity of our partner organizations.',
    note: 'Our roadmap, team allocations, and strategic focus are relentlessly aligned with the commercial triumphs of our clients.',
    detail: [
      'Our business model revolves around partner prosperity. We evaluate every engagement against hard commercial indicators: revenue velocity, customer retention, and brand equity.',
      'We listen deeply, understand the real pressures facing leadership teams, and collaborate as trusted strategic advisors dedicated to accelerating our partners toward market dominance.',
    ],
  },
  {
    letter: 'C',
    title: 'Collaboration',
    summary:
      'We cultivate a borderless ecosystem where diverse disciplines, global clients, and African talents thrive as one unit.',
    note: 'No single discipline wins alone. We bring engineers, designers, strategists, and clients into cohesive, high-trust venture pods.',
    detail: [
      'Great digital enterprises are born from collective intelligence. We break down traditional silos between creative talent, technology specialists, and enterprise decision-makers.',
      'By fostering inclusive communication, psychological safety, and radical collaboration across borders, we unlock creative potential that individual teams could never achieve in isolation.',
    ],
  },
  {
    letter: 'R',
    title: 'Results Matter',
    summary:
      'We prioritize demonstrable business impact and measurable return on investment above subjective opinions and vanity metrics.',
    note: 'At the end of the day, execution is validated by real numbers, operational efficiency, and sustainable revenue growth.',
    detail: [
      'We believe that intention without execution is meaningless. Every creative and technological investment we make must show tangible, demonstrable outcomes for the business.',
      'We set clear key performance metrics at project kickoff, track progress transparently, and continuously iterate until the target business goals are emphatically achieved.',
    ],
  },
];

// Two Acronym Groups: ICE (0, 1, 2) and IOCCR (3, 4, 5, 6, 7)
const iceGroup = computed(() => values.slice(0, 3));
const ioccrGroup = computed(() => values.slice(3, 8));

// ---------------------------------------------------------------------------
// REACTIVE STATE & CONTROLLERS
// ---------------------------------------------------------------------------
const sectionRef = ref<HTMLElement | null>(null);
const cubeRefs = ref<HTMLElement[]>([]);

const hasEntered = ref(false);
const activeIndex = ref<number | null>(null);
const litIndices = ref<Set<number>>(new Set());
const isSequenceFinished = ref(false);
const isHovered = ref(false);
const isTouchDevice = ref(false);

// Note Card State
const activeHoverIndex = ref<number | null>(null);
const noteCardStyle = ref<Record<string, string>>({});

// Modal State
const isModalOpen = ref(false);
const modalValue = ref<CoreValue | null>(null);
const modalRef = ref<HTMLElement | null>(null);
let triggerElement: HTMLElement | null = null;

// Controller run token to prevent overlapping sequences
let runToken = 0;
let autoTimer: ReturnType<typeof setTimeout> | null = null;
let resumeTimer: ReturnType<typeof setTimeout> | null = null;
let entranceTimer: ReturnType<typeof setTimeout> | null = null;
let sectionObserver: IntersectionObserver | null = null;

// ---------------------------------------------------------------------------
// MEANING PANEL DISPLAY HELPERS
// ---------------------------------------------------------------------------
const currentDisplayIndex = computed(() => {
  if (activeHoverIndex.value !== null) return activeHoverIndex.value;
  if (activeIndex.value !== null) return activeIndex.value;
  if (isSequenceFinished.value) return null;
  return 0;
});

const currentDisplayValue = computed(() => {
  if (currentDisplayIndex.value !== null) {
    return values[currentDisplayIndex.value];
  }
  return null;
});

const counterText = computed(() => {
  if (currentDisplayIndex.value !== null) {
    return `0${currentDisplayIndex.value + 1} / 08`;
  }
  return '08 / 08';
});

// ---------------------------------------------------------------------------
// DETERMINISTIC PSEUDO-RANDOM OFFSETS FOR ENTRANCE ZIGZAG
// ---------------------------------------------------------------------------
const getZigzagStyle = (idx: number) => {
  const xOffsets = [-120, 140, -180, 160, -140, 180, -160, 130];
  const yOffsets = [-200, -260, -180, -300, -220, -280, -240, -320];
  const rotX = [45, -60, 50, -45, 60, -50, 40, -55];
  const rotY = [-60, 45, -70, 55, -45, 65, -60, 50];

  return {
    '--scatter-x': `${xOffsets[idx % 8]}px`,
    '--scatter-y': `${yOffsets[idx % 8]}px`,
    '--scatter-rot-x': `${rotX[idx % 8]}deg`,
    '--scatter-rot-y': `${rotY[idx % 8]}deg`,
    '--cube-idx': idx,
    animationDelay: `${idx * ENTRANCE_STAGGER_MS}ms`,
  };
};

// ---------------------------------------------------------------------------
// SEQUENCE RUNNER
// ---------------------------------------------------------------------------
const LOOP_PAUSE_MS = 2400;

const runSequenceStep = (index: number, currentToken: number) => {
  if (currentToken !== runToken) return;

  if (index >= values.length) {
    activeIndex.value = null;
    isSequenceFinished.value = true;
    for (let i = 0; i < values.length; i++) {
      litIndices.value.add(i);
    }

    // Automatically loop back to start once finished
    autoTimer = setTimeout(() => {
      if (currentToken !== runToken || isHovered.value || isModalOpen.value) return;
      litIndices.value.clear();
      isSequenceFinished.value = false;
      runSequenceStep(0, currentToken);
    }, LOOP_PAUSE_MS);
    return;
  }

  isSequenceFinished.value = false;
  activeIndex.value = index;
  litIndices.value.add(index);

  autoTimer = setTimeout(() => {
    if (currentToken !== runToken) return;
    runSequenceStep(index + 1, currentToken);
  }, VALUE_DURATION_MS);
};

const startSequence = (fromIndex = 0) => {
  if (autoTimer) clearTimeout(autoTimer);
  if (resumeTimer) clearTimeout(resumeTimer);

  runToken++;
  const currentToken = runToken;
  isSequenceFinished.value = false;
  runSequenceStep(fromIndex, currentToken);
};

// ---------------------------------------------------------------------------
// HOVER & TOUCH INTERACTIONS
// ---------------------------------------------------------------------------
const handleCubeMouseEnter = (index: number, event: MouseEvent) => {
  if (isTouchDevice.value) return;

  isHovered.value = true;
  runToken++; // Pause auto sequence
  if (autoTimer) clearTimeout(autoTimer);
  if (resumeTimer) clearTimeout(resumeTimer);

  activeHoverIndex.value = index;
  updateNoteCardPosition(event.currentTarget as HTMLElement);
};

const handleCubeMouseLeave = () => {
  if (isTouchDevice.value) return;

  isHovered.value = false;
  activeHoverIndex.value = null;

  if (resumeTimer) clearTimeout(resumeTimer);
  resumeTimer = setTimeout(() => {
    if (isHovered.value || isModalOpen.value) return;
    const nextIndex = activeIndex.value !== null ? (activeIndex.value + 1) % values.length : 0;
    startSequence(nextIndex);
  }, RESUME_DELAY_MS);
};

const updateNoteCardPosition = (targetEl: HTMLElement) => {
  if (!targetEl || typeof window === 'undefined') return;

  const rect = targetEl.getBoundingClientRect();
  const cardWidth = 260;
  const targetLeft = rect.left + rect.width / 2 - cardWidth / 2;
  const clampedLeft = Math.max(16, Math.min(window.innerWidth - cardWidth - 16, targetLeft));
  const arrowX = Math.max(16, Math.min(cardWidth - 16, rect.left + rect.width / 2 - clampedLeft));

  noteCardStyle.value = {
    top: `${Math.max(16, rect.top - 12)}px`,
    left: `${clampedLeft}px`,
    '--arrow-x': `${arrowX}px`,
  };
};

// ---------------------------------------------------------------------------
// CUBE CLICK & MODAL MANAGEMENT
// ---------------------------------------------------------------------------
const handleCubeClick = (index: number) => {
  if (isTouchDevice.value && activeIndex.value !== index) {
    activeIndex.value = index;
    litIndices.value.add(index);
    return;
  }
  openModal(values[index]);
};

const openModal = (value: CoreValue) => {
  triggerElement = document.activeElement as HTMLElement;
  modalValue.value = value;
  isModalOpen.value = true;
  runToken++; // Pause auto sequence while modal is active

  if (typeof document !== 'undefined') {
    document.body.style.overflow = 'hidden';
  }

  nextTick(() => {
    if (modalRef.value) {
      modalRef.value.focus();
    }
  });
};

const closeModal = () => {
  isModalOpen.value = false;
  modalValue.value = null;

  if (typeof document !== 'undefined') {
    document.body.style.overflow = '';
  }

  if (triggerElement) {
    triggerElement.focus();
    triggerElement = null;
  }

  if (!isHovered.value) {
    if (resumeTimer) clearTimeout(resumeTimer);
    resumeTimer = setTimeout(() => {
      const nextIndex = activeIndex.value !== null ? (activeIndex.value + 1) % values.length : 0;
      startSequence(nextIndex);
    }, RESUME_DELAY_MS);
  }
};

const handleModalKeydown = (event: KeyboardEvent) => {
  if (event.key === 'Escape') {
    closeModal();
    return;
  }

  if (event.key === 'Tab' && modalRef.value) {
    const focusable = modalRef.value.querySelectorAll<HTMLElement>(
      'button, [href], input, select, textarea, [tabindex]:not([tabindex="-1"])'
    );
    if (!focusable.length) return;

    const first = focusable[0];
    const last = focusable[focusable.length - 1];

    if (event.shiftKey && document.activeElement === first) {
      last.focus();
      event.preventDefault();
    } else if (!event.shiftKey && document.activeElement === last) {
      first.focus();
      event.preventDefault();
    }
  }
};

// ---------------------------------------------------------------------------
// KEYBOARD ROVING TABINDEX
// ---------------------------------------------------------------------------
const handleCubeKeydown = (event: KeyboardEvent, index: number) => {
  if (event.key === 'ArrowRight') {
    event.preventDefault();
    const nextIdx = (index + 1) % values.length;
    cubeRefs.value[nextIdx]?.focus();
  } else if (event.key === 'ArrowLeft') {
    event.preventDefault();
    const prevIdx = (index - 1 + values.length) % values.length;
    cubeRefs.value[prevIdx]?.focus();
  } else if (event.key === 'Enter' || event.key === ' ') {
    event.preventDefault();
    handleCubeClick(index);
  }
};

// ---------------------------------------------------------------------------
// LIFECYCLE & INTERSECTION OBSERVER
// ---------------------------------------------------------------------------
onMounted(() => {
  if (typeof window !== 'undefined') {
    isTouchDevice.value = 'ontouchstart' in window || navigator.maxTouchPoints > 0;
  }

  if (sectionRef.value && typeof IntersectionObserver !== 'undefined') {
    sectionObserver = new IntersectionObserver(
      (entries) => {
        const [entry] = entries;
        if (entry.isIntersecting && !hasEntered.value) {
          hasEntered.value = true;
          sectionObserver?.disconnect();

          const totalEntranceDuration = 1600 + ENTRANCE_PAUSE_MS;
          entranceTimer = setTimeout(() => {
            startSequence(0);
          }, totalEntranceDuration);
        }
      },
      { threshold: 0.35 }
    );

    sectionObserver.observe(sectionRef.value);
  } else {
    hasEntered.value = true;
    startSequence(0);
  }
});

onBeforeUnmount(() => {
  runToken++;
  if (sectionObserver) sectionObserver.disconnect();
  if (autoTimer) clearTimeout(autoTimer);
  if (resumeTimer) clearTimeout(resumeTimer);
  if (entranceTimer) clearTimeout(entranceTimer);

  if (typeof document !== 'undefined') {
    document.body.style.overflow = '';
  }
});
</script>

<template>
  <section
    id="core-values"
    ref="sectionRef"
    class="values-section"
    aria-labelledby="values-heading"
  >
    <div class="values-container">
      <!-- Section Header -->
      <div class="values-header">
        <span class="values-eyebrow">OUR CORE VALUES</span>
        <h2 id="values-heading" class="values-title">
          Eight values, <span class="values-title-highlight">one standard</span>
        </h2>
        <p class="values-subtitle">
          Our core values reflect what is important to us as a brand, guiding our beliefs,
          attitudes, and behaviors.
        </p>
      </div>

      <!-- 3D Cubes Acronym Row: ICE IOCCR -->
      <div class="cubes-stage" role="region" aria-label="Interactive core values cubes">
        <div class="cubes-wrapper">
          <!-- Group 1: ICE -->
          <div class="cube-group ice-group" role="group" aria-label="ICE Group">
            <div
              v-for="(val, idx) in iceGroup"
              :key="`ice-${idx}`"
              class="cube-scene"
              :class="{ 'has-entered': hasEntered }"
              :style="getZigzagStyle(idx)"
            >
              <div class="cube-bobber">
                <button
                  :ref="
                    (el) => {
                      if (el) cubeRefs[idx] = el as HTMLElement;
                    }
                  "
                  type="button"
                  class="cube"
                  :class="{
                    'is-active': activeIndex === idx || activeHoverIndex === idx,
                    'is-lit': litIndices.has(idx),
                    'is-hovered': activeHoverIndex === idx,
                  }"
                  :aria-label="`${val.letter}, ${val.title}`"
                  :tabindex="activeIndex === idx || (activeIndex === null && idx === 0) ? 0 : -1"
                  @mouseenter="handleCubeMouseEnter(idx, $event)"
                  @mouseleave="handleCubeMouseLeave"
                  @focus="handleCubeMouseEnter(idx, $event)"
                  @blur="handleCubeMouseLeave"
                  @click="handleCubeClick(idx)"
                  @keydown="handleCubeKeydown($event, idx)"
                >
                  <!-- 6 Faces of the 3D Cube -->
                  <div class="cube-face face-front">
                    <span class="cube-letter">{{ val.letter }}</span>
                  </div>
                  <div class="cube-face face-back">
                    <span class="cube-ghost-letter">{{ val.letter }}</span>
                  </div>
                  <div class="cube-face face-right">
                    <span class="cube-ghost-letter">{{ val.letter }}</span>
                  </div>
                  <div class="cube-face face-left">
                    <span class="cube-ghost-letter">{{ val.letter }}</span>
                  </div>
                  <div class="cube-face face-top">
                    <div class="face-pattern" />
                  </div>
                  <div class="cube-face face-bottom">
                    <div class="face-pattern" />
                  </div>
                </button>
              </div>
              <div class="cube-ground-shadow" />
            </div>
          </div>

          <!-- Group 2: IOCCR -->
          <div class="cube-group ioccr-group" role="group" aria-label="IOCCR Group">
            <div
              v-for="(val, offsetIdx) in ioccrGroup"
              :key="`ioccr-${offsetIdx}`"
              class="cube-scene"
              :class="{ 'has-entered': hasEntered }"
              :style="getZigzagStyle(offsetIdx + 3)"
            >
              <div class="cube-bobber">
                <button
                  :ref="
                    (el) => {
                      if (el) cubeRefs[offsetIdx + 3] = el as HTMLElement;
                    }
                  "
                  type="button"
                  class="cube"
                  :class="{
                    'is-active':
                      activeIndex === offsetIdx + 3 || activeHoverIndex === offsetIdx + 3,
                    'is-lit': litIndices.has(offsetIdx + 3),
                    'is-hovered': activeHoverIndex === offsetIdx + 3,
                  }"
                  :aria-label="`${val.letter}, ${val.title}`"
                  :tabindex="activeIndex === offsetIdx + 3 ? 0 : -1"
                  @mouseenter="handleCubeMouseEnter(offsetIdx + 3, $event)"
                  @mouseleave="handleCubeMouseLeave"
                  @focus="handleCubeMouseEnter(offsetIdx + 3, $event)"
                  @blur="handleCubeMouseLeave"
                  @click="handleCubeClick(offsetIdx + 3)"
                  @keydown="handleCubeKeydown($event, offsetIdx + 3)"
                >
                  <!-- 6 Faces of the 3D Cube -->
                  <div class="cube-face face-front">
                    <span class="cube-letter">{{ val.letter }}</span>
                  </div>
                  <div class="cube-face face-back">
                    <span class="cube-ghost-letter">{{ val.letter }}</span>
                  </div>
                  <div class="cube-face face-right">
                    <span class="cube-ghost-letter">{{ val.letter }}</span>
                  </div>
                  <div class="cube-face face-left">
                    <span class="cube-ghost-letter">{{ val.letter }}</span>
                  </div>
                  <div class="cube-face face-top">
                    <div class="face-pattern" />
                  </div>
                  <div class="cube-face face-bottom">
                    <div class="face-pattern" />
                  </div>
                </button>
              </div>
              <div class="cube-ground-shadow" />
            </div>
          </div>
        </div>
      </div>

      <!-- Floating Note Card (Desktop Hover/Focus) -->
      <div
        v-if="activeHoverIndex !== null && !isTouchDevice"
        class="floating-note-card"
        :style="noteCardStyle"
        role="tooltip"
      >
        <div class="note-card-arrow" />
        <div class="note-card-inner">
          <div class="note-card-title">{{ values[activeHoverIndex].title }}</div>
          <p class="note-card-text">{{ values[activeHoverIndex].note }}</p>
          <div class="note-card-hint">Click for full details</div>
        </div>
      </div>

      <!-- Meaning Panel (Structured, centered, fixed min-height 140px) -->
      <div class="meaning-panel" :aria-live="hasEntered ? 'polite' : 'off'" aria-atomic="true">
        <!-- Sequence Progress Indicator -->
        <div class="panel-progress-row">
          <div class="panel-ticks" aria-hidden="true">
            <span
              v-for="(_, tickIdx) in values"
              :key="`tick-${tickIdx}`"
              class="tick"
              :class="{
                'tick-filled': litIndices.has(tickIdx),
                'tick-active': activeIndex === tickIdx || activeHoverIndex === tickIdx,
              }"
            />
          </div>
          <span class="panel-counter">{{ counterText }}</span>
        </div>

        <!-- Meaning Content Area -->
        <div class="panel-content">
          <Transition name="panel-fade" mode="out-in">
            <!-- Active Value Content -->
            <div
              v-if="currentDisplayValue && !isSequenceFinished"
              :key="`val-${currentDisplayValue.title}`"
              class="panel-text-block"
            >
              <h3 class="panel-title">
                {{ currentDisplayValue.title }}
              </h3>
              <p class="panel-summary">
                {{ currentDisplayValue.summary }}
              </p>
              <button type="button" class="panel-read-more" @click="openModal(currentDisplayValue)">
                Read full overview &rarr;
              </button>
            </div>

            <!-- Sequence Completion State (Brief transition before automatic loop) -->
            <div v-else class="panel-completed-block">
              <h3 class="panel-title">Eight values. One standard.</h3>
              <p class="panel-summary">
                Every venture we build and talent we unlock is guided by these enduring commitments.
              </p>
            </div>
          </Transition>
        </div>
      </div>
    </div>

    <!-- Teleported Value Detail Modal -->
    <Teleport to="body">
      <Transition name="modal-fade">
        <div
          v-if="isModalOpen && modalValue"
          class="values-modal-backdrop"
          role="presentation"
          @click.self="closeModal"
        >
          <div
            ref="modalRef"
            class="values-modal-card"
            role="dialog"
            aria-modal="true"
            :aria-labelledby="`modal-title-${modalValue.letter}`"
            tabindex="-1"
            @keydown="handleModalKeydown"
          >
            <!-- Close Button -->
            <button
              type="button"
              class="modal-close-btn"
              aria-label="Close details modal"
              @click="closeModal"
            >
              <span aria-hidden="true">&times;</span>
            </button>

            <!-- Modal Header -->
            <div class="modal-header">
              <div class="modal-letter-badge" aria-hidden="true">
                {{ modalValue.letter }}
              </div>
              <div class="modal-header-text">
                <span class="modal-eyebrow">OUR CORE VALUES</span>
                <h3 :id="`modal-title-${modalValue.letter}`" class="modal-title">
                  {{ modalValue.title }}
                </h3>
              </div>
            </div>

            <!-- Divider Line -->
            <div class="modal-accent-line" />

            <!-- Modal Body Copy -->
            <div class="modal-body">
              <p
                v-for="(para, pIdx) in modalValue.detail"
                :key="`para-${pIdx}`"
                class="modal-paragraph"
              >
                {{ para }}
              </p>
            </div>
          </div>
        </div>
      </Transition>
    </Teleport>
  </section>
</template>

<style scoped>
/* =============================================================================
   BRAND DESIGN SYSTEM VARIABLES (WHITE SECTION THEME)
   ============================================================================= */
.values-section {
  --brand-primary: #04308f;
  --brand-secondary: #0f1e2e;
  --brand-accent: #05ded5;
  --brand-bg: #ffffff;
  --brand-surface: #f8fafc;
  --brand-surface-card: #f4f7fc;
  --brand-text: #0f172a;
  --brand-muted: #64748b;
  --brand-border: #e2e8f0;

  /* Cube Colors */
  --cube-face-default: #ffffff;
  --cube-border-default: #cbd5e1;
  --cube-text-default: #0f172a;

  /* Active & Hover: Black cover with pure white text */
  --cube-face-active: #090e17;
  --cube-border-active: #090e17;
  --cube-text-active: #ffffff;
  --cube-glow: rgba(9, 14, 23, 0.35);

  --cube-size: 84px;
  --half-size: 42px;

  --font-serif: 'Playfair Display', Georgia, 'Source Serif 4', serif;
  --font-sans: 'Open Sauce Sans', Inter, system-ui, -apple-system, sans-serif;

  position: relative;
  width: 100%;
  padding: 96px 20px;
  background-color: var(--brand-bg);
  color: var(--brand-text);
  font-family: var(--font-sans);
  overflow: hidden;
  border-bottom: 1px solid var(--brand-border);
}

.values-container {
  max-width: 1100px;
  margin: 0 auto;
  display: flex;
  flex-direction: column;
  align-items: center;
  position: relative;
}

/* =============================================================================
   SECTION HEADER
   ============================================================================= */
.values-header {
  text-align: center;
  max-width: 760px;
  margin-bottom: 56px;
}

.values-eyebrow {
  display: inline-block;
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 0.18em;
  text-transform: uppercase;
  color: var(--brand-primary);
  background: rgba(4, 48, 143, 0.08);
  padding: 5px 14px;
  border-radius: 9999px;
  margin-bottom: 16px;
}

.values-title {
  font-family: var(--font-serif);
  font-size: clamp(2.2rem, 4.2vw, 3.2rem);
  font-weight: 400;
  line-height: 1.15;
  letter-spacing: -0.02em;
  color: var(--brand-text);
  margin: 0 0 16px 0;
}

.values-title-highlight {
  color: var(--brand-primary);
}

.values-subtitle {
  font-size: clamp(0.95rem, 1.8vw, 1.1rem);
  line-height: 1.6;
  color: var(--brand-muted);
  margin: 0;
}

/* =============================================================================
   3D CUBES STAGE
   ============================================================================= */
.cubes-stage {
  width: 100%;
  display: flex;
  justify-content: center;
  align-items: center;
  padding: 32px 0 44px 0;
}

.cubes-wrapper {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 56px;
  flex-wrap: wrap;
}

.cube-group {
  display: flex;
  align-items: center;
  gap: 18px;
}

/* =============================================================================
   CUBE 3D SCENE & GEOMETRY
   ============================================================================= */
.cube-scene {
  perspective: 900px;
  width: var(--cube-size);
  height: var(--cube-size);
  position: relative;
  opacity: 0;
}

.cube-scene.has-entered {
  animation: cube-zigzag-entrance 1.5s cubic-bezier(0.2, 0.9, 0.3, 1) forwards;
}

.cube-bobber {
  width: 100%;
  height: 100%;
  animation: cube-float-bob 4s ease-in-out infinite;
  animation-delay: calc(var(--cube-idx) * -0.5s);
}

.cube {
  position: relative;
  width: var(--cube-size);
  height: var(--cube-size);
  transform-style: preserve-3d;
  transform: rotateX(-12deg) rotateY(18deg);
  transition: transform 0.6s cubic-bezier(0.25, 1, 0.5, 1);
  background: transparent;
  border: none;
  padding: 0;
  cursor: pointer;
  outline: none;
}

.cube:focus-visible {
  outline: 2px solid var(--brand-primary);
  outline-offset: 8px;
  border-radius: 8px;
}

.cube-face {
  position: absolute;
  width: var(--cube-size);
  height: var(--cube-size);
  top: 0;
  left: 0;
  background: var(--cube-face-default);
  border: 1px solid var(--cube-border-default);
  box-sizing: border-box;
  display: flex;
  align-items: center;
  justify-content: center;
  user-select: none;
  box-shadow: inset 0 0 12px rgba(0, 0, 0, 0.03);
  transition:
    background-color 0.4s ease,
    border-color 0.4s ease,
    color 0.4s ease,
    box-shadow 0.4s ease;
}

/* Face 3D Orientations */
.face-front {
  transform: rotateY(0deg) translateZ(var(--half-size));
}
.face-back {
  transform: rotateY(180deg) translateZ(var(--half-size));
}
.face-right {
  transform: rotateY(90deg) translateZ(var(--half-size));
}
.face-left {
  transform: rotateY(-90deg) translateZ(var(--half-size));
}
.face-top {
  transform: rotateX(90deg) translateZ(var(--half-size));
}
.face-bottom {
  transform: rotateX(-90deg) translateZ(var(--half-size));
}

.cube-letter {
  font-family: var(--font-serif);
  font-size: calc(var(--cube-size) * 0.48);
  font-weight: 600;
  color: var(--cube-text-default);
  line-height: 1;
  transition: color 0.4s ease;
}

.cube-ghost-letter {
  font-family: var(--font-serif);
  font-size: calc(var(--cube-size) * 0.44);
  font-weight: 500;
  color: rgba(15, 23, 42, 0.08);
  line-height: 1;
}

.face-pattern {
  width: 100%;
  height: 100%;
  background-image: radial-gradient(rgba(15, 23, 42, 0.1) 1px, transparent 0);
  background-size: 8px 8px;
  opacity: 0.5;
}

/* Cube Ground Shadow */
.cube-ground-shadow {
  position: absolute;
  bottom: -20px;
  left: 8%;
  width: 84%;
  height: 14px;
  border-radius: 50%;
  background: radial-gradient(ellipse at center, rgba(15, 23, 42, 0.14) 0%, transparent 70%);
  pointer-events: none;
  transition:
    transform 0.5s ease,
    opacity 0.5s ease;
}

/* =============================================================================
   CUBE INTERACTIVE STATES (BLACK COVER WITH WHITE LETTER)
   ============================================================================= */
/* Hover State: black cover on the cube, pure white letter */
.cube.is-hovered {
  transform: rotateX(-4deg) rotateY(8deg) translateZ(26px) scale(1.08) !important;
}

.cube.is-hovered .cube-face {
  background: var(--cube-face-active);
  border-color: var(--cube-border-active);
}

.cube.is-hovered .cube-letter {
  color: var(--cube-text-active) !important;
  font-weight: 700;
}

/* Active Unveiling State (Running through the word) */
.cube.is-active {
  animation: cube-spin-full 0.9s cubic-bezier(0.25, 1, 0.5, 1) forwards;
}

.cube.is-active .cube-face {
  background: var(--cube-face-active);
  border-color: var(--cube-border-active);
  box-shadow: 0 10px 25px var(--cube-glow);
}

.cube.is-active .cube-letter {
  color: var(--cube-text-active) !important;
  font-weight: 700;
}

.cube-scene:has(.cube.is-active) .cube-ground-shadow,
.cube-scene:has(.cube.is-hovered) .cube-ground-shadow {
  transform: scale(1.3);
  opacity: 0.9;
  background: radial-gradient(ellipse at center, rgba(15, 23, 42, 0.28) 0%, transparent 70%);
}

/* Lit (Already Revealed) State */
.cube.is-lit .face-front {
  border-color: var(--brand-primary);
}

.cube.is-lit:not(.is-active):not(.is-hovered) .cube-letter {
  color: var(--brand-primary);
}

/* =============================================================================
   FLOATING NOTE CARD (Desktop Hover Tooltip)
   ============================================================================= */
.floating-note-card {
  position: fixed;
  z-index: 100;
  width: 260px;
  background: #ffffff;
  border: 1px solid var(--brand-border);
  border-radius: 14px;
  padding: 16px 18px;
  box-shadow:
    0 16px 36px rgba(15, 23, 42, 0.12),
    0 4px 12px rgba(15, 23, 42, 0.06);
  pointer-events: none;
  transform: translateY(-100%);
  transition:
    opacity 0.2s ease,
    transform 0.2s ease;
}

.note-card-arrow {
  position: absolute;
  bottom: -6px;
  left: var(--arrow-x, 50%);
  transform: translateX(-50%) rotate(45deg);
  width: 12px;
  height: 12px;
  background: #ffffff;
  border-right: 1px solid var(--brand-border);
  border-bottom: 1px solid var(--brand-border);
}

.note-card-inner {
  display: flex;
  flex-direction: column;
  gap: 6px;
}

.note-card-title {
  font-family: var(--font-serif);
  font-size: 15px;
  font-weight: 600;
  color: var(--brand-primary);
}

.note-card-text {
  font-size: 12px;
  line-height: 1.5;
  color: #475569;
  margin: 0;
}

.note-card-hint {
  font-size: 10px;
  font-weight: 600;
  letter-spacing: 0.05em;
  color: #94a3b8;
  text-transform: uppercase;
  margin-top: 4px;
}

/* =============================================================================
   MEANING PANEL (Structured card layout, min-height 140px)
   ============================================================================= */
.meaning-panel {
  width: 100%;
  max-width: 760px;
  min-height: 160px;
  margin-top: 48px;
  padding: 32px 36px;
  background: var(--brand-surface-card);
  border: 1px solid var(--brand-border);
  border-radius: 24px;
  display: flex;
  flex-direction: column;
  align-items: center;
  text-align: center;
  box-shadow: 0 4px 20px -2px rgba(15, 23, 42, 0.04);
}

.panel-progress-row {
  display: flex;
  align-items: center;
  justify-content: center;
  gap: 16px;
  margin-bottom: 20px;
}

.panel-ticks {
  display: flex;
  align-items: center;
  gap: 6px;
}

.tick {
  width: 20px;
  height: 4px;
  border-radius: 2px;
  background: #cbd5e1;
  transition:
    background-color 0.4s ease,
    transform 0.4s ease;
}

.tick.tick-filled {
  background: var(--brand-primary);
}

.tick.tick-active {
  background: #090e17;
  transform: scaleY(1.4);
}

.panel-counter {
  font-family: monospace;
  font-size: 12px;
  color: #64748b;
  letter-spacing: 0.08em;
  font-weight: 500;
}

.panel-content {
  width: 100%;
}

.panel-text-block,
.panel-completed-block {
  display: flex;
  flex-direction: column;
  align-items: center;
}

.panel-title {
  font-family: var(--font-serif);
  font-size: clamp(1.4rem, 2.5vw, 1.85rem);
  font-weight: 500;
  color: var(--brand-text);
  margin: 0 0 10px 0;
  line-height: 1.25;
}

.panel-summary {
  font-size: clamp(0.95rem, 1.6vw, 1.05rem);
  line-height: 1.65;
  color: var(--brand-muted);
  max-width: 640px;
  margin: 0 0 16px 0;
}

.panel-read-more {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  background: transparent;
  border: none;
  color: var(--brand-primary);
  font-size: 13px;
  font-weight: 600;
  cursor: pointer;
  padding: 4px 8px;
  transition:
    color 0.2s ease,
    transform 0.2s ease;
}

.panel-read-more:hover {
  color: #032163;
  transform: translateX(3px);
}

/* =============================================================================
   MODAL DIALOG (CLEAN WHITE CARD)
   ============================================================================= */
.values-modal-backdrop {
  position: fixed;
  inset: 0;
  z-index: 9999;
  background: rgba(15, 23, 42, 0.65);
  backdrop-filter: blur(8px);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
}

.values-modal-card {
  position: relative;
  width: 100%;
  max-width: 580px;
  background: #ffffff;
  border: 1px solid var(--brand-border);
  border-radius: 24px;
  padding: 38px 36px;
  box-shadow: 0 25px 60px -15px rgba(15, 23, 42, 0.3);
  color: var(--brand-text);
  outline: none;
}

.modal-close-btn {
  position: absolute;
  top: 20px;
  right: 20px;
  width: 36px;
  height: 36px;
  border-radius: 50%;
  background: #f1f5f9;
  border: 1px solid var(--brand-border);
  color: #64748b;
  font-size: 20px;
  line-height: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition: all 0.2s ease;
}

.modal-close-btn:hover {
  background: #e2e8f0;
  color: var(--brand-text);
}

.modal-header {
  display: flex;
  align-items: center;
  gap: 20px;
  margin-bottom: 24px;
}

.modal-letter-badge {
  width: 64px;
  height: 64px;
  background: #090e17;
  border-radius: 18px;
  display: flex;
  align-items: center;
  justify-content: center;
  font-family: var(--font-serif);
  font-size: 32px;
  font-weight: 700;
  color: #ffffff;
  box-shadow: 0 6px 16px rgba(9, 14, 23, 0.25);
  flex-shrink: 0;
}

.modal-header-text {
  display: flex;
  flex-direction: column;
}

.modal-eyebrow {
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 0.15em;
  color: var(--brand-primary);
  text-transform: uppercase;
  margin-bottom: 4px;
}

.modal-title {
  font-family: var(--font-serif);
  font-size: 24px;
  font-weight: 500;
  margin: 0;
  color: var(--brand-text);
}

.modal-accent-line {
  width: 100%;
  height: 1px;
  background: linear-gradient(90deg, var(--brand-primary) 0%, #e2e8f0 40%, transparent 100%);
  margin-bottom: 24px;
}

.modal-body {
  display: flex;
  flex-direction: column;
  gap: 16px;
}

.modal-paragraph {
  font-size: 15px;
  line-height: 1.65;
  color: #475569;
  margin: 0;
}

/* =============================================================================
   KEYFRAME ANIMATIONS
   ============================================================================= */
@keyframes cube-zigzag-entrance {
  0% {
    opacity: 0;
    transform: translate3d(var(--scatter-x), var(--scatter-y), -350px) rotateX(var(--scatter-rot-x))
      rotateY(var(--scatter-rot-y));
  }
  35% {
    opacity: 0.85;
    transform: translate3d(calc(var(--scatter-x) * -0.4), calc(var(--scatter-y) * 0.5), -160px)
      rotateX(calc(var(--scatter-rot-x) * -0.4)) rotateY(calc(var(--scatter-rot-y) * 0.6));
  }
  70% {
    opacity: 1;
    transform: translate3d(calc(var(--scatter-x) * 0.15), -20px, -40px) rotateX(12deg)
      rotateY(-15deg);
  }
  88% {
    transform: translate3d(0, 6px, 0) rotateX(-16deg) rotateY(22deg);
  }
  100% {
    opacity: 1;
    transform: translate3d(0, 0, 0) rotateX(0deg) rotateY(0deg);
  }
}

@keyframes cube-float-bob {
  0%,
  100% {
    transform: translateY(0);
  }
  50% {
    transform: translateY(-6px);
  }
}

@keyframes cube-spin-full {
  0% {
    transform: rotateX(-12deg) rotateY(18deg) scale(1);
  }
  20% {
    transform: rotateX(0deg) rotateY(0deg) scale(1.12);
  }
  80% {
    transform: rotateX(0deg) rotateY(360deg) scale(1.12);
  }
  100% {
    transform: rotateX(0deg) rotateY(360deg) scale(1.12);
  }
}

/* Panel transitions */
.panel-fade-enter-active,
.panel-fade-leave-active {
  transition:
    opacity 0.3s ease,
    transform 0.3s ease;
}

.panel-fade-enter-from {
  opacity: 0;
  transform: translateY(10px);
}

.panel-fade-leave-to {
  opacity: 0;
  transform: translateY(-10px);
}

/* Modal transitions */
.modal-fade-enter-active,
.modal-fade-leave-active {
  transition: opacity 0.3s ease;
}

.modal-fade-enter-from,
.modal-fade-leave-to {
  opacity: 0;
}

.modal-fade-enter-active .values-modal-card {
  transition: transform 0.3s cubic-bezier(0.2, 0.9, 0.3, 1);
}

.modal-fade-enter-from .values-modal-card {
  transform: scale(0.92) translateY(20px);
}

.modal-fade-leave-to .values-modal-card {
  transform: scale(0.95);
}

/* =============================================================================
   RESPONSIVE LAYOUTS
   ============================================================================= */
@media (max-width: 900px) {
  .values-section {
    --cube-size: 68px;
    --half-size: 34px;
    padding: 72px 16px;
  }

  .cubes-wrapper {
    gap: 36px;
  }

  .cube-group {
    gap: 12px;
  }

  .meaning-panel {
    padding: 24px 20px;
  }
}

@media (max-width: 640px) {
  .values-section {
    --cube-size: 64px;
    --half-size: 32px;
    padding: 64px 16px;
  }

  /* Under 640px: groups wrap naturally into a 4x2 grid */
  .cubes-wrapper {
    display: grid;
    grid-template-columns: repeat(4, auto);
    gap: 16px;
    justify-content: center;
  }

  .cube-group {
    display: contents;
  }

  .floating-note-card {
    display: none !important;
  }

  .values-modal-card {
    padding: 28px 20px;
  }

  .modal-letter-badge {
    width: 52px;
    height: 52px;
    font-size: 26px;
  }

  .modal-title {
    font-size: 20px;
  }
}

/* =============================================================================
   ACCESSIBILITY: REDUCED MOTION
   ============================================================================= */
@media (prefers-reduced-motion: reduce) {
  .cube-scene {
    opacity: 1 !important;
    animation: none !important;
  }

  .cube-bobber {
    animation: none !important;
  }

  .cube {
    transition:
      opacity 0.3s ease,
      border-color 0.3s ease !important;
  }

  .cube.is-active,
  .cube.is-hovered {
    animation: none !important;
    transform: rotateX(0deg) rotateY(0deg) scale(1.05) !important;
  }
}
</style>
