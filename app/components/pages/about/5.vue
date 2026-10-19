<!--
=============================================================================
DEAGENSIE TIMELINE / OUR JOURNEY COMPONENT

QUICK CUSTOMIZATION DIRECTORY:
1. Brand Variables: Defined at top of <style scoped> (--brand-bg-dark, --brand-accent, etc.)
2. Headline & Subtitle: Headings in template ("Our journey", "Deagensie has been turning...")
3. Reading Line Offset: READING_LINE_OFFSET constant in <script setup> (default 0.3 for 30vh)
4. Milestones Array: The typed 'milestones' array in <script setup> (date, title, text, image, etc.)
5. Closing Strip Copy: Heading and button in closing section template
=============================================================================
-->

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount } from 'vue';

// ---------------------------------------------------------------------------
// TIMELINE CONSTANTS & CONFIGURATION
// ---------------------------------------------------------------------------
const READING_LINE_OFFSET = 0.3; // 30% from the top of the viewport

interface Milestone {
  date: string;
  title: string;
  text: string | string[];
  image: string;
  imageAlt: string;
  linkLabel?: string;
  linkHref?: string;
}

// 3 Definitive Historical Milestones: In the Beginning, Consolidation, and The Transition
const milestones: Milestone[] = [
  {
    date: '2023',
    title: 'In the Beginning',
    text: [
      "It started with a question. What if building a venture didn't have to feel so difficult? After years of working closely with businesses and witnessing firsthand the challenges entrepreneurs face, we stepped into a dream: to build something that helps ambitious people turn ideas into ventures - and ventures into growing businesses. That dream became theAgency.",
    ],
    image: '/images/pages/about/who-we-are.webp',
    imageAlt: 'The founding vision and genesis of theAgency in 2023',
    linkLabel: 'DISCOVER OUR FOUNDATION',
    linkHref: '/about',
  },
  {
    date: '2024 - 2025',
    title: 'Consolidation',
    text: [
      'For three years, we worked alongside founders, ventures, organisations and institutions, turning ideas into identities, identities into experiences, and experiences into platforms. We built a system that delivered real value and turned those values into real revenue worth over $100,000.',
      'Every project taught us something. Every founder showed us another gap. Every challenge revealed a bigger opportunity. Talent and opportunity remain disconnected. Brilliant people are searching for opportunities to prove themselves, while businesses struggle to find the right people to help them grow. We saw ambition, potential, ideas waiting to become something meaningful, and talent waiting for the right opportunity. And we decided to do something about it.',
    ],
    image: '/images/pages/about/hero-2.png',
    imageAlt: 'Consolidation, venture scaling, and talent connectivity',
    linkLabel: 'EXPLORE OUR VENTURES',
    linkHref: '/business',
  },
  {
    date: '2026',
    title: 'The Transition',
    text: [
      'Somewhere along the journey, we stopped asking: "How can we build another brand?" And started asking: "How can we make it easier for ambitious people to build, grow and thrive?" That became our next chapter - Deagensie. Today, Deagensie has evolved beyond the traditional creative agency. We are building an ecosystem designed around two fundamental needs: helping ventures build the systems they need to grow, and connecting exceptional creative talent to the opportunities where they can thrive.',
    ],
    image: '/images/pages/about/hero.webp',
    imageAlt: 'The transition to Deagensie and ecosystem expansion',
    linkLabel: 'JOIN THE ECOSYSTEM',
    linkHref: 'https://app-deagensie-waitlist.vercel.app/',
  },
];

// ---------------------------------------------------------------------------
// REACTIVE STATE & SCROLL TRACKING
// ---------------------------------------------------------------------------
const timelineContainerRef = ref<HTMLElement | null>(null);
const rowRefs = ref<HTMLElement[]>([]);
const revealedIndices = ref<Set<number>>(new Set());

const activeIndex = ref<number>(-1);
const scrollProgress = ref<number>(0);
const failedImages = ref<Set<number>>(new Set());

let rAFId: number | null = null;
let intersectionObserver: IntersectionObserver | null = null;

const handleImageError = (index: number) => {
  failedImages.value.add(index);
};

// ---------------------------------------------------------------------------
// SCROLL PROGRESS COMPUTATION (requestAnimationFrame)
// ---------------------------------------------------------------------------
const updateScrollState = () => {
  if (!timelineContainerRef.value || typeof window === 'undefined') return;

  const rect = timelineContainerRef.value.getBoundingClientRect();
  const readingLineY = window.innerHeight * READING_LINE_OFFSET;
  const totalHeight = rect.height;

  // Compute how far the reading line has traveled through the container
  const distance = readingLineY - rect.top;
  const progress = Math.max(0, Math.min(1, distance / totalHeight));
  scrollProgress.value = progress;

  // Compute active milestone based on row tops vs reading line
  let currentActive = -1;
  for (let i = 0; i < rowRefs.value.length; i++) {
    const rowEl = rowRefs.value[i];
    if (!rowEl) continue;
    const rowRect = rowEl.getBoundingClientRect();
    if (rowRect.top <= readingLineY + 30) {
      currentActive = i;
    }
  }
  activeIndex.value = currentActive;
};

const handleScroll = () => {
  if (rAFId !== null) return;
  rAFId = requestAnimationFrame(() => {
    updateScrollState();
    rAFId = null;
  });
};

// Smooth anchor scrolling when clicking date
const scrollToMilestone = (index: number) => {
  const rowEl = rowRefs.value[index];
  if (!rowEl || typeof window === 'undefined') return;

  const rowRect = rowEl.getBoundingClientRect();
  const readingLineY = window.innerHeight * READING_LINE_OFFSET;
  const targetTop = window.scrollY + rowRect.top - readingLineY;

  window.scrollTo({
    top: targetTop,
    behavior: 'smooth',
  });
};

// ---------------------------------------------------------------------------
// LIFECYCLE HOOKS
// ---------------------------------------------------------------------------
onMounted(() => {
  if (typeof window !== 'undefined') {
    window.addEventListener('scroll', handleScroll, { passive: true });
    window.addEventListener('resize', handleScroll, { passive: true });
    updateScrollState();

    // IntersectionObserver to reveal milestone content once
    intersectionObserver = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting) {
            const idxStr = (entry.target as HTMLElement).dataset.index;
            if (idxStr !== undefined) {
              revealedIndices.value.add(Number(idxStr));
              intersectionObserver?.unobserve(entry.target);
            }
          }
        });
      },
      { threshold: 0.15 }
    );

    rowRefs.value.forEach((rowEl) => {
      if (rowEl) intersectionObserver?.observe(rowEl);
    });
  }
});

onBeforeUnmount(() => {
  if (typeof window !== 'undefined') {
    window.removeEventListener('scroll', handleScroll);
    window.removeEventListener('resize', handleScroll);
  }
  if (rAFId !== null) {
    cancelAnimationFrame(rAFId);
    rAFId = null;
  }
  if (intersectionObserver) {
    intersectionObserver.disconnect();
    intersectionObserver = null;
  }
});
</script>

<template>
  <div class="journey-wrapper">
    <!-- Main Dark Timeline Section -->
    <section id="our-journey" class="journey-section" aria-labelledby="journey-heading">
      <div class="journey-container">
        <!-- Section Header -->
        <header class="journey-header">
          <span class="journey-eyebrow">OUR HISTORY</span>
          <h2 id="journey-heading" class="journey-title">Our journey</h2>
          <p class="journey-subtitle">
            Deagensie has been turning ventures into scalable brands, one milestone at a time.
          </p>
        </header>

        <!-- Vertical Timeline Body -->
        <div ref="timelineContainerRef" class="timeline-body">
          <!-- Continuous 2px Track & Overlay Progress Line -->
          <div class="timeline-line-track" aria-hidden="true">
            <div
              class="timeline-line-progress"
              :style="{ transform: `scaleY(${scrollProgress})` }"
            />
          </div>

          <!-- Milestones Ordered List -->
          <ol class="milestones-list">
            <li
              v-for="(item, idx) in milestones"
              :key="item.date"
              :ref="
                (el) => {
                  if (el) rowRefs[idx] = el as HTMLElement;
                }
              "
              :data-index="idx"
              class="milestone-row"
              :class="{
                'is-active': activeIndex === idx,
                'is-passed': activeIndex > idx,
                'is-upcoming': activeIndex < idx,
                'is-revealed': revealedIndices.has(idx),
              }"
            >
              <!-- LEFT COLUMN: Sticky Date Label & Center Dot -->
              <div class="milestone-sticky-rail">
                <div class="sticky-pin-wrapper">
                  <button
                    type="button"
                    class="date-button"
                    :aria-label="`Scroll to milestone ${item.date}`"
                    @click="scrollToMilestone(idx)"
                  >
                    <time class="date-label">{{ item.date }}</time>
                  </button>

                  <!-- Milestone Indicator Dot centered on the line -->
                  <div class="timeline-dot" aria-hidden="true" />
                </div>
              </div>

              <!-- RIGHT COLUMN: Body Text, Image Card, & Link -->
              <div class="milestone-content">
                <div class="content-reveal-wrapper">
                  <h3 class="milestone-title">
                    {{ item.title }}
                  </h3>
                  <div class="milestone-text-wrap">
                    <p
                      v-for="(para, pIdx) in Array.isArray(item.text) ? item.text : [item.text]"
                      :key="pIdx"
                      class="milestone-text"
                    >
                      {{ para }}
                    </p>
                  </div>

                  <!-- Rounded Image Card -->
                  <div class="image-card">
                    <img
                      :src="item.image"
                      :alt="item.imageAlt"
                      class="milestone-img"
                      loading="lazy"
                      @error="handleImageError(idx)"
                    />
                    <!-- Fallback if image fails to load -->
                    <div v-if="failedImages.has(idx)" class="image-fallback" aria-hidden="true">
                      <span class="fallback-tag">{{ item.date }}</span>
                    </div>
                  </div>

                  <!-- Optional Tiny Uppercase Link -->
                  <div v-if="item.linkLabel" class="link-wrapper">
                    <NuxtLink :to="item.linkHref || '/about'" class="milestone-link">
                      <span>{{ item.linkLabel }}</span>
                      <svg viewBox="0 0 16 16" fill="none" class="link-arrow" aria-hidden="true">
                        <path
                          d="M6 3.5L10.5 8L6 12.5"
                          stroke="currentColor"
                          stroke-width="1.8"
                          stroke-linecap="round"
                          stroke-linejoin="round"
                        />
                      </svg>
                    </NuxtLink>
                  </div>
                </div>
              </div>
            </li>
          </ol>
        </div>
      </div>
    </section>

    <!-- Closing Light Strip (Visible Dark-to-Light Transition) -->
    <aside class="closing-strip" aria-label="Explore Deagensie">
      <div class="closing-container">
        <h3 class="closing-heading">Explore what Deagensie can build with you</h3>
        <p class="closing-subtitle">
          Partner with our venture teams to engineer sustainable growth and build world-class
          digital platforms.
        </p>
        <NuxtLink to="/contact" class="closing-cta-btn"> Get in touch </NuxtLink>
      </div>
    </aside>
  </div>
</template>

<style scoped>
/* =============================================================================
   BRAND DESIGN TOKENS
   ============================================================================= */
.journey-wrapper {
  --brand-bg-dark: #081320;
  --brand-surface-dark: #0f1e2e;
  --brand-text-on-dark: #f8fafc;
  --brand-muted-on-dark: #94a3b8;
  --brand-accent: #05ded5;
  --brand-line-track: rgba(255, 255, 255, 0.12);
  --brand-light-bg: #ffffff;
  --brand-text: #0f172a;
  --brand-primary: #04308f;

  --font-serif: 'Playfair Display', Georgia, 'Source Serif 4', serif;
  --font-sans: 'Open Sauce Sans', Inter, system-ui, -apple-system, sans-serif;

  width: 100%;
  font-family: var(--font-sans);
}

/* =============================================================================
   MAIN DARK TIMELINE SECTION
   ============================================================================= */
.journey-section {
  width: 100%;
  background-color: var(--brand-bg-dark);
  color: var(--brand-text-on-dark);
  padding: 96px 20px 120px 20px;
  position: relative;
  box-sizing: border-box;
}

.journey-container {
  max-width: 960px;
  margin: 0 auto;
}

/* Header */
.journey-header {
  text-align: center;
  max-width: 680px;
  margin: 0 auto 80px auto;
}

.journey-eyebrow {
  display: inline-block;
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 0.2em;
  text-transform: uppercase;
  color: var(--brand-accent);
  margin-bottom: 14px;
}

.journey-title {
  font-family: var(--font-serif);
  font-size: clamp(32px, 4.5vw, 48px);
  font-weight: 400;
  line-height: 1.15;
  letter-spacing: -0.02em;
  color: #ffffff;
  margin: 0 0 16px 0;
}

.journey-subtitle {
  font-size: 16px;
  line-height: 1.6;
  color: var(--brand-muted-on-dark);
  margin: 0;
}

/* =============================================================================
   TIMELINE BODY & CONTINUOUS TRACK
   ============================================================================= */
.timeline-body {
  position: relative;
  width: 100%;
}

/* 2px Continuous Vertical Track (42% from left of container) */
.timeline-line-track {
  position: absolute;
  top: 0;
  bottom: 0;
  left: 42%;
  width: 2px;
  background-color: var(--brand-line-track);
  transform: translateX(-50%);
  pointer-events: none;
  z-index: 1;
}

.timeline-line-progress {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background-color: var(--brand-accent);
  transform-origin: top;
  will-change: transform;
  box-shadow: 0 0 10px var(--brand-accent);
}

/* Milestones List */
.milestones-list {
  list-style: none;
  padding: 0;
  margin: 0;
  display: flex;
  flex-direction: column;
}

/* Milestone Row: Tall rows with bottom spacing for sticky reading line */
.milestone-row {
  position: relative;
  display: flex;
  margin-bottom: 140px;
  min-height: 440px;
}

.milestone-row:last-child {
  margin-bottom: 40px;
}

/* =============================================================================
   LEFT COLUMN: STICKY DATE & DOT
   ============================================================================= */
.milestone-sticky-rail {
  width: 42%;
  flex-shrink: 0;
  position: relative;
}

/* Sticky wrapper pinned at 30vh (the reading line) */
.sticky-pin-wrapper {
  position: sticky;
  top: 30vh;
  display: flex;
  align-items: center;
  justify-content: flex-end;
  width: 100%;
}

.date-button {
  display: inline-flex;
  align-items: center;
  justify-content: flex-end;
  padding: 0;
  margin-right: 48px;
  background: transparent;
  border: none;
  cursor: pointer;
  outline: none;
  box-sizing: border-box;
}

.date-button:focus-visible .date-label {
  outline: 2px solid var(--brand-accent);
  outline-offset: 4px;
  border-radius: 4px;
}

.date-label {
  display: inline-block;
  font-size: 28px;
  font-weight: 500;
  letter-spacing: -0.01em;
  color: var(--brand-muted-on-dark);
  transition: color 400ms ease;
  white-space: nowrap;
}

/* 10px Indicator Dot centered on the vertical line (right edge of 42% rail) */
.timeline-dot {
  position: absolute;
  right: 0;
  top: 50%;
  transform: translate(50%, -50%);
  width: 10px;
  height: 10px;
  border-radius: 50%;
  background-color: #475569;
  border: 2px solid var(--brand-bg-dark);
  box-sizing: content-box;
  z-index: 3;
  transition: all 400ms cubic-bezier(0.2, 0.9, 0.3, 1);
}

/* =============================================================================
   RIGHT COLUMN: BODY, IMAGE & LINK
   ============================================================================= */
.milestone-content {
  width: 58%;
  flex-grow: 1;
  padding-left: 48px;
  box-sizing: border-box;
}

.content-reveal-wrapper {
  opacity: 0;
  transform: translateY(24px);
  transition:
    opacity 600ms ease,
    transform 600ms ease;
}

.milestone-row.is-revealed .content-reveal-wrapper {
  opacity: 1;
  transform: translateY(0);
}

.milestone-title {
  font-family: var(--font-serif);
  font-size: 22px;
  font-weight: 500;
  color: #ffffff;
  margin: 0 0 10px 0;
  line-height: 1.3;
}

.milestone-text-wrap {
  margin: 0 0 20px 0;
  max-width: 380px;
}

.milestone-text {
  font-size: 15px;
  line-height: 1.65;
  color: var(--brand-muted-on-dark);
  margin: 0 0 12px 0;
  transition: color 400ms ease;
}

.milestone-text:last-child {
  margin-bottom: 0;
}

/* Rounded Image Card */
.image-card {
  position: relative;
  width: 100%;
  max-width: 380px;
  aspect-ratio: 4 / 3;
  border-radius: 14px;
  overflow: hidden;
  background-color: var(--brand-surface-dark);
  margin-bottom: 16px;
  border: 1px solid rgba(255, 255, 255, 0.08);
}

.milestone-img {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
  filter: grayscale(1) brightness(0.55);
  opacity: 0.8;
  transform: scale(0.98);
  transition:
    filter 400ms ease,
    opacity 400ms ease,
    transform 400ms ease;
}

.image-fallback {
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, var(--brand-primary), var(--brand-surface-dark));
}

.fallback-tag {
  font-family: var(--font-serif);
  font-size: 22px;
  font-weight: 600;
  color: #ffffff;
}

/* Optional Uppercase Link */
.link-wrapper {
  margin-top: 8px;
}

.milestone-link {
  display: inline-flex;
  align-items: center;
  gap: 6px;
  font-size: 11px;
  font-weight: 700;
  letter-spacing: 0.12em;
  color: var(--brand-accent);
  text-decoration: none;
  text-transform: uppercase;
  transition:
    color 0.2s ease,
    transform 0.2s ease;
}

.milestone-link:hover {
  color: #ffffff;
  transform: translateX(3px);
}

.milestone-link:focus-visible {
  outline: 2px solid var(--brand-accent);
  outline-offset: 3px;
  border-radius: 2px;
}

.link-arrow {
  width: 12px;
  height: 12px;
}

/* =============================================================================
   VISUAL STATES (400ms EASE TRANSITIONS)
   ============================================================================= */
/* ACTIVE STATE (At Reading Line) */
.milestone-row.is-active .date-label {
  color: #ffffff;
  font-weight: 600;
}

.milestone-row.is-active .timeline-dot {
  width: 14px;
  height: 14px;
  background-color: #ffffff;
  box-shadow:
    0 0 0 5px rgba(5, 222, 213, 0.28),
    0 0 16px var(--brand-accent);
}

.milestone-row.is-active .milestone-text {
  color: #ffffff;
}

.milestone-row.is-active .milestone-img {
  filter: none;
  opacity: 1;
  transform: scale(1);
}

/* PASSED STATE (Already Scrolled Past) */
.milestone-row.is-passed .date-label {
  color: #cbd5e1;
}

.milestone-row.is-passed .timeline-dot {
  width: 10px;
  height: 10px;
  background-color: var(--brand-accent);
  border-color: var(--brand-bg-dark);
  box-shadow: 0 0 8px rgba(5, 222, 213, 0.4);
}

.milestone-row.is-passed .milestone-text {
  color: #cbd5e1;
}

.milestone-row.is-passed .milestone-img {
  filter: none;
  opacity: 0.9;
  transform: scale(1);
}

/* UPCOMING STATE (Below Reading Line) */
.milestone-row.is-upcoming .date-label {
  color: var(--brand-muted-on-dark);
}

.milestone-row.is-upcoming .timeline-dot {
  width: 8px;
  height: 8px;
  background-color: #334155;
  border-color: var(--brand-bg-dark);
  opacity: 0.7;
}

.milestone-row.is-upcoming .milestone-text {
  color: var(--brand-muted-on-dark);
}

/* =============================================================================
   CLOSING LIGHT STRIP (VISIBLY SHIFTS FROM DARK TO LIGHT)
   ============================================================================= */
.closing-strip {
  width: 100%;
  background-color: var(--brand-light-bg);
  color: var(--brand-text);
  padding: 80px 20px;
  text-align: center;
  box-sizing: border-box;
  border-top: 1px solid rgba(0, 0, 0, 0.06);
}

.closing-container {
  max-width: 680px;
  margin: 0 auto;
}

.closing-heading {
  font-family: var(--font-serif);
  font-size: clamp(26px, 3.5vw, 36px);
  font-weight: 400;
  line-height: 1.25;
  color: var(--brand-text);
  margin: 0 0 14px 0;
}

.closing-subtitle {
  font-size: 16px;
  line-height: 1.6;
  color: #64748b;
  margin: 0 0 28px 0;
}

.closing-cta-btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 14px 32px;
  border-radius: 9999px;
  background-color: var(--brand-primary);
  color: #ffffff;
  font-size: 14px;
  font-weight: 600;
  text-decoration: none;
  box-shadow: 0 4px 14px rgba(4, 48, 143, 0.25);
  transition: all 0.3s ease;
}

.closing-cta-btn:hover {
  background-color: var(--brand-accent);
  color: #0f172a;
  transform: translateY(-2px);
}

.closing-cta-btn:focus-visible {
  outline: 2px solid var(--brand-primary);
  outline-offset: 4px;
}

/* =============================================================================
   RESPONSIVE LAYOUTS (UNDER 768px)
   ============================================================================= */
@media (max-width: 768px) {
  .journey-section {
    padding: 72px 16px 80px 16px;
  }

  .journey-header {
    margin-bottom: 56px;
  }

  /* Move vertical line to left edge */
  .timeline-line-track {
    left: 16px;
  }

  .milestone-row {
    flex-direction: column;
    margin-bottom: 72px;
    min-height: auto;
  }

  /* Stack date above content on the right of the line */
  .milestone-sticky-rail {
    width: 100%;
    margin-bottom: 12px;
  }

  .sticky-pin-wrapper {
    position: sticky;
    top: 80px;
    display: flex;
    align-items: center;
    justify-content: flex-start;
    padding-left: 44px;
    z-index: 2;
    background: transparent;
  }

  .date-button {
    margin-right: 0;
    text-align: left;
    justify-content: flex-start;
  }

  .date-label {
    font-size: 20px;
  }

  /* Dot moves to left edge on the line at 16px */
  .timeline-dot {
    position: absolute;
    left: 16px;
    right: auto;
    top: 50%;
    transform: translate(-50%, -50%);
  }

  .milestone-content {
    width: 100%;
    padding-left: 44px;
  }

  .milestone-text {
    max-width: 100%;
  }

  .image-card {
    max-width: 100%;
  }

  .closing-strip {
    padding: 60px 16px;
  }
}

/* =============================================================================
   ACCESSIBILITY: REDUCED MOTION
   ============================================================================= */
@media (prefers-reduced-motion: reduce) {
  .content-reveal-wrapper,
  .milestone-img,
  .timeline-dot,
  .date-label,
  .milestone-text {
    transition: none !important;
    transform: none !important;
    opacity: 1 !important;
    filter: none !important;
  }

  .timeline-line-progress {
    transform: scaleY(1) !important;
  }
}
</style>
