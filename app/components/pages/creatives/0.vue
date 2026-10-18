<template>
  <section
    class="relative overflow-hidden border-b border-gray-100 bg-white pt-28 pb-16 text-gray-900 sm:pt-32 sm:pb-20 lg:pt-36 lg:pb-24"
  >
    <div class="mx-auto w-5/6 max-w-7xl">
      <!-- Hero Header Content -->
      <div v-reveal="'fade-up'" class="mx-auto max-w-4xl text-center">
        <h2
          class="font-serif text-3xl leading-[1.15] font-normal tracking-tight text-gray-900 sm:text-5xl lg:text-6xl"
        >
          We connect creative talent to <br />
          <span class="mt-2 inline-block text-[#04308F]">opportunity. Global Jobs. </span>
        </h2>

        <p
          class="mx-auto mt-5 max-w-2xl text-base leading-relaxed font-normal text-gray-600 sm:text-lg"
        >
          AI-powered talent ecosystem connecting exceptional creative professionals with businesses
          and global job opportunities.
        </p>

        <!-- CTAs -->
        <div class="mt-7 flex flex-wrap items-center justify-center gap-4 sm:gap-5">
          <NuxtLink
            to="https://app-deagensie-waitlist.vercel.app/"
            target="_blank"
            rel="noopener noreferrer"
            class="inline-flex items-center justify-center rounded-full bg-[#0F1E2E] px-8 py-3.5 text-sm font-medium text-white shadow-md shadow-gray-900/10 transition-all duration-300 hover:bg-[#026662] hover:shadow-lg sm:text-base"
          >
            Create Profile
          </NuxtLink>
          <NuxtLink
            to="/business/taas"
            class="inline-flex items-center justify-center rounded-full border border-gray-300 bg-white/90 px-8 py-3.5 text-sm font-medium text-gray-800 shadow-sm transition-all duration-300 hover:border-[#04308F] hover:text-[#04308F] sm:text-base"
          >
            Find Opportunity
          </NuxtLink>
        </div>
      </div>

      <!-- Interactive Graphic: Dotted 3D Globe + Talent Matching Cards -->
      <div class="relative mt-10 sm:mt-14 lg:mt-16">
        <!-- 3D Dotted Globe Wireframe Background -->
        <div
          class="pointer-events-none absolute inset-x-0 -top-6 flex justify-center overflow-hidden sm:-top-10"
        >
          <svg
            class="h-[440px] w-[860px] text-slate-300 opacity-65 transition-opacity sm:h-[540px] sm:w-[1150px] sm:opacity-85 lg:h-[600px] lg:w-[1350px]"
            viewBox="0 0 1200 620"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
          >
            <defs>
              <radialGradient id="globe-glow" cx="50%" cy="75%" r="65%">
                <stop offset="0%" stop-color="#026662" stop-opacity="0.07" />
                <stop offset="50%" stop-color="#04308F" stop-opacity="0.03" />
                <stop offset="100%" stop-color="#FFFFFF" stop-opacity="0" />
              </radialGradient>
            </defs>

            <!-- Soft background atmospheric glow -->
            <ellipse cx="600" cy="440" rx="480" ry="260" fill="url(#globe-glow)" />

            <!-- Spherical Contour Arcs (Latitude) -->
            <path
              d="M 160 520 Q 600 240 1040 520"
              stroke="#CBD5E1"
              stroke-width="1"
              stroke-dasharray="2 8"
              fill="none"
              opacity="0.45"
            />
            <path
              d="M 220 460 Q 600 200 980 460"
              stroke="#CBD5E1"
              stroke-width="1"
              stroke-dasharray="2 8"
              fill="none"
              opacity="0.55"
            />
            <path
              d="M 300 400 Q 600 160 900 400"
              stroke="#CBD5E1"
              stroke-width="1"
              stroke-dasharray="2 8"
              fill="none"
              opacity="0.65"
            />
            <path
              d="M 400 340 Q 600 130 800 340"
              stroke="#CBD5E1"
              stroke-width="1"
              stroke-dasharray="2 8"
              fill="none"
              opacity="0.7"
            />

            <!-- Longitudinal Meridians -->
            <path
              d="M 600 110 C 600 250 600 450 600 580"
              stroke="#CBD5E1"
              stroke-width="1"
              stroke-dasharray="2 8"
              fill="none"
              opacity="0.6"
            />
            <path
              d="M 600 110 C 500 240 420 440 380 580"
              stroke="#CBD5E1"
              stroke-width="1"
              stroke-dasharray="2 8"
              fill="none"
              opacity="0.5"
            />
            <path
              d="M 600 110 C 700 240 780 440 820 580"
              stroke="#CBD5E1"
              stroke-width="1"
              stroke-dasharray="2 8"
              fill="none"
              opacity="0.5"
            />
            <path
              d="M 600 110 C 400 230 260 420 200 560"
              stroke="#CBD5E1"
              stroke-width="1"
              stroke-dasharray="2 8"
              fill="none"
              opacity="0.4"
            />
            <path
              d="M 600 110 C 800 230 940 420 1000 560"
              stroke="#CBD5E1"
              stroke-width="1"
              stroke-dasharray="2 8"
              fill="none"
              opacity="0.4"
            />

            <!-- Projected 3D Dot Grid Points -->
            <g>
              <circle
                v-for="(dot, idx) in globeDots"
                :key="idx"
                :cx="dot.cx"
                :cy="dot.cy"
                :r="dot.r"
                fill="#94A3B8"
                :fill-opacity="dot.opacity"
              />
            </g>
          </svg>
        </div>

        <!-- Foreground Matching Cards -->
        <div
          v-reveal="'scale-in'"
          class="relative z-10 mx-auto flex flex-col items-center justify-center gap-6 md:flex-row md:items-center md:gap-3 lg:gap-5"
        >
          <!-- Left Card: Opportunity / Venture Job Card -->
          <div
            class="w-full max-w-[300px] rounded-2xl border border-slate-200/90 bg-white p-5 text-left shadow-xl shadow-slate-200/70 transition-all duration-300 hover:-translate-y-1 hover:shadow-2xl sm:max-w-[315px]"
          >
            <!-- Top dark container with GitHub logo -->
            <div class="flex h-28 w-full items-center justify-center rounded-xl bg-[#0F1E2E]">
              <svg
                class="size-11 fill-current text-white"
                viewBox="0 0 24 24"
                aria-label="GitHub Logo"
              >
                <path
                  d="M12 0C5.37 0 0 5.37 0 12c0 5.31 3.435 9.795 8.205 11.385.6.105.825-.255.825-.57 0-.285-.015-1.23-.015-2.235-3.015.555-3.795-.735-4.035-1.41-.135-.345-.72-1.41-1.23-1.695-.42-.225-1.02-.78-.015-.795.945-.015 1.62.87 1.845 1.23 1.08 1.815 2.805 1.305 3.495.99.105-.78.42-1.305.765-1.605-2.67-.3-5.46-1.335-5.46-5.925 0-1.305.465-2.385 1.23-3.225-.12-.3-.54-1.53.12-3.18 0 0 1.005-.315 3.3 1.23.96-.27 1.98-.405 3-.405s2.04.135 3 .405c2.295-1.56 3.3-1.23 3.3-1.23.66 1.65.24 2.88.12 3.18.765.84 1.23 1.905 1.23 3.225 0 4.605-2.805 5.625-5.475 5.925.435.375.81 1.095.81 2.22 0 1.605-.015 2.895-.015 3.3 0 .315.225.69.825.57A12.02 12.02 0 0024 12c0-6.63-5.37-12-12-12z"
                />
              </svg>
            </div>

            <!-- Role details -->
            <div class="mt-4">
              <h3 class="text-sm font-semibold text-gray-900 sm:text-base">AI DevOps Engineer</h3>
              <p class="mt-0.5 text-xs text-gray-500">Build a customer support agent</p>
            </div>

            <!-- Required Skills -->
            <div class="mt-4 border-t border-slate-100 pt-3">
              <p class="text-[11px] font-medium tracking-wider text-gray-400 uppercase">
                Required Skills
              </p>
              <div class="mt-2 flex flex-wrap gap-1.5">
                <span
                  class="rounded-md border border-gray-200/90 bg-gray-50 px-2.5 py-1 text-xs text-gray-700"
                  >Kubernetes</span
                >
                <span
                  class="rounded-md border border-gray-200/90 bg-gray-50 px-2.5 py-1 text-xs text-gray-700"
                  >Terraform</span
                >
                <span
                  class="rounded-md border border-gray-200/90 bg-gray-50 px-2.5 py-1 text-xs text-gray-700"
                  >Guardrails AI</span
                >
                <span
                  class="rounded-md border border-gray-200/90 bg-gray-50 px-2.5 py-1 text-xs text-gray-700"
                  >Arize/WhyLabs</span
                >
              </div>
            </div>
          </div>

          <!-- Center AI Matching Node with Connection Lines -->
          <div class="relative flex items-center justify-center py-1 md:py-0">
            <!-- Left connecting dotted line (desktop) -->
            <div
              class="hidden h-0.5 w-6 border-t-2 border-dashed border-slate-300 md:block lg:w-9"
            ></div>

            <!-- Center Node Badge -->
            <div
              class="relative z-10 flex size-11 items-center justify-center rounded-xl bg-[#0F1E2E] shadow-xl ring-4 ring-white"
            >
              <svg
                class="size-5 fill-current text-[#05DED5]"
                viewBox="0 0 24 24"
                aria-label="AI Sparkle"
              >
                <path d="M12 0L14.7 9.3L24 12L14.7 14.7L12 24L9.3 14.7L0 12L9.3 9.3L12 0Z" />
              </svg>
            </div>

            <!-- Right connecting dotted line (desktop) -->
            <div
              class="hidden h-0.5 w-6 border-t-2 border-dashed border-slate-300 md:block lg:w-9"
            ></div>
          </div>

          <!-- Right Card: Talent Profile Card -->
          <div
            class="w-full max-w-[300px] rounded-2xl border border-slate-200/90 bg-white p-5 text-left shadow-xl shadow-slate-200/70 transition-all duration-300 hover:-translate-y-1 hover:shadow-2xl sm:max-w-[315px]"
          >
            <!-- Top photo container -->
            <div class="relative h-28 w-full overflow-hidden rounded-xl bg-slate-100">
              <NuxtImg
                src="/images/pages/creatives/hero-1.png"
                alt="Samantha H. - AI DevOps Engineer"
                class="size-full object-cover object-[50%_15%]"
              />
            </div>

            <!-- Talent details + Fit Badge -->
            <div class="mt-4 flex items-start justify-between gap-2">
              <div>
                <h3 class="text-sm font-semibold text-gray-900 sm:text-base">Samantha H.</h3>
                <p class="mt-0.5 text-xs text-gray-500">AI DevOps Engineer</p>
              </div>
              <span
                class="inline-flex shrink-0 items-center gap-1 rounded-full border border-emerald-200 bg-emerald-50 px-2.5 py-0.5 text-xs font-semibold text-emerald-700"
              >
                Good fit
              </span>
            </div>

            <!-- Core Skills -->
            <div class="mt-4 border-t border-slate-100 pt-3">
              <p class="text-[11px] font-medium tracking-wider text-gray-400 uppercase">
                Core skills
              </p>
              <div class="mt-2 flex flex-wrap gap-1.5">
                <span
                  class="rounded-md border border-gray-200/90 bg-gray-50 px-2.5 py-1 text-xs text-gray-700"
                  >Kubernetes</span
                >
                <span
                  class="rounded-md border border-gray-200/90 bg-gray-50 px-2.5 py-1 text-xs text-gray-700"
                  >Terraform</span
                >
                <span
                  class="rounded-md border border-gray-200/90 bg-gray-50 px-2.5 py-1 text-xs text-gray-700"
                  >Python</span
                >
                <span
                  class="rounded-md border border-gray-200/90 bg-gray-50 px-2.5 py-1 text-xs text-gray-700"
                  >Arize/WhyLabs</span
                >
                <span
                  class="rounded-md border border-gray-200/90 bg-gray-50 px-2.5 py-1 text-xs text-gray-700"
                  >Guardrails AI</span
                >
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<script setup lang="ts">
import { computed } from 'vue';

interface GlobeDot {
  cx: number;
  cy: number;
  r: number;
  opacity: number;
}

// 3D Spherical Projection for Dotted Globe
const globeDots = computed<GlobeDot[]>(() => {
  const dots: GlobeDot[] = [];
  const R = 460;
  const tilt = (28 * Math.PI) / 180;

  for (let lat = -10; lat <= 85; lat += 5) {
    const phi = (lat * Math.PI) / 180;
    const lonStep = lat > 65 ? 8 : lat > 45 ? 6 : 5;
    for (let lon = -95; lon <= 95; lon += lonStep) {
      const theta = (lon * Math.PI) / 180;
      const x = R * Math.cos(phi) * Math.sin(theta);
      const y = R * Math.sin(phi);
      const z = R * Math.cos(phi) * Math.cos(theta);

      // 3D rotation along X axis (tilt towards viewer)
      const yRot = y * Math.cos(tilt) - z * Math.sin(tilt);
      const zRot = y * Math.sin(tilt) + z * Math.cos(tilt);

      if (zRot > -30) {
        const depth = (zRot + 30) / (R + 30);
        dots.push({
          cx: Number((600 + x).toFixed(1)),
          cy: Number((480 - yRot).toFixed(1)),
          r: Number((1.1 + depth * 1.5).toFixed(1)),
          opacity: Number(Math.max(0.12, Math.min(0.75, depth * 0.8)).toFixed(2)),
        });
      }
    }
  }
  return dots;
});
</script>

<style scoped lang="css"></style>
