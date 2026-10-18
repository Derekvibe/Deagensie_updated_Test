<script setup lang="ts">
import { Icon } from '@iconify/vue';

interface TaasStep {
  number: string;
  title: string;
  tagline: string;
  description: string;
  paramType: string;
  parameters: string[];
}

const steps: TaasStep[] = [
  {
    number: '/01',
    title: 'Tell Us What You Need',
    tagline: 'Define your role, skills, and timeline.',
    description:
      'Create a job or project with role, skills, experience, industry, project requirements, timeline and engagement type.',
    paramType: 'REQUIREMENTS DEFINED:',
    parameters: [
      'Role & Seniority Scope',
      'Core Skills & Tools',
      'Industry & Domain Focus',
      'Project Deliverables',
      'Timeline & Sprints',
      'Engagement Type',
    ],
  },
  {
    number: '/02',
    title: 'AI-Powered Matching',
    tagline: 'Predictive analysis against talent profiles.',
    description:
      'Our predictive engine analyzes the requirements against talent profiles to identify relevant candidates.',
    paramType: 'MATCHING ENGINE:',
    parameters: [
      'Contextual Requirement Analysis',
      'Verified Talent Profiles',
      'Competency & Portfolio Scoring',
      'Availability Alignment',
      'Performance Track Record',
      'Precision Candidate Shortlist',
    ],
  },
  {
    number: '/03',
    title: 'Review & Connect',
    tagline: 'Inspect portfolios and interview.',
    description:
      'Review matched professionals and connect with the talent that fits your requirements.',
    paramType: 'EVALUATION & FIT:',
    parameters: [
      'Curated Talent Profiles',
      'Verified Case Studies',
      'Direct Introduction Calls',
      'Technical & Cultural Fit',
      'Transparent Rate Structures',
      'Fast-Track Selection',
    ],
  },
  {
    number: '/04',
    title: 'Build Your Team',
    tagline: 'Deploy talent on flexible terms.',
    description:
      'Engage talent for projects, contract roles, remote positions, long-term engagements or dedicated creative support.',
    paramType: 'ENGAGEMENT MODELS:',
    parameters: [
      'Project-Based Deployments',
      'Flexible Contract Roles',
      'Embedded Remote Talent',
      'Long-Term Engagements',
      'Dedicated Creative Support',
      'Managed Quality Assurance',
    ],
  },
];

// Active card index on desktop (null = all cards closed by default, moderate height)
const activeIndex = ref<number | null>(null);

const selectStep = (idx: number) => {
  activeIndex.value = activeIndex.value === idx ? null : idx;
};

// Split parameters into two columns for desktop flex layout
const getCol1 = (items: string[]) => items.slice(0, Math.ceil(items.length / 2));
const getCol2 = (items: string[]) => items.slice(Math.ceil(items.length / 2));

// Mobile expanded card tracking (null by default)
const mobileActiveIndex = ref<number | null>(null);

const toggleMobileExpand = (idx: number) => {
  mobileActiveIndex.value = mobileActiveIndex.value === idx ? null : idx;
};
</script>

<template>
  <section
    id="how-it-works"
    class="border-b border-gray-100 bg-white pt-6 pb-20 text-gray-900 sm:pt-8 sm:pb-24 lg:pt-8 lg:pb-28"
  >
    <div class="mx-auto w-5/6 max-w-7xl space-y-12 lg:space-y-14">
      <!-- Section Header -->
      <div v-reveal="'fade-up'" class="mx-auto max-w-3xl space-y-3 text-center">
        <span
          class="inline-block rounded-full bg-[#04308F]/10 px-4 py-1.5 text-xs font-semibold tracking-widest text-[#04308F] uppercase"
        >
          Streamlined Process
        </span>
        <h2
          class="font-serif text-3xl leading-tight font-normal tracking-tight text-gray-900 sm:text-4xl lg:text-5xl"
        >
          How It Works
        </h2>
        <p class="mx-auto max-w-xl text-base leading-relaxed text-gray-600 sm:text-lg">
          From requirement definition to team integration in four structured phases.
        </p>
      </div>

      <!-- ============================================================ -->
      <!-- DESKTOP SCREEN: Moderate Height Horizontal Row & Closed      -->
      <!-- ============================================================ -->
      <div class="hidden lg:flex lg:flex-row lg:items-stretch lg:gap-5">
        <div
          v-for="(st, idx) in steps"
          :key="st.title"
          v-reveal="{ animation: 'fade-up', delay: idx * 80 }"
          class="group relative flex min-h-[220px] flex-col justify-between rounded-2xl transition-all duration-500 ease-out sm:min-h-[230px]"
          :class="[
            activeIndex === idx
              ? 'cursor-pointer bg-[#0F1E2E] p-7 text-white shadow-xl sm:p-8 lg:flex-[2.4]'
              : 'cursor-pointer border border-gray-200/90 bg-white p-6 text-gray-900 shadow-2xs hover:border-gray-300 hover:shadow-md sm:p-7 lg:flex-1',
          ]"
          @click="selectStep(idx)"
        >
          <!-- Top Card Header & Content Area -->
          <div>
            <!-- Step Index: /01, /02, /03, /04 -->
            <div
              class="font-mono text-xs font-normal tracking-wider sm:text-sm"
              :class="activeIndex === idx ? 'text-gray-400' : 'text-gray-400'"
            >
              {{ st.number }}
            </div>

            <!-- Inactive / Closed State Layout: Moderate height, clean and compact -->
            <div v-if="activeIndex !== idx" class="space-y-2.5 pt-4">
              <h3
                class="font-serif text-xl leading-snug font-normal text-gray-900 transition-colors group-hover:text-[#04308F] sm:text-2xl"
              >
                {{ st.title }}
              </h3>
              <p class="text-xs leading-relaxed text-gray-500 sm:text-sm">
                {{ st.tagline }}
              </p>
            </div>

            <!-- Active / Opened State Layout: 2-Column checklist -->
            <div v-else class="space-y-3 pt-3">
              <h3 class="font-serif text-2xl leading-snug font-bold text-white sm:text-3xl">
                {{ st.title }}
              </h3>
              <p class="text-xs font-medium text-[#05DED5] sm:text-sm">
                {{ st.tagline }}
              </p>
              <p class="pt-0.5 pb-2 text-xs leading-relaxed text-gray-300 sm:text-sm">
                {{ st.description }}
              </p>

              <!-- Parameters: 2 Columns -->
              <div class="space-y-2.5 border-t border-white/10 pt-3.5">
                <div class="text-[11px] font-bold tracking-wider text-gray-400 uppercase">
                  {{ st.paramType }}
                </div>
                <div class="grid grid-cols-2 gap-x-6 gap-y-2">
                  <!-- Left Column -->
                  <ul class="space-y-2 text-xs text-gray-100 sm:text-sm">
                    <li
                      v-for="item in getCol1(st.parameters)"
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
                      v-for="item in getCol2(st.parameters)"
                      :key="item"
                      class="flex items-start gap-2 leading-tight"
                    >
                      <Icon icon="lucide:check" class="mt-0.5 size-4 shrink-0 text-emerald-400" />
                      <span>{{ item }}</span>
                    </li>
                  </ul>
                </div>
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
          v-for="(st, idx) in steps"
          :key="st.title"
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
              {{ st.number }}
            </div>

            <!-- Title & Tagline -->
            <div>
              <h3
                class="font-serif text-xl leading-snug font-bold sm:text-2xl"
                :class="mobileActiveIndex === idx ? 'text-white' : 'text-gray-900'"
              >
                {{ st.title }}
              </h3>
              <p
                class="mt-1 text-xs font-medium sm:text-sm"
                :class="mobileActiveIndex === idx ? 'text-[#05DED5]' : 'text-[#04308F]'"
              >
                {{ st.tagline }}
              </p>
            </div>

            <!-- Opened State: Description & Full Parameters -->
            <div v-if="mobileActiveIndex === idx" class="space-y-3 pt-1">
              <!-- Narrative Description -->
              <p class="text-xs leading-relaxed text-gray-300 sm:text-sm">
                {{ st.description }}
              </p>

              <!-- Parameters Section -->
              <div class="space-y-2 border-t border-white/10 pt-3">
                <div class="text-[11px] font-bold tracking-wider text-gray-400 uppercase">
                  {{ st.paramType }}
                </div>
                <div
                  class="grid grid-cols-1 gap-2 pt-1 text-xs text-gray-100 sm:grid-cols-2 sm:text-sm"
                >
                  <ul class="space-y-2">
                    <li
                      v-for="item in getCol1(st.parameters)"
                      :key="item"
                      class="flex items-start gap-2 leading-tight"
                    >
                      <Icon icon="lucide:check" class="mt-0.5 size-4 shrink-0 text-emerald-400" />
                      <span>{{ item }}</span>
                    </li>
                  </ul>
                  <ul class="space-y-2">
                    <li
                      v-for="item in getCol2(st.parameters)"
                      :key="item"
                      class="flex items-start gap-2 leading-tight"
                    >
                      <Icon icon="lucide:check" class="mt-0.5 size-4 shrink-0 text-emerald-400" />
                      <span>{{ item }}</span>
                    </li>
                  </ul>
                </div>
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
