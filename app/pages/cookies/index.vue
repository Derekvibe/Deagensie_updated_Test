<script setup lang="ts">
import { Icon } from '@iconify/vue';
import { push } from 'notivue';

definePageMeta({
  alias: ['/cookie-policy'],
});

const sections = [
  { id: 'what-are-cookies', label: '1. What Are Cookies?' },
  { id: 'why-we-use-cookies', label: '2. Why We Use Cookies' },
  { id: 'preferences-manager', label: '3. Interactive Preferences' },
  { id: 'cookie-categories', label: '4. Cookie Categories' },
  { id: 'cookie-inventory', label: '5. Detailed Cookie Table' },
  { id: 'third-party-services', label: '6. Third-Party Services' },
  { id: 'browser-controls', label: '7. Managing Browser Settings' },
  { id: 'dnt-gpc-signals', label: '8. DNT & Global Privacy Control' },
  { id: 'policy-updates', label: '9. Policy Updates & Inquiries' },
];

const activeSection = ref('what-are-cookies');

// Interactive Cookie Preferences State
const cookiePreferences = reactive({
  necessary: true, // Always locked
  functional: true,
  analytics: true,
  marketing: false,
});

const savedNotification = ref(false);

function saveCookiePreferences() {
  if (import.meta.client) {
    try {
      localStorage.setItem('deag_cookie_preferences', JSON.stringify(cookiePreferences));
      savedNotification.value = true;
      push.success({
        title: 'Preferences Updated',
        message: 'Your cookie choices have been saved successfully.',
      });
      setTimeout(() => {
        savedNotification.value = false;
      }, 4000);
    } catch {
      // Graceful fallback for local storage restriction
    }
  }
}

function acceptAllCookies() {
  cookiePreferences.functional = true;
  cookiePreferences.analytics = true;
  cookiePreferences.marketing = true;
  saveCookiePreferences();
}

onMounted(() => {
  if (import.meta.client) {
    try {
      const stored = localStorage.getItem('deag_cookie_preferences');
      if (stored) {
        const parsed = JSON.parse(stored);
        cookiePreferences.functional = !!parsed.functional;
        cookiePreferences.analytics = !!parsed.analytics;
        cookiePreferences.marketing = !!parsed.marketing;
      }
    } catch {
      // Use defaults
    }
  }

  const observer = new IntersectionObserver(
    (entries) => {
      for (const entry of entries) {
        if (entry.isIntersecting) {
          activeSection.value = entry.target.id;
          break;
        }
      }
    },
    {
      rootMargin: '-100px 0px -60% 0px',
      threshold: 0,
    }
  );

  for (const s of sections) {
    const el = document.getElementById(s.id);
    if (el) observer.observe(el);
  }

  onUnmounted(() => observer.disconnect());
});
</script>

<template>
  <div class="min-h-screen bg-white">
    <!-- Hero & Tabs -->
    <PagesLegalLegalHero
      title="Cookie Policy"
      subtitle="How Deagensie uses cookies, local storage, and tracking technologies to ensure platform security, streamline multi-step onboarding, and optimize user experience."
      active-page="cookies"
      last-updated="October 13, 2026"
      reading-time="7 min read"
    />

    <!-- Main Content Layout -->
    <div class="mx-auto w-5/6 max-w-7xl py-12 lg:py-16">
      <div class="grid grid-cols-1 gap-12 lg:grid-cols-[280px_1fr] lg:gap-16">
        <!-- Sidebar Navigation (Desktop Sticky) -->
        <aside class="hidden lg:block">
          <div class="sticky top-28 space-y-6">
            <div class="rounded-2xl border border-gray-100 bg-gray-50/80 p-5">
              <h3 class="mb-4 text-xs font-bold tracking-wider text-gray-900 uppercase">
                Contents
              </h3>
              <nav aria-label="Table of Contents" class="space-y-1">
                <a
                  v-for="item in sections"
                  :key="item.id"
                  :href="`#${item.id}`"
                  :class="[
                    'block rounded-lg px-3 py-2 text-xs font-medium transition-all duration-150',
                    activeSection === item.id
                      ? 'bg-[#04308F] font-semibold text-white shadow-xs'
                      : 'text-gray-600 hover:bg-gray-200/60 hover:text-gray-900',
                  ]"
                >
                  {{ item.label }}
                </a>
              </nav>
            </div>

            <!-- Quick Action to Jump to Preferences -->
            <div class="rounded-2xl border border-teal-100 bg-teal-50/60 p-5 text-xs text-gray-700">
              <div class="mb-2 flex items-center gap-2 font-semibold text-teal-800">
                <Icon icon="solar:slider-minimalistic-horizontal-bold" class="text-base" />
                <span>Instant Controls</span>
              </div>
              <p class="leading-relaxed text-gray-600">
                You can adjust your cookie consent settings at any time using our on-page manager.
              </p>
              <a
                href="#preferences-manager"
                class="mt-3 inline-block font-semibold text-teal-800 hover:underline"
              >
                Open Preferences &darr;
              </a>
            </div>
          </div>
        </aside>

        <!-- Document Body -->
        <article class="prose-like space-y-12 text-gray-700">
          <!-- Key Takeaways Highlight Box -->
          <div class="rounded-3xl border border-teal-100 bg-teal-50/40 p-6 sm:p-8">
            <div class="mb-3 flex items-center gap-2.5">
              <div
                class="flex h-8 w-8 items-center justify-center rounded-full bg-teal-700 text-white"
              >
                <Icon icon="solar:cookie-bold" class="text-lg" />
              </div>
              <h3 class="font-serif text-lg font-bold text-gray-900">
                Cookie Transparency Principles
              </h3>
            </div>
            <ul class="grid gap-3 pt-2 text-sm text-gray-700 sm:grid-cols-2">
              <li class="flex items-start gap-2.5">
                <Icon icon="solar:check-circle-bold" class="mt-0.5 shrink-0 text-teal-700" />
                <span
                  ><strong>No Invasive Tracking:</strong> We do not use third-party data broker ad
                  trackers.</span
                >
              </li>
              <li class="flex items-start gap-2.5">
                <Icon icon="solar:check-circle-bold" class="mt-0.5 shrink-0 text-teal-700" />
                <span
                  ><strong>Form Wizard Resilience:</strong> Local storage saves your multi-step
                  registration steps so work is never lost.</span
                >
              </li>
              <li class="flex items-start gap-2.5">
                <Icon icon="solar:check-circle-bold" class="mt-0.5 shrink-0 text-teal-700" />
                <span
                  ><strong>Granular Control:</strong> You can toggle functional, analytical, and
                  marketing cookies at will.</span
                >
              </li>
              <li class="flex items-start gap-2.5">
                <Icon icon="solar:check-circle-bold" class="mt-0.5 shrink-0 text-teal-700" />
                <span
                  ><strong>Strictly Necessary Security:</strong> Essential cookies safeguard tokens,
                  CSRF integrity, and DDoS prevention.</span
                >
              </li>
            </ul>
          </div>

          <!-- Section 1 -->
          <section id="what-are-cookies" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              1. What Are Cookies & Tracking Technologies?
            </h2>
            <p class="leading-relaxed">
              Cookies are compact text files placed onto your computer, tablet, or mobile phone by
              websites that you visit. They are widely utilized by web platforms to make sites
              operate efficiently, ensure secure browsing, and provide valuable operational data to
              website administrators.
            </p>
            <p class="leading-relaxed">
              In addition to standard HTTP cookies, Deagensie may use related web technologies such
              as:
            </p>
            <ul class="list-disc space-y-2 pl-6">
              <li>
                <strong>Local Storage & Session Storage:</strong> HTML5 client-side storage
                mechanisms allowing our web application to store registration drafts and UI
                preferences locally on your device without transmitting them across every HTTP
                header.
              </li>
              <li>
                <strong>IndexedDB:</strong> In-browser storage employed for high-performance offline
                caching and registration data resilience.
              </li>
              <li>
                <strong>Pixel Tags & Web Beacons:</strong> Small transparent image snippets used in
                transactional emails to confirm message delivery.
              </li>
            </ul>
          </section>

          <!-- Section 2 -->
          <section id="why-we-use-cookies" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              2. Why Deagensie Uses Cookies
            </h2>
            <p class="leading-relaxed">
              We employ cookies and browser storage technologies across the Deagensie platform to
              fulfill several critical objectives:
            </p>
            <ul class="list-disc space-y-2 pl-6">
              <li>
                <strong>Session Continuity:</strong> Keeping you securely signed in to client
                project workspaces and creative profile portals.
              </li>
              <li>
                <strong>Form Persistence:</strong> Ensuring that complex multi-stage flows (such as
                our Business Registration Flow at <code>/register/business</code> and Creative
                Registration Flow at <code>/register/creative</code>) preserve your inputs even if
                your connection reloads.
              </li>
              <li>
                <strong>Platform Security:</strong> Protecting against cross-site request forgery
                (CSRF), credential stuffing, and bot scraping.
              </li>
              <li>
                <strong>Performance Optimization:</strong> Measuring page load speeds, resource
                caching, and identifying broken links or rendering anomalies.
              </li>
            </ul>
          </section>

          <!-- Section 3: Interactive Preferences Manager -->
          <section id="preferences-manager" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              3. Interactive Cookie Preferences Manager
            </h2>
            <p class="leading-relaxed">
              You maintain direct control over non-essential cookies. Use the interactive controls
              below to configure your preferences. Your selections will take effect immediately and
              remain saved on this browser:
            </p>

            <div class="space-y-6 rounded-3xl border border-gray-200 bg-gray-50/70 p-6 sm:p-8">
              <div
                class="flex flex-wrap items-center justify-between gap-4 border-b border-gray-200 pb-4"
              >
                <div>
                  <h4 class="text-base font-bold text-gray-900 sm:text-lg">
                    Your Cookie Preferences
                  </h4>
                  <p class="text-xs text-gray-500">
                    Configure your privacy settings for this browser session.
                  </p>
                </div>
                <button
                  type="button"
                  class="rounded-full bg-gray-900 px-4 py-2 text-xs font-semibold text-white transition-all hover:scale-105 hover:bg-gray-800"
                  @click="acceptAllCookies"
                >
                  Accept All Cookies
                </button>
              </div>

              <!-- Strictly Necessary (Locked) -->
              <div
                class="flex items-start justify-between gap-4 rounded-2xl border border-gray-200 bg-white p-4"
              >
                <div class="space-y-1">
                  <div class="flex items-center gap-2">
                    <span class="text-sm font-semibold text-gray-900"
                      >Strictly Necessary Cookies</span
                    >
                    <span
                      class="rounded-md bg-gray-100 px-2 py-0.5 text-[10px] font-bold text-gray-600 uppercase"
                      >Always Active</span
                    >
                  </div>
                  <p class="text-xs text-gray-500">
                    Mandatory for core site security, user authentication, CSRF tokens, and basic
                    navigation. Cannot be disabled.
                  </p>
                </div>
                <div class="shrink-0 pt-1">
                  <div
                    class="flex h-6 w-11 cursor-not-allowed items-center rounded-full bg-[#04308F] p-1 opacity-75"
                  >
                    <div class="h-4 w-4 translate-x-5 transform rounded-full bg-white" />
                  </div>
                </div>
              </div>

              <!-- Functional & Experience -->
              <div
                class="flex items-start justify-between gap-4 rounded-2xl border border-gray-200 bg-white p-4"
              >
                <div class="space-y-1">
                  <div class="flex items-center gap-2">
                    <span class="text-sm font-semibold text-gray-900"
                      >Functional & Persistence Storage</span
                    >
                    <span
                      class="rounded-md bg-blue-50 px-2 py-0.5 text-[10px] font-bold text-[#04308F] uppercase"
                      >Recommended</span
                    >
                  </div>
                  <p class="text-xs text-gray-500">
                    Stores multi-step registration drafts, portfolio filter selections, back-to-top
                    scroll position, and UI states.
                  </p>
                </div>
                <div class="shrink-0 pt-1">
                  <button
                    type="button"
                    :aria-checked="cookiePreferences.functional"
                    role="switch"
                    class="relative inline-flex h-6 w-11 shrink-0 cursor-pointer rounded-full border-2 border-transparent transition-colors duration-200 ease-in-out focus:outline-hidden"
                    :class="cookiePreferences.functional ? 'bg-[#04308F]' : 'bg-gray-300'"
                    @click="cookiePreferences.functional = !cookiePreferences.functional"
                  >
                    <span
                      class="pointer-events-none inline-block h-5 w-5 transform rounded-full bg-white shadow-sm ring-0 transition duration-200 ease-in-out"
                      :class="cookiePreferences.functional ? 'translate-x-5' : 'translate-x-0'"
                    />
                  </button>
                </div>
              </div>

              <!-- Performance & Analytics -->
              <div
                class="flex items-start justify-between gap-4 rounded-2xl border border-gray-200 bg-white p-4"
              >
                <div class="space-y-1">
                  <div class="flex items-center gap-2">
                    <span class="text-sm font-semibold text-gray-900">Performance & Analytics</span>
                  </div>
                  <p class="text-xs text-gray-500">
                    Gathers anonymous, aggregate usage telemetry to help us diagnose slow page
                    components and optimize matchmaking.
                  </p>
                </div>
                <div class="shrink-0 pt-1">
                  <button
                    type="button"
                    :aria-checked="cookiePreferences.analytics"
                    role="switch"
                    class="relative inline-flex h-6 w-11 shrink-0 cursor-pointer rounded-full border-2 border-transparent transition-colors duration-200 ease-in-out focus:outline-hidden"
                    :class="cookiePreferences.analytics ? 'bg-[#04308F]' : 'bg-gray-300'"
                    @click="cookiePreferences.analytics = !cookiePreferences.analytics"
                  >
                    <span
                      class="pointer-events-none inline-block h-5 w-5 transform rounded-full bg-white shadow-sm ring-0 transition duration-200 ease-in-out"
                      :class="cookiePreferences.analytics ? 'translate-x-5' : 'translate-x-0'"
                    />
                  </button>
                </div>
              </div>

              <!-- Marketing & Attribution -->
              <div
                class="flex items-start justify-between gap-4 rounded-2xl border border-gray-200 bg-white p-4"
              >
                <div class="space-y-1">
                  <div class="flex items-center gap-2">
                    <span class="text-sm font-semibold text-gray-900"
                      >Marketing & Referral Attribution</span
                    >
                  </div>
                  <p class="text-xs text-gray-500">
                    Tracks early-access waitlist referral links and attribution for growth
                    campaigns. No data broker retargeting.
                  </p>
                </div>
                <div class="shrink-0 pt-1">
                  <button
                    type="button"
                    :aria-checked="cookiePreferences.marketing"
                    role="switch"
                    class="relative inline-flex h-6 w-11 shrink-0 cursor-pointer rounded-full border-2 border-transparent transition-colors duration-200 ease-in-out focus:outline-hidden"
                    :class="cookiePreferences.marketing ? 'bg-[#04308F]' : 'bg-gray-300'"
                    @click="cookiePreferences.marketing = !cookiePreferences.marketing"
                  >
                    <span
                      class="pointer-events-none inline-block h-5 w-5 transform rounded-full bg-white shadow-sm ring-0 transition duration-200 ease-in-out"
                      :class="cookiePreferences.marketing ? 'translate-x-5' : 'translate-x-0'"
                    />
                  </button>
                </div>
              </div>

              <!-- Save Action -->
              <div class="flex items-center justify-between pt-2">
                <span
                  v-if="savedNotification"
                  class="flex items-center gap-1.5 text-xs font-semibold text-emerald-600"
                >
                  <Icon icon="solar:check-circle-bold" />
                  Preferences updated and saved!
                </span>
                <span v-else class="text-xs text-gray-400">
                  Settings are stored locally in your browser.
                </span>

                <button
                  type="button"
                  class="rounded-full bg-[#05DED5] px-6 py-2.5 text-xs font-bold text-[#020B1E] shadow-sm transition-all hover:scale-105 hover:bg-white"
                  @click="saveCookiePreferences"
                >
                  Save My Preferences
                </button>
              </div>
            </div>
          </section>

          <!-- Section 4 -->
          <section id="cookie-categories" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              4. Cookie Categories Explained
            </h2>
            <p class="leading-relaxed">
              We group the cookies and storage tokens used across Deagensie into four distinct
              operational classifications:
            </p>
            <div class="space-y-4 pt-2">
              <div class="rounded-2xl border border-gray-100 bg-gray-50/60 p-5">
                <h4 class="font-bold text-gray-900">A. Strictly Necessary Cookies</h4>
                <p class="mt-1 text-sm text-gray-600">
                  Essential for the operation of the website and cannot be deactivated. They are
                  usually set in response to actions made by you, such as requesting services,
                  setting your privacy preferences, or logging in. You can configure your browser to
                  block them, but portions of the site will not function.
                </p>
              </div>
              <div class="rounded-2xl border border-gray-100 bg-gray-50/60 p-5">
                <h4 class="font-bold text-gray-900">B. Functional & Persistence Technologies</h4>
                <p class="mt-1 text-sm text-gray-600">
                  These allow the platform to provide enhanced functionality, personalization, and
                  multi-step registration memory. If you do not allow these cookies, some
                  registration wizards and interactive portfolio previews may reset upon navigation.
                </p>
              </div>
              <div class="rounded-2xl border border-gray-100 bg-gray-50/60 p-5">
                <h4 class="font-bold text-gray-900">C. Performance & Analytical Cookies</h4>
                <p class="mt-1 text-sm text-gray-600">
                  Help us quantify visits and traffic sources so we can evaluate and elevate site
                  performance. They help us understand which pages are the most and least popular
                  and see how visitors navigate the site. All information collected is aggregated
                  and anonymized.
                </p>
              </div>
              <div class="rounded-2xl border border-gray-100 bg-gray-50/60 p-5">
                <h4 class="font-bold text-gray-900">D. Marketing & Referral Cookies</h4>
                <p class="mt-1 text-sm text-gray-600">
                  Utilized to track campaign effectiveness and early-access referral links. They do
                  not store direct personal identifiers but rely on uniquely identifying your
                  browser and device.
                </p>
              </div>
            </div>
          </section>

          <!-- Section 5 -->
          <section id="cookie-inventory" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              5. Detailed Inventory of Cookies
            </h2>
            <p class="leading-relaxed">
              The following inventory details the cookies and storage keys commonly utilized on the
              Deagensie platform:
            </p>

            <div class="overflow-x-auto rounded-2xl border border-gray-100">
              <table class="w-full text-left text-xs sm:text-sm">
                <thead class="bg-gray-50 text-gray-900">
                  <tr>
                    <th class="p-3.5 font-bold">Cookie / Key Name</th>
                    <th class="p-3.5 font-bold">Category</th>
                    <th class="p-3.5 font-bold">Purpose</th>
                    <th class="p-3.5 font-bold">Duration</th>
                  </tr>
                </thead>
                <tbody class="divide-y divide-gray-100 text-gray-600">
                  <tr>
                    <td class="p-3.5 font-mono font-semibold text-gray-900">deag_session</td>
                    <td class="p-3.5">
                      <span
                        class="rounded-md bg-gray-100 px-2 py-0.5 text-xs font-semibold text-gray-700"
                        >Necessary</span
                      >
                    </td>
                    <td class="p-3.5">
                      Maintains authenticated user session and security context.
                    </td>
                    <td class="p-3.5">Session</td>
                  </tr>
                  <tr>
                    <td class="p-3.5 font-mono font-semibold text-gray-900">
                      deag_cookie_preferences
                    </td>
                    <td class="p-3.5">
                      <span
                        class="rounded-md bg-gray-100 px-2 py-0.5 text-xs font-semibold text-gray-700"
                        >Necessary</span
                      >
                    </td>
                    <td class="p-3.5">Stores user cookie consent settings locally.</td>
                    <td class="p-3.5">1 Year</td>
                  </tr>
                  <tr>
                    <td class="p-3.5 font-mono font-semibold text-gray-900">deag_biz_reg_draft</td>
                    <td class="p-3.5">
                      <span
                        class="rounded-md bg-blue-50 px-2 py-0.5 text-xs font-semibold text-[#04308F]"
                        >Functional</span
                      >
                    </td>
                    <td class="p-3.5">Preserves incomplete business registration form inputs.</td>
                    <td class="p-3.5">30 Days</td>
                  </tr>
                  <tr>
                    <td class="p-3.5 font-mono font-semibold text-gray-900">
                      deag_creative_reg_draft
                    </td>
                    <td class="p-3.5">
                      <span
                        class="rounded-md bg-blue-50 px-2 py-0.5 text-xs font-semibold text-[#04308F]"
                        >Functional</span
                      >
                    </td>
                    <td class="p-3.5">Preserves talent application wizard inputs.</td>
                    <td class="p-3.5">30 Days</td>
                  </tr>
                  <tr>
                    <td class="p-3.5 font-mono font-semibold text-gray-900">_deag_telemetry_id</td>
                    <td class="p-3.5">
                      <span
                        class="rounded-md bg-teal-50 px-2 py-0.5 text-xs font-semibold text-teal-800"
                        >Analytics</span
                      >
                    </td>
                    <td class="p-3.5">
                      Anonymous identifier for pageview telemetry and performance monitoring.
                    </td>
                    <td class="p-3.5">1 Year</td>
                  </tr>
                  <tr>
                    <td class="p-3.5 font-mono font-semibold text-gray-900">_deag_waitlist_ref</td>
                    <td class="p-3.5">
                      <span
                        class="rounded-md bg-amber-50 px-2 py-0.5 text-xs font-semibold text-amber-800"
                        >Marketing</span
                      >
                    </td>
                    <td class="p-3.5">Tracks early-access waitlist referral invitation codes.</td>
                    <td class="p-3.5">60 Days</td>
                  </tr>
                  <tr>
                    <td class="p-3.5 font-mono font-semibold text-gray-900">__cf_bm / _cfuvid</td>
                    <td class="p-3.5">
                      <span
                        class="rounded-md bg-gray-100 px-2 py-0.5 text-xs font-semibold text-gray-700"
                        >Necessary</span
                      >
                    </td>
                    <td class="p-3.5">Cloudflare bot management and DDoS protection.</td>
                    <td class="p-3.5">30 Minutes</td>
                  </tr>
                </tbody>
              </table>
            </div>
          </section>

          <!-- Section 6 -->
          <section id="third-party-services" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              6. Third-Party Services
            </h2>
            <p class="leading-relaxed">
              In certain circumstances, third-party infrastructure services may set cookies on our
              behalf to ensure high uptime, secure payment processing, and interactive components:
            </p>
            <ul class="list-disc space-y-2 pl-6">
              <li>
                <strong>Cloudflare / Edge Networks:</strong> Used for global content delivery, SSL
                certificate termination, and edge DDoS defense.
              </li>
              <li>
                <strong>Payment Processors (Stripe):</strong> During subscription checkouts
                (<code>/subscription/[code]/[plan]/checkout</code>), Stripe sets security cookies to
                authenticate transactions and detect fraudulent cards.
              </li>
              <li>
                <strong>Iconography & Typography:</strong> Google Fonts and Iconify CDN resources
                are served securely to render web typography and icons.
              </li>
            </ul>
          </section>

          <!-- Section 7 -->
          <section id="browser-controls" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              7. How to Manage Cookies via Browser Controls
            </h2>
            <p class="leading-relaxed">
              Most web browsers automatically accept cookies by default, but you can adjust your
              browser settings to refuse cookies or notify you whenever a cookie is set:
            </p>
            <ul class="list-disc space-y-2 pl-6">
              <li>
                <strong>Google Chrome:</strong> Settings &rarr; Privacy and security &rarr;
                Third-party cookies.
              </li>
              <li>
                <strong>Mozilla Firefox:</strong> Settings &rarr; Privacy &amp; Security &rarr;
                Enhanced Tracking Protection.
              </li>
              <li>
                <strong>Apple Safari:</strong> Preferences &rarr; Privacy &rarr; Prevent cross-site
                tracking.
              </li>
              <li>
                <strong>Microsoft Edge:</strong> Settings &rarr; Cookies and site permissions &rarr;
                Manage and delete cookies.
              </li>
            </ul>
            <p class="text-sm leading-relaxed text-gray-500">
              Please note that disabling strictly necessary cookies in your browser may impair the
              core functionality of the Deagensie web platform, such as submitting project briefs or
              receiving instant registration confirmations.
            </p>
          </section>

          <!-- Section 8 -->
          <section id="dnt-gpc-signals" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              8. Do Not Track (DNT) & Global Privacy Control (GPC)
            </h2>
            <p class="leading-relaxed">
              Deagensie respects user privacy preferences. Our systems are configured to detect and
              honor the <strong>Global Privacy Control (GPC)</strong> browser signal. When a GPC
              signal is detected from your browser, our application automatically treats that signal
              as an opt-out request for non-essential analytical and marketing tracking
              technologies.
            </p>
          </section>

          <!-- Section 9 -->
          <section id="policy-updates" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              9. Policy Updates & Inquiries
            </h2>
            <p class="leading-relaxed">
              We may revise this Cookie Policy occasionally to reflect technological enhancements,
              operational changes, or statutory regulations. Any updates will be published on this
              page with a revised &ldquo;Effective Date&rdquo;.
            </p>
            <div class="rounded-2xl border border-gray-100 bg-gray-50 p-6 text-sm text-gray-700">
              <p class="font-bold text-gray-900">Deagensie Inc. &mdash; Data Protection Team</p>
              <p class="mt-1">
                Cookie & Privacy Inquiries:
                <a href="mailto:privacy@deagensie.com" class="text-[#04308F] underline"
                  >privacy@deagensie.com</a
                >
              </p>
              <p class="mt-1">
                Technical Support:
                <a href="mailto:support@deagensie.com" class="text-[#04308F] underline"
                  >support@deagensie.com</a
                >
              </p>
              <p class="mt-1">
                Contact Portal:
                <NuxtLink to="/contact" class="text-[#04308F] underline"
                  >deagensie.com/contact</NuxtLink
                >
              </p>
            </div>
          </section>
        </article>
      </div>
    </div>

    <!-- Bottom CTA -->
    <PagesLegalLegalCta />
  </div>
</template>
