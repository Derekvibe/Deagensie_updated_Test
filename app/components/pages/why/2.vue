<script setup lang="ts">
import { Icon } from '@iconify/vue';

interface Stage {
  id: number;
  code: string;
  name: string;
  tagline: string;
  score: string;
  vertex: { x: number; y: number };
  polyPt: { x: number; y: number };
  badgePos: { x: number; y: number };
  labelPos: { x: number; y: number };
  textAnchor: 'middle' | 'start' | 'end';
}

const stages: Stage[] = [
  {
    id: 0,
    code: '01',
    name: 'Discover',
    tagline: 'Research your market, audience and competitors.',
    score: '4.9',
    vertex: { x: 300, y: 100 },
    polyPt: { x: 300, y: 115 },
    badgePos: { x: 300, y: 52 },
    labelPos: { x: 300, y: 82 },
    textAnchor: 'middle',
  },
  {
    id: 1,
    code: '02',
    name: 'Define',
    tagline: 'Develop clear positioning and growth strategies.',
    score: '4.8',
    vertex: { x: 447.2, y: 185 },
    polyPt: { x: 441.2, y: 188.5 },
    badgePos: { x: 468, y: 154 },
    labelPos: { x: 468, y: 178 },
    textAnchor: 'start',
  },
  {
    id: 2,
    code: '03',
    name: 'Design',
    tagline: 'Create compelling brands and digital experiences.',
    score: '5.0',
    vertex: { x: 447.2, y: 355 },
    polyPt: { x: 435.1, y: 348 },
    badgePos: { x: 468, y: 362 },
    labelPos: { x: 468, y: 386 },
    textAnchor: 'start',
  },
  {
    id: 3,
    code: '04',
    name: 'Develop',
    tagline: 'Build scalable digital products and systems.',
    score: '4.7',
    vertex: { x: 300, y: 440 },
    polyPt: { x: 300, y: 415 },
    badgePos: { x: 300, y: 494 },
    labelPos: { x: 300, y: 472 },
    textAnchor: 'middle',
  },
  {
    id: 4,
    code: '05',
    name: 'Deploy',
    tagline: 'Launch integrated campaigns.',
    score: '4.8',
    vertex: { x: 152.8, y: 355 },
    polyPt: { x: 183.1, y: 337.5 },
    badgePos: { x: 132, y: 362 },
    labelPos: { x: 132, y: 386 },
    textAnchor: 'end',
  },
  {
    id: 5,
    code: '06',
    name: 'Drive Growth',
    tagline: 'Measure, optimize and continuously improve.',
    score: '5.0',
    vertex: { x: 152.8, y: 185 },
    polyPt: { x: 165.8, y: 192.5 },
    badgePos: { x: 132, y: 154 },
    labelPos: { x: 132, y: 178 },
    textAnchor: 'end',
  },
];

const activeStage = ref<number | null>(null);

// Concentric polygon ring coordinates (r = 42.5, 85, 127.5, 170)
const rings = [
  '300,227.5 336.8,248.8 336.8,291.3 300,312.5 263.2,291.3 263.2,248.8',
  '300,185 373.6,227.5 373.6,312.5 300,355 226.4,312.5 226.4,227.5',
  '300,142.5 410.4,206.3 410.4,333.8 300,397.5 189.6,333.8 189.6,206.3',
  '300,100 447.2,185 447.2,355 300,440 152.8,355 152.8,185',
];

const capabilityPolygonPoints = computed(() =>
  stages.map((s) => `${s.polyPt.x},${s.polyPt.y}`).join(' ')
);
</script>

<template>
  <section class="border-b border-gray-100 bg-[#FCFCFE] py-20 text-gray-900 sm:py-24 lg:py-24">
    <div class="mx-auto w-5/6 max-w-7xl space-y-12 sm:space-y-16">
      <!-- Centered Section Header -->
      <div v-reveal="'fade-up'" class="mx-auto max-w-3xl space-y-4 text-center">
        <h2
          class="font-serif text-3xl leading-tight font-normal tracking-tight text-gray-900 sm:text-4xl lg:text-5xl"
        >
          Deagensie 6D’s Approach. <br />
          <span class="text-[#04308F]">From Insight to Impact.</span>
        </h2>
        <p
          class="font-open-sans mx-auto max-w-2xl text-center text-base leading-relaxed font-normal text-gray-600 sm:text-lg"
        >
          We turn ideas into growth through a six-stage approach: discover the opportunity, define
          the strategy, design the experience, develop the solution, deploy to market, and drive
          growth through continuous optimization.
        </p>
      </div>

      <!-- Main Visual & Checklist Card -->
      <div
        v-reveal="'fade-up'"
        class="rounded-3xl border border-gray-100 bg-white p-6 shadow-sm sm:p-10 lg:p-14"
      >
        <div class="grid grid-cols-1 items-center gap-12 lg:grid-cols-12 lg:gap-14">
          <!-- Left Column: Impact Callout & 6D Checklist -->
          <div class="space-y-6 lg:col-span-6 xl:col-span-6">
            <div
              class="rounded-2xl border border-gray-100 bg-gray-50/80 p-5 text-sm leading-relaxed font-medium text-gray-700"
            >
              Every stage is intentional. Every solution is built for impact. Every move brings your
              business closer to its full potential.
            </div>

            <!-- 6D Stage Checklist with Interactive Linkage to Chart -->
            <ul class="space-y-2.5 pt-2">
              <li
                v-for="stage in stages"
                :key="stage.name"
                class="group flex cursor-pointer items-start gap-3 rounded-xl border border-transparent p-2.5 transition-all duration-200 hover:border-gray-200 hover:bg-gray-50"
                :class="
                  activeStage === stage.id ? 'border-[#026662]/30 bg-[#026662]/5 shadow-2xs' : ''
                "
                @mouseenter="activeStage = stage.id"
                @mouseleave="activeStage = null"
              >
                <div
                  class="mt-0.5 flex size-5 shrink-0 items-center justify-center rounded-full transition-colors"
                  :class="
                    activeStage === stage.id
                      ? 'bg-[#026662] text-white'
                      : 'bg-[#026662]/10 text-[#026662]'
                  "
                >
                  <Icon icon="lucide:check" class="size-3.5 stroke-[2.5]" />
                </div>
                <div class="text-xs leading-relaxed sm:text-sm">
                  <span class="font-bold text-gray-900">{{ stage.name }}:</span>
                  <span class="text-gray-600"> {{ stage.tagline }}</span>
                </div>
              </li>
            </ul>
          </div>

          <!-- Right Column: Hexagonal Radar Graph Visualization -->
          <div class="flex flex-col items-center justify-center lg:col-span-6 xl:col-span-6">
            <div class="relative w-full max-w-[540px]">
              <svg
                viewBox="0 0 600 560"
                class="h-auto w-full select-none"
                xmlns="http://www.w3.org/2000/svg"
              >
                <defs>
                  <!-- Center Avatar Clipping Mask -->
                  <clipPath id="radar-avatar-clip">
                    <circle cx="300" cy="270" r="32" />
                  </clipPath>

                  <!-- Capability Polygon Gradient Fill -->
                  <radialGradient id="radar-fill" cx="50%" cy="50%" r="50%">
                    <stop offset="0%" stop-color="#026662" stop-opacity="0.18" />
                    <stop offset="100%" stop-color="#026662" stop-opacity="0.08" />
                  </radialGradient>
                </defs>

                <!-- Concentric Hexagon Grid Rings -->
                <polygon
                  v-for="(ringPoints, rIdx) in rings"
                  :key="rIdx"
                  :points="ringPoints"
                  fill="none"
                  stroke="#E2E8F0"
                  :stroke-width="rIdx === rings.length - 1 ? 1.5 : 1"
                  :stroke-dasharray="rIdx === rings.length - 1 ? 'none' : '3 4'"
                  opacity="0.85"
                />

                <!-- 6 Radial Spoke Axes -->
                <line
                  v-for="stage in stages"
                  :key="stage.code"
                  x1="300"
                  y1="270"
                  :x2="stage.vertex.x"
                  :y2="stage.vertex.y"
                  stroke="#E2E8F0"
                  stroke-width="1.2"
                  :opacity="activeStage === stage.id ? 1 : 0.65"
                />

                <!-- Assessed Capability Polygon (Green shaded area from reference) -->
                <polygon
                  :points="capabilityPolygonPoints"
                  fill="url(#radar-fill)"
                  stroke="#026662"
                  stroke-width="2.5"
                  stroke-linejoin="round"
                  class="transition-all duration-300"
                />

                <!-- Small Nodes at Polygon Vertices -->
                <circle
                  v-for="stage in stages"
                  :key="'pt-' + stage.name"
                  :cx="stage.polyPt.x"
                  :cy="stage.polyPt.y"
                  :r="activeStage === stage.id ? 6 : 4"
                  fill="#026662"
                  stroke="#FFFFFF"
                  stroke-width="2"
                  class="transition-all duration-200"
                />

                <!-- Outer Grid Vertex Corner Markers (Small squares from reference) -->
                <rect
                  v-for="stage in stages"
                  :key="'node-' + stage.name"
                  :x="stage.vertex.x - 4"
                  :y="stage.vertex.y - 4"
                  width="8"
                  height="8"
                  rx="2"
                  fill="white"
                  stroke="#CBD5E1"
                  stroke-width="1.5"
                  :class="activeStage === stage.id ? 'stroke-[#026662]' : ''"
                />

                <!-- Center Avatar: Portrait with Circular Ring Frame -->
                <circle cx="300" cy="270" r="35" fill="white" stroke="#E2E8F0" stroke-width="3" />
                <image
                  href="/images/Godwin.jpeg"
                  x="266"
                  y="236"
                  width="68"
                  height="68"
                  clip-path="url(#radar-avatar-clip)"
                  preserveAspectRatio="xMidYMid slice"
                />
                <circle
                  cx="300"
                  cy="270"
                  r="33"
                  fill="none"
                  stroke="#026662"
                  stroke-width="1.5"
                  opacity="0.4"
                />

                <!-- Vertex Stage Labels & Score Badges -->
                <g
                  v-for="stage in stages"
                  :key="'label-' + stage.name"
                  class="cursor-pointer transition-opacity duration-200"
                  :opacity="activeStage === null || activeStage === stage.id ? 1 : 0.6"
                  @mouseenter="activeStage = stage.id"
                  @mouseleave="activeStage = null"
                >
                  <!-- Score Badge Pill (e.g. 3.7, 4.7, 4.5 from reference image) -->
                  <g>
                    <rect
                      :x="
                        stage.textAnchor === 'middle'
                          ? stage.badgePos.x - 17
                          : stage.textAnchor === 'start'
                            ? stage.badgePos.x
                            : stage.badgePos.x - 34
                      "
                      :y="stage.badgePos.y - 12"
                      width="34"
                      height="18"
                      rx="5"
                      fill="#F0FDF4"
                      stroke="#DCFCE7"
                      stroke-width="1"
                    />
                    <text
                      :x="
                        stage.textAnchor === 'middle'
                          ? stage.badgePos.x
                          : stage.textAnchor === 'start'
                            ? stage.badgePos.x + 17
                            : stage.badgePos.x - 17
                      "
                      :y="stage.badgePos.y + 1"
                      text-anchor="middle"
                      font-size="11"
                      font-weight="700"
                      fill="#166534"
                      font-family="system-ui, -apple-system, sans-serif"
                    >
                      {{ stage.score }}
                    </text>
                  </g>

                  <!-- Stage Title Label -->
                  <text
                    :x="stage.labelPos.x"
                    :y="stage.labelPos.y"
                    :text-anchor="stage.textAnchor"
                    font-size="13"
                    font-weight="600"
                    fill="#1F2937"
                    font-family="'Open Sans', system-ui, sans-serif"
                    class="transition-colors"
                  >
                    {{ stage.name }}
                  </text>
                </g>
              </svg>

              <!-- Legend (matching screenshot pill + 'Assessed capability level') -->
              <div class="mt-4 flex items-center justify-center gap-2.5">
                <span class="inline-block h-2.5 w-6 rounded-full bg-[#026662]"></span>
                <span class="text-xs font-medium text-gray-700">Assessed capability level</span>
              </div>
            </div>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>

<style scoped lang="css"></style>
