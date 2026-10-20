<!--
=============================================================================
DEAGENSIE MEET THE TEAM COMPONENT

QUICK CUSTOMIZATION DIRECTORY:
1. Brand Variables: Defined at top of <style scoped> (--brand-primary, --brand-card-dark, etc.)
2. Headline & Subtitle: Headings in template ("Meet the people behind Deagensie")
3. Team Array: The typed 'team' array in <script setup> (name, role, photo, shortBio, fullBio, linkedin)
4. CTA Card Copy: Title and subtitle in template ("Looking for your next role?")
=============================================================================
-->

<script setup lang="ts">
import { ref, onMounted, onBeforeUnmount, nextTick } from 'vue';

// ---------------------------------------------------------------------------
// DATA MODEL
// ---------------------------------------------------------------------------
interface TeamMember {
  name: string;
  role: string;
  photo: string;
  shortBio: string;
  fullBio: string[];
  linkedin: string;
}

// 11 Team Members filling the 4-column grid (Cell 12 is the Careers CTA card)
const team: TeamMember[] = [
  {
    name: 'Bright Okorafor',
    role: 'Founder & CEO',
    photo: '/images/Bright.jpeg',
    shortBio:
      'Visionary entrepreneur bridging African creative talent with international enterprise opportunities.',
    fullBio: [
      'Bright is a visionary entrepreneur and growth strategist passionate about bridging African creative talent with international enterprise opportunities.',
      'He steers Deagensie strategic direction and global expansion with over a decade of expertise in digital innovation, business acceleration, and brand development.',
    ],
    linkedin: 'https://linkedin.com/in/bright-okorafor',
  },
  {
    name: 'Jennifer Arthur',
    role: 'People & Operations Consultant',
    photo: '/images/Jennifer.jpeg',
    shortBio: 'Fostering operational rhythm, talent onboarding, and international venture culture.',
    fullBio: [
      'Jennifer ensures the people and operational framework of Deagensie thrives with consistency and empathy.',
      'She serves as the connective tissue between strategic leadership and human excellence.',
    ],
    linkedin: 'https://linkedin.com',
  },
  {
    name: 'Peter Bassey Okon',
    role: 'Brand Communication & Marketing Lead',
    photo: '/images/Peter.jpeg',
    shortBio:
      'Orchestrating brand voice, narrative strategy, and multi-channel marketing campaigns.',
    fullBio: [
      'Peter drives Deagensie brand voice, communication strategy, and marketing operations across global touchpoints.',
      'He crafts compelling narratives that connect ventures with high-value audiences, scaling engagement and commercial impact.',
    ],
    linkedin: 'https://linkedin.com',
  },
  {
    name: 'Gift Olungwe',
    role: 'Product Designer',
    photo: '/images/Gift.jpeg',
    shortBio:
      'Blending user-centric architecture with refined visual aesthetics for scalable platforms.',
    fullBio: [
      'Gift combines aesthetic sensibility with user-centered thinking to craft digital products that are both beautiful and functional.',
      'Her work focuses on building scalable design systems and high-converting product interfaces.',
    ],
    linkedin: 'https://linkedin.com',
  },

  {
    name: 'Godwin Enebeli Chinonso',
    role: 'Creative Director',
    photo: '/images/Godwin.jpeg',
    shortBio: 'Translating bold concepts into distinctive brand identities and visual systems.',
    fullBio: [
      'Godwin leads visual art direction, developing distinctive visual systems, digital brand assets, and collateral.',
      'His work elevates how innovative brands present themselves across international markets.',
    ],
    linkedin: 'https://linkedin.com',
  },
  {
    name: 'Okoro Emmanuel Nzube',
    role: 'Lead Full-Stack Engineer',
    photo: '/images/Okoro.jpeg',
    shortBio: 'Engineering resilient web architectures, modern APIs, and AI automation systems.',
    fullBio: [
      'Emmanuel architects and builds robust web applications, data pipelines, and AI product integrations.',
      'He is committed to performance optimization, clean code architectures, and developer excellence.',
    ],
    linkedin: 'https://linkedin.com',
  },
  {
    name: 'Blossom Adaku Obiorah',
    role: 'Executive Operations Lead',
    photo: '/images/Blossom.jpeg',
    shortBio: 'Powering executive coordination, strategic scheduling, and organizational velocity.',
    fullBio: [
      'Blossom keeps the leadership engine operating at peak performance with precision coordination and sharp intelligence.',
      'She manages cross-functional milestones to ensure strategic initiatives land seamlessly.',
    ],
    linkedin: 'https://linkedin.com',
  },
  {
    name: 'Vivian Etim',
    role: 'Brand & Marketing Associate',
    photo: '/images/Vivian.jpeg',
    shortBio: 'Championing audience engagement, creative content, and community growth.',
    fullBio: [
      'Vivian supports brand storytelling, creative copywriting, and social growth campaigns.',
      'Her focus centers on amplifying African creative talent stories across digital media.',
    ],
    linkedin: 'https://linkedin.com',
  },
  // {
  //   name: 'Anthony Olori',
  //   role: 'Head of Venture Strategy',
  //   photo: '/images/pages/about/team/anthony-olori.png',
  //   shortBio: 'Structuring venture models, commercial positioning, and rapid market validation.',
  //   fullBio: [
  //     'Anthony guides startups and enterprise clients through market sizing, business validation, and monetization.',
  //     'He combines financial modeling with creative growth mechanisms to engineer sustainable revenue.'
  //   ],
  //   linkedin: 'https://linkedin.com'
  // },
  // {
  //   name: 'Solabomi Jeminusi',
  //   role: 'Talent & Ecosystem Lead',
  //   photo: '/images/pages/about/team/solabomi-jeminusi.png',
  //   shortBio: 'Connecting elite African creative specialists to high-impact international teams.',
  //   fullBio: [
  //     'Solabomi oversees talent partnerships and ecosystem curation across the continent.',
  //     'She champions borderless collaboration, ensuring creative professionals thrive on global stages.'
  //   ],
  //   linkedin: 'https://linkedin.com'
  // },
  // {
  //   name: 'Victor Ephraim',
  //   role: 'AI & Innovation Specialist',
  //   photo: '/images/pages/about/team/victor-ephraim.png',
  //   shortBio: 'Designing predictive intelligence tools and automated venture operations.',
  //   fullBio: [
  //     'Victor develops applied artificial intelligence frameworks and machine learning workflows.',
  //     'He builds smart tools that eliminate operational friction and accelerate client productivity.'
  //   ],
  //   linkedin: 'https://linkedin.com'
  // }
];

// ---------------------------------------------------------------------------
// STATE & CONTROLLERS
// ---------------------------------------------------------------------------
const activeTouchIndex = ref<number | null>(null);
const selectedMember = ref<TeamMember | null>(null);
const isModalOpen = ref(false);
const modalCardRef = ref<HTMLElement | null>(null);
const closeBtnRef = ref<HTMLElement | null>(null);
let triggerElement: HTMLElement | null = null;
const failedImages = ref<Set<number>>(new Set());

// Touch device detection
const isTouchDevice = ref(false);

const handleImageError = (index: number) => {
  failedImages.value.add(index);
};

const getInitials = (name: string): string => {
  return name
    .split(' ')
    .filter(Boolean)
    .slice(0, 2)
    .map((part) => part[0].toUpperCase())
    .join('');
};

// Touch behavior: first tap reveals card, tapping again or outside closes
const handleTileClick = (index: number, event: MouseEvent) => {
  if (!isTouchDevice.value) return;

  if (activeTouchIndex.value === index) {
    // If already revealed and user taps outside the button, keep or toggle
    return;
  }
  activeTouchIndex.value = index;
  event.stopPropagation();
};

const handleGlobalTouch = () => {
  if (isTouchDevice.value) {
    activeTouchIndex.value = null;
  }
};

// ---------------------------------------------------------------------------
// MODAL MANAGEMENT
// ---------------------------------------------------------------------------
const openModal = (member: TeamMember) => {
  triggerElement = document.activeElement as HTMLElement;
  selectedMember.value = member;
  isModalOpen.value = true;

  if (typeof document !== 'undefined') {
    document.body.style.overflow = 'hidden';
  }

  nextTick(() => {
    if (closeBtnRef.value) {
      closeBtnRef.value.focus();
    } else if (modalCardRef.value) {
      modalCardRef.value.focus();
    }
  });
};

const closeModal = () => {
  isModalOpen.value = false;
  selectedMember.value = null;

  if (typeof document !== 'undefined') {
    document.body.style.overflow = '';
  }

  if (triggerElement) {
    triggerElement.focus();
    triggerElement = null;
  }
};

const handleModalKeydown = (event: KeyboardEvent) => {
  if (event.key === 'Escape') {
    closeModal();
    return;
  }

  if (event.key === 'Tab' && modalCardRef.value) {
    const focusable = modalCardRef.value.querySelectorAll<HTMLElement>(
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
// LIFECYCLE HOOKS
// ---------------------------------------------------------------------------
onMounted(() => {
  if (typeof window !== 'undefined') {
    isTouchDevice.value = window.matchMedia('(hover: none)').matches;
    window.addEventListener('click', handleGlobalTouch);
  }
});

onBeforeUnmount(() => {
  if (typeof window !== 'undefined') {
    window.removeEventListener('click', handleGlobalTouch);
  }
  if (typeof document !== 'undefined') {
    document.body.style.overflow = '';
  }
});

// ---------------------------------------------------------------------------
// METRICS & IMPACT DATA (Andela Reference Style)
// ---------------------------------------------------------------------------
interface MetricItem {
  label: string;
  value: string;
  description?: string;
}

const metrics: MetricItem[] = [
  {
    label: 'Talent ecosystem',
    value: '2,000+',
    description: 'Network of top-rated, highly skilled global creatives',
  },
  {
    label: 'Clients served',
    value: '30+',
    description: 'Happy and returning clients serviced in 1096 days in business.',
  },
  {
    label: 'Intelligent solutions',
    value: '100+',
    description: 'Intelligent solutions delivered',
  },
  {
    label: 'Cost efficiency',
    value: '$10,000',
    description: 'Save of hiring cost with Deagensie',
  },
  {
    label: 'Growth acceleration',
    value: '45%',
    description: '',
  },
];
</script>

<template>
  <div class="team-and-metrics-wrapper">
    <section id="team" class="team-section" aria-labelledby="team-heading">
      <div class="team-container">
        <!-- Section Header -->
        <div class="team-header">
          <h2 id="team-heading" class="team-title">Meet the people behind Deagensie</h2>
          <p class="team-subtitle">
            Strategists, designers, engineers and marketers building ventures end to end.
          </p>
        </div>

        <!-- 4-Column Responsive Team Grid -->
        <div class="team-grid">
          <!-- 11 Team Member Tiles -->
          <div
            v-for="(member, idx) in team"
            :key="member.name"
            class="member-tile"
            :class="{ 'is-revealed': activeTouchIndex === idx }"
            tabindex="0"
            role="group"
            :aria-label="`${member.name}, ${member.role}`"
            @click="handleTileClick(idx, $event)"
            @keydown.enter.self="openModal(member)"
            @keydown.space.self.prevent="openModal(member)"
          >
            <!-- Base Card: Portrait photo (4/5 aspect ratio) + caption -->
            <div class="tile-base">
              <div class="photo-container">
                <img
                  :src="member.photo"
                  :alt="member.name"
                  class="member-photo"
                  loading="lazy"
                  @error="handleImageError(idx)"
                />
                <!-- Gradient fallback with initials if image fails to load -->
                <div v-if="failedImages.has(idx)" class="photo-fallback" aria-hidden="true">
                  <span class="fallback-initials">{{ getInitials(member.name) }}</span>
                </div>
              </div>
              <div class="caption-container">
                <h3 class="member-name">{{ member.name }}</h3>
                <p class="member-role">{{ member.role }}</p>
              </div>
            </div>

            <!-- Dark Bio Hover Panel (Covers entire tile on hover/focus) -->
            <div class="tile-hover-panel">
              <p class="hover-bio">{{ member.shortBio }}</p>
              <button
                type="button"
                class="hover-more-btn"
                :aria-label="`Find out more about ${member.name}`"
                @click.stop="openModal(member)"
              >
                <span>Find out more</span>
                <span class="more-icon-box" aria-hidden="true">
                  <svg viewBox="0 0 16 16" fill="none" class="arrow-svg">
                    <path
                      d="M6 3.5L10.5 8L6 12.5"
                      stroke="currentColor"
                      stroke-width="1.8"
                      stroke-linecap="round"
                      stroke-linejoin="round"
                    />
                  </svg>
                </span>
              </button>
            </div>
          </div>

          <!-- 12th Cell: Careers Call-to-Action Card -->
          <div class="cta-card">
            <div class="cta-top">
              <h3 class="cta-heading">Looking for your next role?</h3>
              <p class="cta-subtext">Work with teams shaping the future of ventures.</p>
            </div>
            <a
              href="https://app-deagensie-waitlist.vercel.app/"
              target="_blank"
              rel="noopener noreferrer"
              class="cta-button"
            >
              Explore opportunities
            </a>
          </div>
        </div>
      </div>
    </section>

    <!-- Section 2: Key Metrics & Impact Grid (Andela Reference Style) -->
    <section class="metrics-section" aria-label="Key performance indicators and network impact">
      <div class="metrics-container">
        <div class="metrics-grid">
          <article v-for="item in metrics" :key="item.value" class="metric-item">
            <div class="metric-label-row">
              <span class="metric-label">{{ item.label }}</span>
            </div>
            <div class="metric-divider" aria-hidden="true" />
            <div class="metric-value-row">
              <span class="metric-value">{{ item.value }}</span>
            </div>
            <p v-if="item.description" class="metric-description">{{ item.description }}</p>
          </article>
        </div>

        <!-- Centered Pill Action Button -->
        <div class="metrics-cta-row">
          <NuxtLink to="/why" class="metrics-cta-btn"> Explore our model </NuxtLink>
        </div>
      </div>
    </section>

    <!-- Teleported Profile Modal -->
    <Teleport to="body">
      <Transition name="modal-pop">
        <div
          v-if="isModalOpen && selectedMember"
          class="team-modal-backdrop"
          role="presentation"
          @click.self="closeModal"
        >
          <div
            ref="modalCardRef"
            class="team-modal-card"
            role="dialog"
            aria-modal="true"
            :aria-labelledby="`modal-title-${selectedMember.name.replace(/\s+/g, '-')}`"
            tabindex="-1"
            @keydown="handleModalKeydown"
          >
            <!-- Left Column: Portrait & LinkedIn Badge -->
            <div class="modal-portrait-col">
              <img :src="selectedMember.photo" :alt="selectedMember.name" class="modal-photo" />
              <!-- LinkedIn Badge Anchor -->
              <a
                :href="selectedMember.linkedin"
                target="_blank"
                rel="noopener noreferrer"
                class="linkedin-badge"
                aria-label="Open LinkedIn profile"
              >
                <svg
                  viewBox="0 0 24 24"
                  fill="currentColor"
                  class="linkedin-svg"
                  aria-hidden="true"
                >
                  <path
                    d="M19 3a2 2 0 0 1 2 2v14a2 2 0 0 1-2 2H5a2 2 0 0 1-2-2V5a2 2 0 0 1 2-2h14m-.5 15.5v-5.3a3.26 3.26 0 0 0-3.26-3.26c-.85 0-1.84.52-2.28 1.3v-1.11h-2.79v8.37h2.79v-4.93c0-.77.62-1.4 1.39-1.4a1.4 1.4 0 0 1 1.4 1.4v4.93h2.75M6.46 10.9h2.79v8.37H6.46v-8.37M7.86 6.72a1.62 1.62 0 1 0 0 3.24 1.62 1.62 0 0 0 0-3.24"
                  />
                </svg>
              </a>
            </div>

            <!-- Right Column: Header & Scrollable Bio -->
            <div class="modal-content-col">
              <div class="modal-header-row">
                <div class="modal-title-group">
                  <h3
                    :id="`modal-title-${selectedMember.name.replace(/\s+/g, '-')}`"
                    class="modal-member-name"
                  >
                    {{ selectedMember.name }}
                  </h3>
                  <p class="modal-member-role">{{ selectedMember.role }}</p>
                </div>
                <button
                  ref="closeBtnRef"
                  type="button"
                  class="modal-close-icon-btn"
                  aria-label="Close"
                  @click="closeModal"
                >
                  <span aria-hidden="true">&times;</span>
                </button>
              </div>

              <!-- Scrollable Bio Body -->
              <div class="modal-bio-scroll">
                <p
                  v-for="(paragraph, pIdx) in selectedMember.fullBio"
                  :key="pIdx"
                  class="modal-bio-paragraph"
                >
                  {{ paragraph }}
                </p>
              </div>
            </div>
          </div>
        </div>
      </Transition>
    </Teleport>
  </div>
</template>

<style scoped>
/* =============================================================================
   DEAGENSIE BRAND DESIGN TOKENS
   ============================================================================= */
.team-and-metrics-wrapper,
.team-section {
  --brand-primary: #04308f;
  --brand-secondary: #0f1e2e;
  --brand-accent: #05ded5;
  --brand-bg: #ffffff;
  --brand-surface: #f8fafc;
  --brand-card-dark: #0f1e2e;
  --brand-text: #0f172a;
  --brand-muted: #64748b;
  --brand-border: #e2e8f0;
  --brand-overlay: rgba(15, 30, 46, 0.55);

  --font-serif: 'Playfair Display', Georgia, 'Source Serif 4', serif;
  --font-sans: 'Open Sauce Sans', Inter, system-ui, -apple-system, sans-serif;
  --font-open-sans: 'Open Sans', sans-serif;

  position: relative;
  width: 100%;
  padding-top: 80px;
  background-color: var(--brand-bg);
  color: var(--brand-text);
  font-family: var(--font-sans);
}

.team-container {
  max-width: 1100px;
  margin: 0 auto;
  padding: 0 20px 80px 20px;
}

/* =============================================================================
   SECTION HEADER
   ============================================================================= */
.team-header {
  text-align: center;
  max-width: 780px;
  margin: 0 auto 56px auto;
}

.team-title {
  font-family: var(--font-serif);
  font-size: clamp(32px, 4vw, 44px);
  font-weight: 400;
  line-height: 1.15;
  letter-spacing: -0.02em;
  color: var(--brand-text);
  margin: 0 0 16px 0;
}

.team-subtitle {
  font-size: 16px;
  line-height: 1.6;
  color: var(--brand-muted);
  margin: 0;
}

/* =============================================================================
   4-COLUMN TEAM GRID
   ============================================================================= */
.team-grid {
  display: grid;
  grid-template-columns: repeat(4, 1fr);
  gap: 20px;
}

/* =============================================================================
   MEMBER TILE & HOVER REVEAL
   ============================================================================= */
.member-tile {
  position: relative;
  border-radius: 12px;
  overflow: hidden;
  background-color: var(--brand-bg);
  cursor: pointer;
  outline: none;
  display: flex;
  flex-direction: column;
}

.member-tile:focus-visible {
  outline: 2px solid var(--brand-accent);
  outline-offset: 4px;
}

.tile-base {
  display: flex;
  flex-direction: column;
  width: 100%;
}

.photo-container {
  position: relative;
  width: 100%;
  aspect-ratio: 4 / 5;
  border-radius: 12px;
  overflow: hidden;
  background-color: var(--brand-card-dark);
}

.member-photo {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.photo-fallback {
  position: absolute;
  inset: 0;
  display: flex;
  align-items: center;
  justify-content: center;
  background: linear-gradient(135deg, var(--brand-primary), var(--brand-card-dark));
}

.fallback-initials {
  font-family: var(--font-serif);
  font-size: 36px;
  font-weight: 600;
  color: #ffffff;
  letter-spacing: 0.05em;
}

.caption-container {
  padding-top: 12px;
}

.member-name {
  font-size: 15px;
  font-weight: 500;
  color: var(--brand-text);
  margin: 0;
  line-height: 1.35;
}

.member-role {
  font-size: 13px;
  color: var(--brand-muted);
  margin: 3px 0 0 0;
  line-height: 1.35;
}

/* Dark Bio Hover Panel covering entire tile */
.tile-hover-panel {
  position: absolute;
  inset: 0;
  border-radius: 12px;
  background-color: var(--brand-card-dark);
  padding: 20px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  opacity: 0;
  pointer-events: none;
  transition: opacity 280ms ease;
  z-index: 2;
  box-sizing: border-box;
}

.hover-bio {
  font-size: 17px;
  line-height: 1.45;
  color: #ffffff;
  margin: 0;
  transform: translateY(6px);
  transition: transform 280ms ease;
}

.hover-more-btn {
  display: inline-flex;
  align-items: center;
  gap: 8px;
  background: transparent;
  border: none;
  color: var(--brand-accent);
  font-size: 13px;
  font-weight: 500;
  padding: 0;
  cursor: pointer;
  align-self: flex-start;
  transition: opacity 0.2s ease;
}

.hover-more-btn:hover {
  opacity: 0.85;
}

.more-icon-box {
  width: 22px;
  height: 22px;
  border-radius: 6px;
  background: rgba(5, 222, 213, 0.15);
  display: flex;
  align-items: center;
  justify-content: center;
  color: var(--brand-accent);
}

.arrow-svg {
  width: 12px;
  height: 12px;
}

/* Hover on desktop */
@media (hover: hover) {
  .member-tile:hover .tile-hover-panel,
  .member-tile:focus-within .tile-hover-panel {
    opacity: 1;
    pointer-events: auto;
  }

  .member-tile:hover .hover-bio,
  .member-tile:focus-within .hover-bio {
    transform: translateY(0);
  }
}

/* Touch devices */
.member-tile.is-revealed .tile-hover-panel {
  opacity: 1;
  pointer-events: auto;
}

.member-tile.is-revealed .hover-bio {
  transform: translateY(0);
}

/* =============================================================================
   CAREERS CALL-TO-ACTION CARD (12th cell)
   ============================================================================= */
.cta-card {
  border-radius: 12px;
  background-color: var(--brand-surface);
  border: 1px solid var(--brand-border);
  padding: 24px;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  box-sizing: border-box;
}

.cta-top {
  display: flex;
  flex-direction: column;
}

.cta-heading {
  font-family: var(--font-serif);
  font-size: clamp(22px, 2.2vw, 26px);
  font-weight: 400;
  line-height: 1.25;
  color: var(--brand-text);
  margin: 0 0 10px 0;
}

.cta-subtext {
  font-size: 14px;
  line-height: 1.55;
  color: var(--brand-muted);
  margin: 0;
}

.cta-button {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 12px 22px;
  border-radius: 9999px;
  background-color: var(--brand-card-dark);
  color: #ffffff;
  font-size: 13px;
  font-weight: 600;
  text-decoration: none;
  transition: all 0.2s ease;
  align-self: flex-start;
  margin-top: 24px;
}

.cta-button:hover {
  background-color: var(--brand-primary);
  transform: translateY(-1px);
}

.cta-button:focus-visible {
  outline: 2px solid var(--brand-accent);
  outline-offset: 3px;
}

/* =============================================================================
   BOTTOM DARK BRAND BAND
   ============================================================================= */
.brand-bottom-band {
  width: 100%;
  min-height: 96px;
  background-color: var(--brand-card-dark);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 24px 20px;
  box-sizing: border-box;
}

.band-content {
  max-width: 1100px;
  width: 100%;
  display: flex;
  align-items: center;
  justify-content: space-between;
  gap: 20px;
  flex-wrap: wrap;
}

.band-text {
  font-size: 13px;
  color: rgba(255, 255, 255, 0.7);
  letter-spacing: 0.02em;
}

.band-wordmark {
  font-family: var(--font-serif);
  font-size: 15px;
  font-weight: 700;
  letter-spacing: 0.2em;
  color: #ffffff;
}

/* =============================================================================
   PROFILE MODAL
   ============================================================================= */
.team-modal-backdrop {
  position: fixed;
  inset: 0;
  z-index: 9999;
  background-color: var(--brand-overlay);
  backdrop-filter: blur(6px);
  display: flex;
  align-items: center;
  justify-content: center;
  padding: 20px;
  box-sizing: border-box;
}

.team-modal-card {
  position: relative;
  background: #ffffff;
  border-radius: 16px;
  max-width: 720px;
  width: 92vw;
  max-height: 80vh;
  padding: 16px;
  box-shadow: 0 25px 60px rgba(0, 0, 0, 0.35);
  display: flex;
  gap: 20px;
  overflow: hidden;
  outline: none;
  box-sizing: border-box;
}

.modal-portrait-col {
  width: 38%;
  flex-shrink: 0;
  position: relative;
  border-radius: 12px;
  overflow: hidden;
  background-color: var(--brand-card-dark);
}

.modal-photo {
  width: 100%;
  height: 100%;
  object-fit: cover;
  display: block;
}

.linkedin-badge {
  position: absolute;
  bottom: 12px;
  left: 12px;
  width: 36px;
  height: 36px;
  border-radius: 8px;
  background-color: #0a66c2; /* Hardcoded LinkedIn brand color */
  color: #ffffff;
  display: flex;
  align-items: center;
  justify-content: center;
  box-shadow: 0 4px 12px rgba(10, 102, 194, 0.4);
  transition:
    transform 0.2s ease,
    opacity 0.2s ease;
  z-index: 3;
}

.linkedin-badge:hover {
  transform: scale(1.08);
}

.linkedin-badge:focus-visible {
  outline: 2px solid #ffffff;
  outline-offset: 2px;
}

.linkedin-svg {
  width: 20px;
  height: 20px;
}

.modal-content-col {
  flex: 1;
  min-width: 0;
  display: flex;
  flex-direction: column;
}

.modal-header-row {
  display: flex;
  align-items: flex-start;
  justify-content: space-between;
  gap: 16px;
  padding-bottom: 14px;
  border-bottom: 1px solid var(--brand-border);
}

.modal-title-group {
  display: flex;
  flex-direction: column;
}

.modal-member-name {
  font-size: 18px;
  font-weight: 600;
  color: var(--brand-text);
  margin: 0;
}

.modal-member-role {
  font-size: 13px;
  color: var(--brand-muted);
  margin: 4px 0 0 0;
}

.modal-close-icon-btn {
  width: 40px;
  height: 40px;
  border-radius: 50%;
  background: transparent;
  border: none;
  color: var(--brand-muted);
  font-size: 24px;
  line-height: 1;
  display: flex;
  align-items: center;
  justify-content: center;
  cursor: pointer;
  transition:
    background-color 0.2s ease,
    color 0.2s ease;
  flex-shrink: 0;
}

.modal-close-icon-btn:hover {
  background-color: #f1f5f9;
  color: var(--brand-text);
}

.modal-close-icon-btn:focus-visible {
  outline: 2px solid var(--brand-accent);
}

.modal-bio-scroll {
  flex: 1;
  overflow-y: auto;
  padding: 16px 8px 12px 0;
  display: flex;
  flex-direction: column;
  gap: 12px;
}

/* Thin custom scrollbar */
.modal-bio-scroll::-webkit-scrollbar {
  width: 4px;
}

.modal-bio-scroll::-webkit-scrollbar-track {
  background: transparent;
}

.modal-bio-scroll::-webkit-scrollbar-thumb {
  background: var(--brand-border);
  border-radius: 4px;
}

.modal-bio-paragraph {
  font-size: 14px;
  line-height: 1.6;
  color: #475569;
  margin: 0;
}

/* =============================================================================
   MODAL POP TRANSITIONS
   ============================================================================= */
.modal-pop-enter-active,
.modal-pop-leave-active {
  transition: opacity 250ms ease;
}

.modal-pop-enter-from,
.modal-pop-leave-to {
  opacity: 0;
}

.modal-pop-enter-active .team-modal-card {
  transition:
    transform 250ms cubic-bezier(0.2, 0.9, 0.3, 1),
    opacity 250ms ease;
}

.modal-pop-enter-from .team-modal-card {
  transform: scale(0.96);
  opacity: 0;
}

.modal-pop-leave-to .team-modal-card {
  transform: scale(0.96);
  opacity: 0;
}

/* =============================================================================
   RESPONSIVE BREAKPOINTS
   ============================================================================= */
@media (max-width: 900px) {
  .team-grid {
    grid-template-columns: repeat(2, 1fr);
    gap: 18px;
  }

  .team-container {
    padding-bottom: 60px;
  }
}

@media (max-width: 640px) {
  .team-modal-card {
    flex-direction: column;
    max-height: 88vh;
    padding: 16px;
    gap: 14px;
  }

  .modal-portrait-col {
    width: 100%;
    height: 220px;
  }

  .band-content {
    flex-direction: column;
    text-align: center;
    gap: 10px;
  }
}

@media (max-width: 520px) {
  .team-grid {
    grid-template-columns: 1fr;
    gap: 20px;
  }

  .cta-card {
    min-height: 240px;
  }
}

/* =============================================================================
   METRICS & IMPACT SECTION (Andela Reference Style)
   ============================================================================= */
.metrics-section {
  width: 100%;
  background-color: #ffffff;
  padding: 40px 20px 100px 20px;
  box-sizing: border-box;
}

.metrics-container {
  max-width: 1100px;
  margin: 0 auto;
}

.metrics-grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  column-gap: 56px;
  row-gap: 56px;
}

.metric-item {
  display: flex;
  flex-direction: column;
}

.metric-label-row {
  margin-bottom: 14px;
}

.metric-label {
  font-family: var(--font-open-sans, 'Open Sans', sans-serif);
  font-size: 15px;
  font-weight: 600;
  color: #0f172a;
  letter-spacing: -0.01em;
}

.metric-divider {
  width: 100%;
  height: 1px;
  background-color: #e2e8f0;
  margin-bottom: 24px;
}

.metric-value-row {
  margin-bottom: 16px;
}

.metric-value {
  font-family: var(--font-open-sans, 'Open Sans', sans-serif);
  font-size: clamp(40px, 4.5vw, 58px);
  font-weight: 700;
  line-height: 1.05;
  letter-spacing: -0.03em;
  color: #081320;
}

.metric-description {
  font-family: var(--font-open-sans, 'Open Sans', sans-serif);
  font-size: 15px;
  line-height: 1.6;
  color: #64748b;
  margin: 0;
  max-width: 320px;
}

/* Centered Pill Action Button */
.metrics-cta-row {
  margin-top: 68px;
  display: flex;
  justify-content: center;
}

.metrics-cta-btn {
  display: inline-flex;
  align-items: center;
  justify-content: center;
  padding: 13px 32px;
  border-radius: 9999px;
  background-color: #0e1b2a;
  color: #ffffff;
  font-size: 14px;
  font-weight: 600;
  text-decoration: none;
  box-shadow: 0 4px 12px rgba(14, 27, 42, 0.15);
  transition: all 0.25s cubic-bezier(0.16, 1, 0.3, 1);
}

.metrics-cta-btn:hover {
  background-color: var(--brand-primary);
  color: #ffffff;
  transform: translateY(-2px);
  box-shadow: 0 6px 18px rgba(4, 48, 143, 0.25);
}

.metrics-cta-btn:focus-visible {
  outline: 2px solid var(--brand-primary);
  outline-offset: 4px;
}

/* Responsive adjustments for Metrics */
@media (max-width: 960px) {
  .metrics-grid {
    grid-template-columns: repeat(2, 1fr);
    column-gap: 40px;
    row-gap: 48px;
  }

  .metrics-section {
    padding: 30px 20px 80px 20px;
  }
}

@media (max-width: 640px) {
  .metrics-grid {
    grid-template-columns: 1fr;
    row-gap: 36px;
  }

  .metric-divider {
    margin-bottom: 18px;
  }

  .metric-value-row {
    margin-bottom: 12px;
  }

  .metric-description {
    max-width: 100%;
  }

  .metrics-cta-row {
    margin-top: 48px;
  }

  .metrics-section {
    padding: 20px 16px 64px 16px;
  }
}

/* =============================================================================
   ACCESSIBILITY: REDUCED MOTION
   ============================================================================= */
@media (prefers-reduced-motion: reduce) {
  .tile-hover-panel,
  .hover-bio,
  .modal-pop-enter-active,
  .modal-pop-leave-active,
  .modal-pop-enter-active .team-modal-card {
    transition: opacity 0.2s ease !important;
    transform: none !important;
  }
}
</style>
