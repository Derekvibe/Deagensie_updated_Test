<script setup lang="ts">
import { Icon } from '@iconify/vue';

const engagementModels = [
  {
    icon: 'lucide:layers',
    title: 'Project Deployments',
    scope: 'Defined Sprints',
    description:
      'Fixed-scope deliverables with milestone commitments. Ideal for rapid brand launches, digital platform builds, and campaign rollouts.',
    tags: ['Brand Identity', 'Product MVP', 'Design Systems', 'Launch Campaigns'],
  },
  {
    icon: 'lucide:calendar-clock',
    title: 'Contract Roles',
    scope: 'Flexible Terms',
    description:
      'Augment your internal team with specialized talent on monthly arrangements. Scale up or down as project demands evolve.',
    tags: ['UI/UX Specialists', 'Lead Developers', 'Growth Strategists', 'Creative Directors'],
  },
  {
    icon: 'lucide:globe',
    title: 'Remote Positions',
    scope: 'Embedded Talent',
    description:
      'Hire vetted African talent for full-time remote roles. Embedded directly into your timezone, tools, and daily operating rhythm.',
    tags: ['Timezone Aligned', 'Full Integration', 'Direct Reporting', 'Vetted Culture Fit'],
  },
  {
    icon: 'lucide:shield-check',
    title: 'Dedicated Creative Support',
    scope: 'Managed Squads',
    description:
      "Deploy full multi-disciplinary creative squads to handle your venture's continuous design, marketing, and engineering needs.",
    tags: ['Dedicated Squad Lead', 'Multi-Disciplinary', 'Continuous Velocity', 'Managed Quality'],
  },
];

const candidateSimulations = [
  {
    role: 'Lead Product Designer',
    matchScore: 99,
    experience: '7+ Years Experience',
    bio: 'Ex-fintech design lead specializing in complex SaaS platforms, design tokens, and user research.',
    skills: ['Figma', 'Design Systems', 'Prototyping', 'User Testing', 'Mobile Apps'],
    status: 'Available Immediately',
  },
  {
    role: 'Senior Growth & Performance Marketer',
    matchScore: 97,
    experience: '6+ Years Experience',
    bio: 'Data-driven growth architect with verified track record scaling venture pipeline across B2B and consumer tech.',
    skills: [
      'Paid Acquisition',
      'Funnel Optimization',
      'Meta & Google Ads',
      'Mixpanel',
      'CRM Automation',
    ],
    status: 'Available in 1 Week',
  },
  {
    role: 'Full-Stack Platform Engineer',
    matchScore: 98,
    experience: '8+ Years Experience',
    bio: 'Senior engineer focused on modern TypeScript stacks, cloud microservices, and high-conversion web platforms.',
    skills: ['Nuxt / Vue', 'Node.js', 'PostgreSQL', 'Tailwind CSS', 'AWS / Cloudflare'],
    status: 'Available Immediately',
  },
];

const selectedCandidateIndex = ref(0);
</script>

<template>
  <section class="border-b border-gray-100 bg-[#FAFAFA] py-20 text-gray-900 lg:py-28">
    <div class="mx-auto w-5/6 max-w-7xl space-y-16 lg:space-y-20">
      <!-- Section 1: Engagement Models -->
      <div class="space-y-12">
        <div v-reveal="'fade-up'" class="mx-auto max-w-3xl space-y-3 text-center">
          <span
            class="inline-block rounded-full bg-[#04308F]/10 px-4 py-1.5 text-xs font-semibold tracking-widest text-[#04308F] uppercase"
          >
            Flexible Deployment
          </span>
          <h2
            class="font-serif text-3xl leading-tight font-normal tracking-tight text-gray-900 sm:text-4xl lg:text-5xl"
          >
            Engagement Models Tailored to Scale
          </h2>
          <p class="mx-auto max-w-2xl text-base leading-relaxed text-gray-600 sm:text-lg">
            Engage talent for projects, contract roles, remote positions, long-term engagements or
            dedicated creative support.
          </p>
        </div>

        <div class="grid grid-cols-1 gap-6 sm:grid-cols-2 lg:grid-cols-4 lg:gap-6">
          <div
            v-for="(mod, idx) in engagementModels"
            :key="mod.title"
            v-reveal="{ animation: 'fade-up', delay: idx * 80 }"
            class="group flex flex-col justify-between rounded-2xl border border-gray-200/90 bg-white p-7 transition-all duration-300 hover:border-[#04308F]/30 hover:shadow-lg sm:p-8"
          >
            <div class="space-y-4">
              <div class="flex items-center justify-between border-b border-gray-100 pb-4">
                <div
                  class="flex size-10 items-center justify-center rounded-xl bg-[#04308F]/10 text-xl text-[#04308F] transition-colors group-hover:bg-[#04308F] group-hover:text-white"
                >
                  <Icon :icon="mod.icon" />
                </div>
                <span class="font-mono text-xs font-semibold text-gray-500 uppercase">
                  {{ mod.scope }}
                </span>
              </div>

              <h3 class="font-serif text-xl font-bold tracking-tight text-gray-900">
                {{ mod.title }}
              </h3>

              <p class="text-xs leading-relaxed text-gray-600 sm:text-sm">
                {{ mod.description }}
              </p>
            </div>

            <!-- Tags -->
            <div class="pt-6">
              <div class="flex flex-wrap gap-1.5">
                <span
                  v-for="tg in mod.tags"
                  :key="tg"
                  class="rounded-md bg-gray-100 px-2 py-1 text-[11px] font-medium text-gray-700"
                >
                  {{ tg }}
                </span>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Section 2: AI Matching Engine Interactive Showcase -->
      <div
        v-reveal="'fade-up'"
        class="rounded-3xl border border-gray-200/90 bg-white p-8 shadow-sm sm:p-10 lg:p-12"
      >
        <div class="grid grid-cols-1 gap-8 lg:grid-cols-12 lg:items-center">
          <!-- Left Column: Context -->
          <div class="space-y-5 lg:col-span-5">
            <span
              class="inline-block rounded-full bg-[#05DED5]/20 px-3.5 py-1 text-xs font-semibold tracking-wider text-teal-800 uppercase"
            >
              Predictive Match Engine
            </span>

            <h3
              class="font-serif text-2xl leading-tight font-normal text-gray-900 sm:text-3xl lg:text-4xl"
            >
              Matched Against Verified Talent Profiles
            </h3>

            <p class="text-sm leading-relaxed text-gray-600 sm:text-base">
              Our matching engine evaluates requirement criteria across verified technical skills,
              industry background, project complexity, and timezone requirements to deliver precise
              talent matches.
            </p>

            <!-- Role Selector Tabs -->
            <div class="space-y-2 pt-2">
              <div class="text-xs font-bold tracking-wider text-gray-400 uppercase">
                Sample Verified Talent Matches:
              </div>
              <div class="flex flex-col gap-2">
                <button
                  v-for="(cand, idx) in candidateSimulations"
                  :key="cand.role"
                  type="button"
                  class="flex items-center justify-between rounded-xl px-4 py-3 text-left text-xs font-semibold transition-all duration-200 sm:text-sm"
                  :class="
                    selectedCandidateIndex === idx
                      ? 'bg-[#04308F] text-white shadow-sm'
                      : 'bg-gray-50 text-gray-700 hover:bg-gray-100'
                  "
                  @click="selectedCandidateIndex = idx"
                >
                  <span>{{ cand.role }}</span>
                  <span
                    class="rounded-full px-2 py-0.5 font-mono text-[11px]"
                    :class="
                      selectedCandidateIndex === idx
                        ? 'bg-[#05DED5] font-bold text-gray-950'
                        : 'bg-gray-200 text-gray-700'
                    "
                  >
                    {{ cand.matchScore }}% Match
                  </span>
                </button>
              </div>
            </div>
          </div>

          <!-- Right Column: Interactive Profile Card -->
          <div class="lg:col-span-7">
            <div
              class="relative rounded-2xl bg-[#0F1E2E] p-7 text-white shadow-xl transition-all duration-300 sm:p-8"
            >
              <!-- Card Top Row -->
              <div
                class="flex flex-wrap items-center justify-between gap-3 border-b border-white/10 pb-5"
              >
                <div>
                  <div class="font-mono text-xs text-gray-400">VERIFIED TALENT PROFILE</div>
                  <h4 class="mt-1 font-serif text-2xl font-bold text-white">
                    {{ candidateSimulations[selectedCandidateIndex].role }}
                  </h4>
                </div>
                <div class="flex items-center gap-2">
                  <span
                    class="inline-flex items-center gap-1.5 rounded-full bg-[#05DED5]/20 px-3 py-1 font-mono text-xs font-bold text-[#05DED5]"
                  >
                    <span class="size-2 animate-pulse rounded-full bg-[#05DED5]" />
                    {{ candidateSimulations[selectedCandidateIndex].matchScore }}% Requirement Match
                  </span>
                </div>
              </div>

              <!-- Body -->
              <div class="space-y-4 py-5">
                <div class="flex items-center gap-4 text-xs text-gray-300">
                  <span class="inline-flex items-center gap-1.5 font-medium text-gray-200">
                    <Icon icon="lucide:award" class="text-base text-[#05DED5]" />
                    {{ candidateSimulations[selectedCandidateIndex].experience }}
                  </span>
                  <span class="inline-flex items-center gap-1.5 font-medium text-emerald-400">
                    <Icon icon="lucide:check-circle-2" class="text-base" />
                    {{ candidateSimulations[selectedCandidateIndex].status }}
                  </span>
                </div>

                <p class="text-xs leading-relaxed text-gray-300 sm:text-sm">
                  {{ candidateSimulations[selectedCandidateIndex].bio }}
                </p>

                <!-- Skills -->
                <div class="space-y-2 pt-2">
                  <div class="text-[11px] font-bold tracking-wider text-gray-400 uppercase">
                    Core Competencies & Stack:
                  </div>
                  <div class="flex flex-wrap gap-2">
                    <span
                      v-for="sk in candidateSimulations[selectedCandidateIndex].skills"
                      :key="sk"
                      class="rounded-md border border-white/10 bg-white/5 px-2.5 py-1 text-xs text-gray-200"
                    >
                      {{ sk }}
                    </span>
                  </div>
                </div>
              </div>

              <!-- Card Bottom -->
              <div
                class="flex flex-wrap items-center justify-between gap-4 border-t border-white/10 pt-5"
              >
                <span class="text-xs text-gray-400">
                  Verified portfolio, background vetted, and culture screened.
                </span>
                <NuxtLink
                  to="/contact"
                  class="inline-flex items-center gap-2 rounded-full bg-[#05DED5] px-5 py-2.5 text-xs font-bold text-gray-950 transition-all duration-200 hover:bg-white"
                >
                  <span>Request Candidate Dossier</span>
                  <Icon icon="lucide:arrow-right" class="text-sm" />
                </NuxtLink>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped lang="css"></style>
