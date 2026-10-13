<script setup lang="ts">
import { Icon } from '@iconify/vue';

const isVisible = ref(false);

const STORAGE_KEY = 'deag_cookie_consent';

onMounted(() => {
  if (import.meta.client) {
    try {
      const consent = localStorage.getItem(STORAGE_KEY);
      if (!consent) {
        // Subtle delay for smoother page entrance
        setTimeout(() => {
          isVisible.value = true;
        }, 700);
      }
    } catch {
      // Storage restricted, display banner safely
      isVisible.value = true;
    }
  }
});

function acceptCookies() {
  if (import.meta.client) {
    try {
      localStorage.setItem(STORAGE_KEY, 'accepted');
      localStorage.setItem(
        'deag_cookie_preferences',
        JSON.stringify({
          necessary: true,
          functional: true,
          analytics: true,
          marketing: true,
        })
      );
    } catch {
      // Fallback
    }
  }
  isVisible.value = false;
}

function dismissBanner() {
  if (import.meta.client) {
    try {
      localStorage.setItem(STORAGE_KEY, 'dismissed');
      localStorage.setItem(
        'deag_cookie_preferences',
        JSON.stringify({
          necessary: true,
          functional: false,
          analytics: false,
          marketing: false,
        })
      );
    } catch {
      // Fallback
    }
  }
  isVisible.value = false;
}
</script>

<template>
  <Transition name="cookie-slide">
    <div
      v-if="isVisible"
      role="region"
      aria-label="Cookie consent banner"
      class="fixed bottom-4 left-4 z-50 w-[calc(100%-2rem)] max-w-md sm:bottom-6 sm:left-6"
    >
      <div
        class="relative overflow-hidden rounded-3xl border border-white/15 bg-[#020B1E]/95 p-5 text-white shadow-2xl backdrop-blur-md sm:p-6"
      >
        <!-- Subtle Glow Effect -->
        <div
          class="pointer-events-none absolute -top-12 -right-12 h-32 w-32 rounded-full bg-[#05DED5]/15 blur-2xl"
        />

        <!-- Top Row: Icon + Title + Close (X) Button -->
        <div class="flex items-start justify-between gap-3">
          <div class="flex items-center gap-3">
            <div
              class="flex size-10 shrink-0 items-center justify-center rounded-2xl bg-[#04308F] text-[#05DED5] shadow-inner shadow-[#05DED5]/20"
            >
              <Icon icon="solar:cookie-bold" class="text-xl" />
            </div>
            <div>
              <h3 class="text-sm font-bold tracking-tight text-white sm:text-base">
                Cookie Preferences
              </h3>
              <p class="text-[11px] font-medium tracking-wider text-[#05DED5] uppercase">
                Privacy & Transparency
              </p>
            </div>
          </div>

          <!-- X Cancel / Dismiss Button -->
          <button
            type="button"
            aria-label="Close cookie banner"
            class="group -mt-1 -mr-1 flex size-8 shrink-0 items-center justify-center rounded-full text-gray-400 transition-colors hover:bg-white/10 hover:text-white focus:outline-hidden"
            @click="dismissBanner"
          >
            <Icon icon="lucide:x" class="text-lg transition-transform group-hover:scale-110" />
          </button>
        </div>

        <!-- Description -->
        <p class="mt-3 text-xs leading-relaxed text-gray-300 sm:text-sm">
          We use cookies to protect your session, power our Growth Lab and TaaS features, and
          analyze traffic. You can accept all or dismiss. Read our
          <NuxtLink
            to="/cookies"
            class="font-medium text-[#05DED5] underline transition-colors hover:text-white"
            @click="isVisible = false"
          >
            Cookie Policy </NuxtLink
          >.
        </p>

        <!-- Action Buttons -->
        <div class="mt-4 flex flex-wrap items-center justify-between gap-3 pt-1">
          <NuxtLink
            to="/cookies"
            class="text-xs text-gray-400 underline transition-colors hover:text-white"
            @click="isVisible = false"
          >
            Manage choices
          </NuxtLink>

          <div class="flex items-center gap-2">
            <button
              type="button"
              class="rounded-full border border-white/20 bg-white/5 px-4 py-2 text-xs font-semibold text-gray-300 transition-all hover:bg-white/10 hover:text-white"
              @click="dismissBanner"
            >
              Cancel
            </button>
            <button
              type="button"
              class="rounded-full bg-[#05DED5] px-5 py-2 text-xs font-bold text-[#020B1E] shadow-md shadow-[#05DED5]/25 transition-all hover:scale-105 hover:bg-white"
              @click="acceptCookies"
            >
              Accept Cookies
            </button>
          </div>
        </div>
      </div>
    </div>
  </Transition>
</template>

<style scoped>
.cookie-slide-enter-active,
.cookie-slide-leave-active {
  transition: all 0.4s cubic-bezier(0.16, 1, 0.3, 1);
}

.cookie-slide-enter-from,
.cookie-slide-leave-to {
  opacity: 0;
  transform: translateY(24px) scale(0.96);
}
</style>
