<script setup lang="ts">
import { Icon } from '@iconify/vue';

const audiences = [
  'Startups',
  'Category Disruptors',
  'Fortune 100',
  'High-Growth SMEs',
  'African Innovators',
];
</script>

<template>
  <section class="border-b border-gray-100 bg-white py-16 text-gray-900 lg:py-24">
    <div class="mx-auto w-5/6 max-w-7xl space-y-12 lg:space-y-16">
      <!-- Top Card: Headline, Description, Tags and Abstract Geometry -->
      <div
        v-reveal="'scale-in'"
        class="relative overflow-hidden rounded-[28px] border border-gray-200/80 bg-[#F4F7FC]/80 p-8 sm:p-12 lg:p-16"
      >
        <div class="grid grid-cols-1 items-center gap-10 lg:grid-cols-12 lg:gap-12">
          <!-- Left Content -->
          <div class="space-y-6 lg:col-span-7">
            <span
              class="inline-block rounded-full bg-[#04308F]/10 px-4 py-1.5 text-xs font-semibold tracking-widest text-[#04308F] uppercase"
            >
              Ecosystem Focus
            </span>

            <h2
              class="font-serif text-3xl leading-[1.15] font-normal tracking-tight text-gray-900 sm:text-4xl lg:text-5xl"
            >
              Premium growth solutions for <br class="hidden sm:inline" />
              <span class="text-[#04308F]">visionary brands</span>
            </h2>

            <p class="max-w-xl text-base leading-relaxed font-normal text-gray-600 sm:text-lg">
              Growth isn&apos;t accidental; it&apos;s engineered. We partner with startups ready to
              scale, ambitious category disruptors, and established brands seeking reinvention.
            </p>

            <!-- Audience Chips -->
            <div class="flex flex-wrap gap-2.5 pt-2">
              <span
                v-for="item in audiences"
                :key="item"
                class="rounded-full border border-gray-200/90 bg-white px-4 py-1.5 text-xs font-semibold text-gray-700 shadow-2xs transition-colors hover:border-[#04308F]/30 hover:text-[#04308F]"
              >
                {{ item }}
              </span>
            </div>
          </div>

          <!-- Right Abstract Geometric Art (Deagensie Palette) -->
          <div class="relative flex items-center justify-center lg:col-span-5">
            <svg
              viewBox="0 0 380 340"
              class="h-auto w-full max-w-[340px] select-none lg:max-w-none"
              fill="none"
              xmlns="http://www.w3.org/2000/svg"
              aria-hidden="true"
            >
              <defs>
                <!-- Striped pattern for the circular node -->
                <pattern
                  id="diagHatch1"
                  width="8"
                  height="8"
                  patternTransform="rotate(45 0 0)"
                  patternUnits="userSpaceOnUse"
                >
                  <line x1="0" y1="0" x2="0" y2="8" stroke="#05DED5" stroke-width="2" />
                </pattern>
                <!-- Dotted pattern for top cube face -->
                <pattern
                  id="dotPattern1"
                  x="0"
                  y="0"
                  width="10"
                  height="10"
                  patternUnits="userSpaceOnUse"
                >
                  <circle cx="2" cy="2" r="1.2" fill="#04308F" fill-opacity="0.35" />
                </pattern>
              </defs>

              <!-- Connected Lines -->
              <line
                x1="260"
                y1="85"
                x2="280"
                y2="75"
                stroke="#94A3B8"
                stroke-width="1.2"
                stroke-dasharray="3 3"
              />
              <line
                x1="260"
                y1="85"
                x2="245"
                y2="50"
                stroke="#94A3B8"
                stroke-width="1.2"
                stroke-dasharray="3 3"
              />
              <line
                x1="260"
                y1="85"
                x2="230"
                y2="140"
                stroke="#94A3B8"
                stroke-width="1.2"
                stroke-dasharray="3 3"
              />

              <!-- Junction Dot -->
              <circle cx="260" cy="85" r="3.5" fill="#04308F" />

              <!-- Top-Right Textured Circle Node -->
              <g transform="translate(260, 20)">
                <circle cx="50" cy="50" r="48" fill="#E6FEFD" />
                <circle cx="50" cy="50" r="48" fill="url(#diagHatch1)" fill-opacity="0.75" />
                <circle cx="50" cy="50" r="48" stroke="#05DED5" stroke-width="1.5" />
              </g>

              <!-- Small Top Isometric Diamond -->
              <g transform="translate(230, 25)">
                <polygon points="15,0 30,10 15,20 0,10" fill="#E6FEFD" />
                <polygon points="0,10 15,20 15,36 0,26" fill="#04308F" />
                <polygon points="30,10 15,20 15,36 30,26" fill="#026662" />
              </g>

              <!-- Main Isometric 3D Cube -->
              <g transform="translate(170, 100)">
                <!-- Top Face -->
                <polygon
                  points="65,0 130,38 65,76 0,38"
                  fill="#EBF2FF"
                  stroke="#CBD5E1"
                  stroke-width="1"
                />
                <polygon points="65,0 130,38 65,76 0,38" fill="url(#dotPattern1)" />

                <!-- Left Face (Deep Blue) -->
                <polygon
                  points="0,38 65,76 65,152 0,114"
                  fill="#04308F"
                  stroke="#04308F"
                  stroke-width="1"
                />

                <!-- Right Face (Vibrant Teal / Slate) -->
                <polygon
                  points="130,38 65,76 65,152 130,114"
                  fill="#026662"
                  stroke="#026662"
                  stroke-width="1"
                />
              </g>
            </svg>
          </div>
        </div>
      </div>

      <!-- Bottom Metrics Row: Two Columns with Icons and Stats -->
      <div v-reveal="'fade-up'" class="grid grid-cols-1 gap-10 md:grid-cols-2 lg:gap-16">
        <!-- Metric Column 1 -->
        <div class="space-y-4">
          <!-- Small Rounded Box Icon -->
          <div
            class="flex size-11 items-center justify-center rounded-xl border border-gray-200 bg-white text-[#04308F] shadow-2xs"
          >
            <Icon icon="lucide:trending-up" class="text-xl" />
          </div>

          <!-- Big Stat -->
          <div class="font-serif text-5xl font-normal tracking-tight text-gray-900 sm:text-6xl">
            +40%
          </div>

          <!-- Metric Label -->
          <h3 class="text-base font-bold text-gray-900">Accelerated Time-to-Market</h3>

          <!-- Description -->
          <p class="max-w-md text-sm leading-relaxed text-gray-600 sm:text-base">
            Applied venture methodology helps founders and enterprise teams build stronger
            positioning, rapid market validation, and scalable digital solutions in real work.
          </p>
        </div>

        <!-- Metric Column 2 (Divided on Desktop) -->
        <div class="space-y-4 md:border-l md:border-gray-200 md:pl-10 lg:pl-16">
          <!-- Small Rounded Box Icon -->
          <div
            class="flex size-11 items-center justify-center rounded-xl border border-gray-200 bg-white text-[#05DED5] shadow-2xs"
          >
            <Icon icon="lucide:zap" class="text-xl text-[#026662]" />
          </div>

          <!-- Big Stat -->
          <div class="font-serif text-5xl font-normal tracking-tight text-gray-900 sm:text-6xl">
            +30%
          </div>

          <!-- Metric Label -->
          <h3 class="text-base font-bold text-gray-900">Modeled Venture Efficiency</h3>

          <!-- Description -->
          <p class="max-w-md text-sm leading-relaxed text-gray-600 sm:text-base">
            Integrated strategy, borderless creative talent, and AI-led execution compound the
            productivity and growth gains visionary organizations realize as they scale.
          </p>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped lang="css"></style>
