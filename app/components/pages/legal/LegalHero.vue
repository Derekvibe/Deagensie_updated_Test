<script setup lang="ts">
import { Icon } from '@iconify/vue';

interface Props {
  title: string;
  subtitle: string;
  lastUpdated?: string;
  readingTime?: string;
  activePage: 'privacy' | 'terms' | 'cookies';
}

withDefaults(defineProps<Props>(), {
  lastUpdated: 'October 13, 2026',
  readingTime: '7 min read',
});

function handlePrint() {
  if (import.meta.client) {
    window.print();
  }
}
</script>

<template>
  <section class="border-b border-gray-100 bg-white pt-28 pb-12 lg:pt-36 lg:pb-16">
    <div class="mx-auto w-5/6 max-w-7xl">
      <!-- Breadcrumb & Tag -->
      <div class="mb-6 flex flex-wrap items-center justify-between gap-4">
        <div class="flex items-center gap-2 text-xs font-semibold tracking-widest uppercase">
          <NuxtLink to="/" class="text-gray-400 transition-colors hover:text-[#04308F]"
            >Home</NuxtLink
          >
          <span class="text-gray-300">/</span>
          <span class="text-[#04308F]">Legal & Governance</span>
        </div>

        <button
          type="button"
          class="inline-flex items-center gap-1.5 rounded-full border border-gray-200 bg-white px-3.5 py-1.5 text-xs font-medium text-gray-700 shadow-xs transition-all hover:border-[#04308F]/40 hover:bg-gray-50 hover:text-[#04308F]"
          @click="handlePrint"
        >
          <Icon icon="solar:printer-linear" class="text-sm" />
          <span>Print / Save PDF</span>
        </button>
      </div>

      <!-- Main Headline -->
      <div class="max-w-4xl space-y-4">
        <div
          class="inline-flex items-center gap-2 rounded-full bg-[#04308F]/10 px-3.5 py-1 text-xs font-semibold tracking-wider text-[#04308F] uppercase"
        >
          <Icon
            :icon="
              activePage === 'privacy'
                ? 'solar:shield-check-bold'
                : activePage === 'terms'
                  ? 'solar:document-text-bold'
                  : 'solar:cookie-bold'
            "
            class="text-sm"
          />
          <span>Official Policy</span>
        </div>

        <h1 class="type-editorial-title font-serif text-gray-900">
          {{ title }}
        </h1>

        <p class="text-base leading-relaxed text-gray-600 sm:text-lg">
          {{ subtitle }}
        </p>

        <!-- Metadata Strip -->
        <div class="flex flex-wrap items-center gap-4 pt-2 text-xs text-gray-500 sm:text-sm">
          <div class="flex items-center gap-1.5">
            <Icon icon="solar:calendar-linear" class="text-gray-400" />
            <span
              >Effective Date: <strong>{{ lastUpdated }}</strong></span
            >
          </div>
          <span class="hidden text-gray-300 sm:inline">&bull;</span>
          <div class="flex items-center gap-1.5">
            <Icon icon="solar:clock-circle-linear" class="text-gray-400" />
            <span>{{ readingTime }}</span>
          </div>
          <span class="hidden text-gray-300 sm:inline">&bull;</span>
          <div class="flex items-center gap-1.5">
            <Icon icon="solar:global-linear" class="text-gray-400" />
            <span>Applicable Worldwide (GDPR / CCPA / Delaware)</span>
          </div>
        </div>
      </div>
    </div>
  </section>
</template>
