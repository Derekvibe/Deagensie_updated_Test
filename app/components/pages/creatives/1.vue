<template>
  <section class="border-b border-gray-100 bg-white py-20 text-gray-900 sm:py-24 lg:py-28">
    <div class="mx-auto w-5/6 max-w-7xl">
      <!-- Section Header -->
      <div v-reveal="'fade-up'" class="mx-auto max-w-4xl text-center">
        <span
          class="inline-block rounded-full bg-[#04308F]/10 px-4 py-1.5 text-xs font-semibold tracking-widest text-[#04308F] uppercase"
        >
          How It Works
        </span>

        <h2
          class="mt-4 font-serif text-3xl leading-[1.15] font-normal tracking-tight text-gray-900 sm:text-4xl lg:text-5xl"
        >
          Your Talent Should Travel Further <br class="hidden sm:inline" />
          <span class="text-[#04308F]">Than Your Location.</span>
        </h2>

        <p
          class="mx-auto mt-6 max-w-3xl text-sm leading-relaxed font-normal text-gray-600 sm:text-base lg:text-lg"
        >
          Instead of relying solely on conventional recruitment or endless applications, Deagensie
          TaaS uses a predictive AI matching engine to understand talent, opportunities and
          requirements, and identify where the strongest potential matches exist. Great creative
          talent should not be limited by geography. TaaS helps designers, developers, strategists,
          marketers, writers, creators and other creative professionals discover relevant
          opportunities beyond their immediate markets.
        </p>
      </div>

      <!-- Bento Grid: Structure of Attached Reference with Standard Deagensie Colors & User Content -->
      <div class="mt-14 space-y-6 sm:mt-16 sm:space-y-8 lg:mt-20">
        <!-- 01: Top Wide Card (Build Your Profile) -->
        <div
          v-reveal="'fade-up'"
          class="relative overflow-hidden rounded-3xl border border-gray-200/80 bg-[#FAFAFA] p-6 transition-all duration-300 hover:border-gray-300 hover:shadow-md sm:p-8 lg:p-10"
        >
          <div class="grid grid-cols-1 items-center gap-8 lg:grid-cols-12 lg:gap-12">
            <!-- Left Column: Content -->
            <div class="space-y-4 lg:col-span-5">
              <span class="font-mono text-xs font-semibold tracking-wider text-[#04308F] uppercase">
                / 01
              </span>
              <h3 class="font-serif text-2xl font-normal tracking-tight text-gray-900 sm:text-3xl">
                Build Your Profile
              </h3>
              <p class="text-sm leading-relaxed font-normal text-gray-600 sm:text-base">
                Showcase your skills, experience, portfolio, specializations, industry experience,
                career interests, availability.
              </p>
            </div>

            <!-- Right Column: Profile Showcase Card -->
            <div class="lg:col-span-7">
              <div class="rounded-2xl border border-gray-200/90 bg-white p-5 shadow-xs sm:p-6">
                <div class="flex items-center justify-between border-b border-gray-100 pb-4">
                  <div class="flex items-center gap-3">
                    <div
                      class="flex size-10 items-center justify-center rounded-xl bg-[#0F1E2E] text-white"
                    >
                      <svg class="size-5 fill-none stroke-current stroke-2" viewBox="0 0 24 24">
                        <path d="M20 21v-2a4 4 0 0 0-4-4H8a4 4 0 0 0-4 4v2" />
                        <circle cx="12" cy="7" r="4" />
                      </svg>
                    </div>
                    <div>
                      <h4 class="text-sm font-semibold text-gray-900 sm:text-base">
                        Creative Profile
                      </h4>
                      <p class="text-xs text-gray-500">Talent Ecosystem Showcase</p>
                    </div>
                  </div>
                  <span
                    class="rounded-full bg-[#04308F]/10 px-3 py-1 text-xs font-semibold text-[#04308F]"
                  >
                    Verified
                  </span>
                </div>

                <!-- Profile Parameters directly from user copy -->
                <div class="mt-4 grid grid-cols-1 gap-2.5 sm:grid-cols-2">
                  <div class="rounded-xl border border-gray-100 bg-[#FAFAFA] p-3">
                    <p class="text-[11px] font-semibold tracking-wider text-gray-400 uppercase">
                      Showcase Focus
                    </p>
                    <p class="mt-1 text-xs font-medium text-gray-800">Skills & Specializations</p>
                  </div>
                  <div class="rounded-xl border border-gray-100 bg-[#FAFAFA] p-3">
                    <p class="text-[11px] font-semibold tracking-wider text-gray-400 uppercase">
                      Experience
                    </p>
                    <p class="mt-1 text-xs font-medium text-gray-800">Portfolio & Case Studies</p>
                  </div>
                  <div class="rounded-xl border border-gray-100 bg-[#FAFAFA] p-3">
                    <p class="text-[11px] font-semibold tracking-wider text-gray-400 uppercase">
                      Domain
                    </p>
                    <p class="mt-1 text-xs font-medium text-gray-800">Industry Experience</p>
                  </div>
                  <div class="rounded-xl border border-gray-100 bg-[#FAFAFA] p-3">
                    <p class="text-[11px] font-semibold tracking-wider text-gray-400 uppercase">
                      Status
                    </p>
                    <p class="mt-1 text-xs font-medium text-gray-800">
                      Career Interests & Availability
                    </p>
                  </div>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Bottom 3-Card Row: Get Matched | Work Globally | Grow Your Career -->
        <div class="grid grid-cols-1 gap-6 sm:gap-8 md:grid-cols-3">
          <!-- 02: Get Matched -->
          <div
            v-reveal="'fade-up'"
            class="flex flex-col justify-between rounded-3xl border border-gray-200/80 bg-[#FAFAFA] p-6 transition-all duration-300 hover:border-gray-300 hover:shadow-md sm:p-8"
          >
            <div>
              <span class="font-mono text-xs font-semibold tracking-wider text-[#04308F] uppercase">
                / 02
              </span>
              <h3
                class="mt-3 font-serif text-xl font-normal tracking-tight text-gray-900 sm:text-2xl"
              >
                Get Matched
              </h3>
              <p class="mt-3 text-sm leading-relaxed font-normal text-gray-600">
                Our predictive AI engine evaluates your profile against available opportunities to
                identify relevant job and project matches.
              </p>
            </div>

            <!-- UI Card: Predictive AI Engine -->
            <div class="mt-6 rounded-2xl border border-gray-200/90 bg-white p-4 shadow-xs">
              <div class="flex items-center justify-between">
                <div class="flex items-center gap-2.5">
                  <div
                    class="flex size-8 items-center justify-center rounded-lg bg-[#04308F] text-white"
                  >
                    <svg class="size-4 fill-current" viewBox="0 0 24 24">
                      <path d="M12 0L14.7 9.3L24 12L14.7 14.7L12 24L9.3 14.7L0 12L9.3 9.3L12 0Z" />
                    </svg>
                  </div>
                  <div>
                    <p class="text-xs font-semibold text-gray-900">Predictive AI Engine</p>
                    <p class="text-[11px] text-gray-500">Evaluates Profile vs Opportunities</p>
                  </div>
                </div>
                <span class="text-xs font-bold text-[#04308F]">98%</span>
              </div>
              <!-- Progress Bar -->
              <div class="mt-3 h-1.5 w-full overflow-hidden rounded-full bg-gray-100">
                <div class="h-full w-[98%] rounded-full bg-[#04308F]"></div>
              </div>
              <p class="mt-2.5 flex items-center gap-1.5 text-[11px] font-medium text-gray-500">
                <span class="size-1.5 rounded-full bg-[#04308F]"></span> Relevant Matches Identified
              </p>
            </div>
          </div>

          <!-- 03: Work Globally -->
          <div
            v-reveal="'fade-up'"
            class="flex flex-col justify-between rounded-3xl border border-gray-200/80 bg-[#FAFAFA] p-6 transition-all duration-300 hover:border-gray-300 hover:shadow-md sm:p-8"
          >
            <div>
              <span class="font-mono text-xs font-semibold tracking-wider text-[#04308F] uppercase">
                / 03
              </span>
              <h3
                class="mt-3 font-serif text-xl font-normal tracking-tight text-gray-900 sm:text-2xl"
              >
                Work Globally
              </h3>
              <p class="mt-3 text-sm leading-relaxed font-normal text-gray-600">
                Access opportunities from businesses, startups and organizations seeking creative
                talent.
              </p>
            </div>

            <!-- UI Card: Global Access -->
            <div
              class="mt-6 space-y-2 rounded-2xl border border-gray-200/90 bg-white p-4 shadow-xs"
            >
              <div class="text-[11px] font-semibold tracking-wider text-gray-400 uppercase">
                Opportunities From
              </div>
              <div class="space-y-1.5">
                <div
                  class="flex items-center justify-between rounded-lg bg-[#FAFAFA] px-3 py-2 text-xs"
                >
                  <span class="font-medium text-gray-800">Businesses</span>
                  <span class="text-[11px] font-semibold text-[#04308F]">Global</span>
                </div>
                <div
                  class="flex items-center justify-between rounded-lg bg-[#FAFAFA] px-3 py-2 text-xs"
                >
                  <span class="font-medium text-gray-800">Startups</span>
                  <span class="text-[11px] font-semibold text-[#04308F]">Remote</span>
                </div>
                <div
                  class="flex items-center justify-between rounded-lg bg-[#FAFAFA] px-3 py-2 text-xs"
                >
                  <span class="font-medium text-gray-800">Organizations</span>
                  <span class="text-[11px] font-semibold text-[#04308F]">Projects</span>
                </div>
              </div>
            </div>
          </div>

          <!-- 04: Grow Your Career -->
          <div
            v-reveal="'fade-up'"
            class="flex flex-col justify-between rounded-3xl border border-gray-200/80 bg-[#FAFAFA] p-6 transition-all duration-300 hover:border-gray-300 hover:shadow-md sm:p-8"
          >
            <div>
              <span class="font-mono text-xs font-semibold tracking-wider text-[#04308F] uppercase">
                / 04
              </span>
              <h3
                class="mt-3 font-serif text-xl font-normal tracking-tight text-gray-900 sm:text-2xl"
              >
                Grow Your Career
              </h3>
              <p class="mt-3 text-sm leading-relaxed font-normal text-gray-600">
                Build experience, strengthen your portfolio and develop a career that can grow
                beyond borders.
              </p>
            </div>

            <!-- UI Card: Career Growth -->
            <div class="mt-6 rounded-2xl border border-gray-200/90 bg-white p-4 shadow-xs">
              <div
                class="border-b border-gray-100 pb-2 text-[11px] font-semibold tracking-wider text-gray-400 uppercase"
              >
                Career Progression
              </div>
              <ul class="mt-2.5 space-y-2 text-xs text-gray-700">
                <li class="flex items-center gap-2">
                  <span class="font-semibold text-[#04308F]">✓</span> Build Experience
                </li>
                <li class="flex items-center gap-2">
                  <span class="font-semibold text-[#04308F]">✓</span> Strengthen Portfolio
                </li>
                <li class="flex items-center gap-2">
                  <span class="font-semibold text-[#04308F]">✓</span> Grow Beyond Borders
                </li>
              </ul>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts"></script>

<style scoped lang="css"></style>
