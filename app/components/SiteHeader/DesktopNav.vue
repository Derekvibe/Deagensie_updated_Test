<script setup lang="ts">
import { Icon } from '@iconify/vue';

type DesktopMenu = 'business' | 'creatives' | 'why' | 'about' | 'subscription' | 'resource';

const route = useRoute();
const desktopNavRef = ref<HTMLElement | null>(null);
const activeDesktopMenu = ref<DesktopMenu | null>(null);
let closeTimer: ReturnType<typeof setTimeout> | undefined;

const menuItems: { id: DesktopMenu; label: string; to: string }[] = [
  { id: 'business', label: 'Ventures', to: '/business' },
  { id: 'creatives', label: 'Creatives', to: '/creatives' },
  { id: 'why', label: 'Why Deagensie?', to: '/why' },
  { id: 'about', label: 'About Us', to: '/about' },
  { id: 'resource', label: 'Resources', to: '/resource' },
];

const directLinks: { label: string; to: string }[] = [];

const cancelClose = () => {
  if (!closeTimer) return;
  clearTimeout(closeTimer);
  closeTimer = undefined;
};

const openDesktopMenu = (menu: DesktopMenu) => {
  cancelClose();
  activeDesktopMenu.value = menu;
};

const closeDesktopMenu = () => {
  cancelClose();
  activeDesktopMenu.value = null;
};

const scheduleDesktopMenuClose = () => {
  cancelClose();
  closeTimer = setTimeout(closeDesktopMenu, 180);
};

const handleDesktopNavFocusOut = (event: FocusEvent) => {
  const nextTarget = event.relatedTarget;
  if (!(nextTarget instanceof Node) || !desktopNavRef.value?.contains(nextTarget)) {
    closeDesktopMenu();
  }
};

watch(route, closeDesktopMenu);

onUnmounted(cancelClose);
</script>

<template>
  <nav
    ref="desktopNavRef"
    class="flex flex-1 items-center"
    @mouseleave="scheduleDesktopMenuClose"
    @mouseenter="cancelClose"
    @focusout="handleDesktopNavFocusOut"
    @keydown.esc="closeDesktopMenu"
  >
    <div class="mx-auto flex gap-4 text-xs font-semibold xl:gap-6 xl:text-sm xl:leading-relaxed">
      <NuxtLink
        v-for="item in menuItems"
        :key="item.id"
        :to="item.to"
        class="inline-flex items-center gap-1.5 hover:underline"
        @mouseenter="openDesktopMenu(item.id)"
        @focus="openDesktopMenu(item.id)"
      >
        {{ item.label }}
        <svg
          width="16"
          height="16"
          viewBox="0 0 20 20"
          fill="none"
          xmlns="http://www.w3.org/2000/svg"
        >
          <path
            d="M16.6 7.45831L11.1667 12.8916C10.525 13.5333 9.475 13.5333 8.83333 12.8916L3.4 7.45831"
            stroke="currentColor"
            stroke-width="1.5"
            stroke-miterlimit="10"
            stroke-linecap="round"
            stroke-linejoin="round"
          />
        </svg>
      </NuxtLink>
      <NuxtLink
        v-for="link in directLinks"
        :key="link.to"
        :to="link.to"
        class="inline-flex items-center hover:underline"
        @mouseenter="closeDesktopMenu"
        @focus="closeDesktopMenu"
      >
        {{ link.label }}
      </NuxtLink>
    </div>
    <NuxtLink
      to="https://app-deagensie-waitlist.vercel.app/"
      class="text-foreground rounded-full bg-[#05DED5] px-4 py-2 text-sm font-semibold transition-transform hover:scale-105 xl:px-6 xl:py-3 xl:text-base"
      @focus="closeDesktopMenu"
    >
      Enter Deagensie
    </NuxtLink>
  </nav>

  <!-- Desktop Navigation High-Opacity Neutral Gray Backdrop Overlay -->
  <Teleport to="body">
    <Transition
      enter-active-class="transition-opacity duration-200 ease-out"
      enter-from-class="opacity-0"
      enter-to-class="opacity-100"
      leave-active-class="transition-opacity duration-150 ease-in"
      leave-from-class="opacity-100"
      leave-to-class="opacity-0"
    >
      <div
        v-if="activeDesktopMenu"
        class="fixed inset-0 z-40 bg-gray-900/90 backdrop-blur-md"
        aria-hidden="true"
        @click="closeDesktopMenu"
        @mouseenter="closeDesktopMenu"
      />
    </Transition>
  </Teleport>

  <div
    v-if="activeDesktopMenu"
    class="text-popover-foreground animate-in fade-in-0 zoom-in-95 fixed top-[calc((var(--spacing)*20)+(var(--spacing)*1))] left-1/2 z-50 -translate-x-1/2 rounded-3xl border border-gray-200/80 bg-white shadow-2xl outline-none"
    @mouseenter="cancelClose"
    @mouseleave="scheduleDesktopMenuClose"
  >
    <div
      v-if="activeDesktopMenu === 'business'"
      class="flex w-[860px] max-w-[calc(100vw-3rem)] gap-6 rounded-[inherit] p-6 lg:gap-8 lg:p-7"
    >
      <div class="flex flex-1 flex-col justify-between">
        <div class="space-y-2">
          <NuxtLink
            to="/business/growth-lab"
            class="group flex items-start gap-3.5 rounded-2xl p-2.5 transition-colors hover:bg-gray-100/70"
            @click="closeDesktopMenu"
          >
            <div
              class="flex size-10 shrink-0 items-center justify-center rounded-xl border border-gray-200/80 bg-gray-50 text-xl text-[#026662] transition-colors group-hover:bg-[#026662] group-hover:text-white"
            >
              <Icon icon="hugeicons:target-02" />
            </div>
            <div>
              <p class="text-sm font-semibold text-gray-950 group-hover:text-[#026662]">
                Venture's Growth Lab
              </p>
              <p class="mt-0.5 text-xs leading-relaxed text-gray-500">
                Strategy, branding, marketing, and digital platforms to turn ventures into scalable,
                market-ready businesses.
              </p>
            </div>
          </NuxtLink>

          <NuxtLink
            to="/business/taas"
            class="group flex items-start gap-3.5 rounded-2xl p-2.5 transition-colors hover:bg-gray-100/70"
            @click="closeDesktopMenu"
          >
            <div
              class="flex size-10 shrink-0 items-center justify-center rounded-xl border border-gray-200/80 bg-gray-50 text-xl text-[#026662] transition-colors group-hover:bg-[#026662] group-hover:text-white"
            >
              <Icon icon="hugeicons:user-group" />
            </div>
            <div>
              <p class="text-sm font-semibold text-gray-950 group-hover:text-[#026662]">
                TaaS for Ventures
              </p>
              <p class="mt-0.5 text-xs leading-relaxed text-gray-500">
                On-demand creative squads and growth specialists embedded directly into your
                venture.
              </p>
            </div>
          </NuxtLink>
        </div>

        <div class="mt-4 border-t border-gray-100 pt-3">
          <NuxtLink
            to="/business"
            class="inline-flex items-center gap-2 text-xs font-semibold text-[#026662] hover:underline sm:text-sm"
            @click="closeDesktopMenu"
          >
            Explore all venture solutions
            <Icon icon="hugeicons:arrow-right-02" class="text-base" />
          </NuxtLink>
        </div>
      </div>

      <div
        class="relative flex w-[290px] shrink-0 flex-col justify-between overflow-hidden rounded-2xl border border-[#05DED5]/30 bg-[#E6FEFD] p-5 text-gray-950 lg:w-[310px] lg:p-6"
      >
        <div class="space-y-2">
          <p class="text-lg leading-tight font-bold lg:text-xl">Build a Scalable Brand</p>
          <NuxtLink
            to="https://app-deagensie-waitlist.vercel.app/"
            target="_blank"
            rel="noopener noreferrer"
            class="inline-flex items-center gap-1.5 text-xs font-semibold text-[#04308F] hover:underline lg:text-sm"
            @click="closeDesktopMenu"
          >
            Enter Deagensie Waitlist
            <Icon icon="hugeicons:arrow-right-02" class="text-base" />
          </NuxtLink>
        </div>
        <div class="mt-3 overflow-hidden rounded-xl border border-gray-200/80 bg-white p-1.5">
          <NuxtImg
            src="/images/pages/(home)/hero.webp"
            class="aspect-16/10 w-full rounded-lg object-cover"
          />
        </div>
      </div>
    </div>

    <div
      v-else-if="activeDesktopMenu === 'creatives'"
      class="flex w-[860px] max-w-[calc(100vw-3rem)] gap-6 rounded-[inherit] p-6 lg:gap-8 lg:p-7"
    >
      <div class="flex flex-1 flex-col justify-between">
        <div class="space-y-2">
          <NuxtLink
            to="/creatives"
            class="group flex items-start gap-3.5 rounded-2xl p-2.5 transition-colors hover:bg-gray-100/70"
            @click="closeDesktopMenu"
          >
            <div
              class="flex size-10 shrink-0 items-center justify-center rounded-xl border border-gray-200/80 bg-gray-50 text-xl text-[#026662] transition-colors group-hover:bg-[#026662] group-hover:text-white"
            >
              <Icon icon="hugeicons:user-ai" />
            </div>
            <div>
              <p class="text-sm font-semibold text-gray-950 group-hover:text-[#026662]">
                Talent-as-a-Service (TaaS)
              </p>
              <p class="mt-0.5 text-xs leading-relaxed text-gray-500">
                Predictive AI talent matching engine connecting African talent to global roles.
              </p>
            </div>
          </NuxtLink>

          <NuxtLink
            to="/creatives"
            class="group flex items-start gap-3.5 rounded-2xl p-2.5 transition-colors hover:bg-gray-100/70"
            @click="closeDesktopMenu"
          >
            <div
              class="flex size-10 shrink-0 items-center justify-center rounded-xl border border-gray-200/80 bg-gray-50 text-xl text-[#026662] transition-colors group-hover:bg-[#026662] group-hover:text-white"
            >
              <Icon icon="hugeicons:paint-brush-01" />
            </div>
            <div>
              <p class="text-sm font-semibold text-gray-950 group-hover:text-[#026662]">
                For Creatives & Designers
              </p>
              <p class="mt-0.5 text-xs leading-relaxed text-gray-500">
                Build your talent profile, earn competitive global income and remain rooted in
                Africa.
              </p>
            </div>
          </NuxtLink>

          <NuxtLink
            to="/register"
            class="group flex items-start gap-3.5 rounded-2xl p-2.5 transition-colors hover:bg-gray-100/70"
            @click="closeDesktopMenu"
          >
            <div
              class="flex size-10 shrink-0 items-center justify-center rounded-xl border border-gray-200/80 bg-gray-50 text-xl text-[#026662] transition-colors group-hover:bg-[#026662] group-hover:text-white"
            >
              <Icon icon="hugeicons:user-group-02" />
            </div>
            <div>
              <p class="text-sm font-semibold text-gray-950 group-hover:text-[#026662]">
                Join Creative Community
              </p>
              <p class="mt-0.5 text-xs leading-relaxed text-gray-500">
                Network of emerging young leaders, innovators and top creative minds across the
                continent.
              </p>
            </div>
          </NuxtLink>
        </div>

        <div class="mt-4 border-t border-gray-100 pt-3">
          <NuxtLink
            to="/creatives"
            class="inline-flex items-center gap-2 text-xs font-semibold text-[#026662] hover:underline sm:text-sm"
            @click="closeDesktopMenu"
          >
            Learn about our creative talent
            <Icon icon="hugeicons:arrow-right-02" class="text-base" />
          </NuxtLink>
        </div>
      </div>

      <div
        class="relative flex w-[290px] shrink-0 flex-col justify-between overflow-hidden rounded-2xl border border-[#05DED5]/30 bg-[#E6FEFD] p-5 text-gray-950 lg:w-[310px] lg:p-6"
      >
        <div class="space-y-2">
          <p class="text-lg leading-tight font-bold lg:text-xl">Hire Top 1% African Creatives</p>
          <NuxtLink
            to="/subscription"
            class="inline-flex items-center gap-1.5 text-xs font-semibold text-[#04308F] hover:underline lg:text-sm"
            @click="closeDesktopMenu"
          >
            Explore Talent Subscriptions
            <Icon icon="hugeicons:arrow-right-02" class="text-base" />
          </NuxtLink>
        </div>
        <div class="mt-3 overflow-hidden rounded-xl border border-gray-200/80 bg-white p-1.5">
          <NuxtImg
            src="/images/pages/why/hero-4.png"
            class="aspect-16/10 w-full rounded-lg object-cover"
          />
        </div>
      </div>
    </div>

    <div
      v-else-if="activeDesktopMenu === 'why'"
      class="flex w-[860px] max-w-[calc(100vw-3rem)] gap-6 rounded-[inherit] p-6 lg:gap-8 lg:p-7"
    >
      <div class="flex flex-1 flex-col justify-between">
        <div class="space-y-2">
          <NuxtLink
            to="/why"
            class="group flex items-start gap-3.5 rounded-2xl p-2.5 transition-colors hover:bg-gray-100/70"
            @click="closeDesktopMenu"
          >
            <div
              class="flex size-10 shrink-0 items-center justify-center rounded-xl border border-gray-200/80 bg-gray-50 text-xl text-[#026662] transition-colors group-hover:bg-[#026662] group-hover:text-white"
            >
              <Icon icon="hugeicons:zap" />
            </div>
            <div>
              <p class="text-sm font-semibold text-gray-950 group-hover:text-[#026662]">
                The Deagensie Difference
              </p>
              <p class="mt-0.5 text-xs leading-relaxed text-gray-500">
                Strategy + Brand + Market + Technology + Talent integrated into one ecosystem.
              </p>
            </div>
          </NuxtLink>

          <NuxtLink
            to="/why"
            class="group flex items-start gap-3.5 rounded-2xl p-2.5 transition-colors hover:bg-gray-100/70"
            @click="closeDesktopMenu"
          >
            <div
              class="flex size-10 shrink-0 items-center justify-center rounded-xl border border-gray-200/80 bg-gray-50 text-xl text-[#026662] transition-colors group-hover:bg-[#026662] group-hover:text-white"
            >
              <Icon icon="hugeicons:rocket" />
            </div>
            <div>
              <p class="text-sm font-semibold text-gray-950 group-hover:text-[#026662]">
                Founders' Growth Lab
              </p>
              <p class="mt-0.5 text-xs leading-relaxed text-gray-500">
                Where early-stage startups and scaling companies become category leaders.
              </p>
            </div>
          </NuxtLink>

          <NuxtLink
            to="/why"
            class="group flex items-start gap-3.5 rounded-2xl p-2.5 transition-colors hover:bg-gray-100/70"
            @click="closeDesktopMenu"
          >
            <div
              class="flex size-10 shrink-0 items-center justify-center rounded-xl border border-gray-200/80 bg-gray-50 text-xl text-[#026662] transition-colors group-hover:bg-[#026662] group-hover:text-white"
            >
              <Icon icon="hugeicons:globe-02" />
            </div>
            <div>
              <p class="text-sm font-semibold text-gray-950 group-hover:text-[#026662]">
                African Excellence, Global Scale
              </p>
              <p class="mt-0.5 text-xs leading-relaxed text-gray-500">
                Building world-class brands from the continent competing on a global stage.
              </p>
            </div>
          </NuxtLink>
        </div>

        <div class="mt-4 border-t border-gray-100 pt-3">
          <NuxtLink
            to="/why"
            class="inline-flex items-center gap-2 text-xs font-semibold text-[#026662] hover:underline sm:text-sm"
            @click="closeDesktopMenu"
          >
            Discover the Deagensie Ecosystem
            <Icon icon="hugeicons:arrow-right-02" class="text-base" />
          </NuxtLink>
        </div>
      </div>

      <div
        class="relative flex w-[290px] shrink-0 flex-col justify-between overflow-hidden rounded-2xl border border-[#05DED5]/30 bg-[#E6FEFD] p-5 text-gray-950 lg:w-[310px] lg:p-6"
      >
        <div class="space-y-2">
          <p class="text-lg leading-tight font-bold lg:text-xl">See Our Brand Transformations</p>
          <NuxtLink
            to="/portfolio"
            class="inline-flex items-center gap-1.5 text-xs font-semibold text-[#04308F] hover:underline lg:text-sm"
            @click="closeDesktopMenu"
          >
            View Selected Work
            <Icon icon="hugeicons:arrow-right-02" class="text-base" />
          </NuxtLink>
        </div>
        <div class="mt-3 overflow-hidden rounded-xl border border-gray-200/80 bg-white p-1.5">
          <NuxtImg
            src="/images/pages/why/hero-2.png"
            class="aspect-16/10 w-full rounded-lg object-cover"
          />
        </div>
      </div>
    </div>

    <div
      v-else-if="activeDesktopMenu === 'about'"
      class="flex w-[860px] max-w-[calc(100vw-3rem)] gap-6 rounded-[inherit] p-6 lg:gap-8 lg:p-7"
    >
      <div class="flex flex-1 flex-col justify-between">
        <div class="space-y-2">
          <NuxtLink
            to="/about"
            class="group flex items-start gap-3.5 rounded-2xl p-2.5 transition-colors hover:bg-gray-100/70"
            @click="closeDesktopMenu"
          >
            <div
              class="flex size-10 shrink-0 items-center justify-center rounded-xl border border-gray-200/80 bg-gray-50 text-xl text-[#026662] transition-colors group-hover:bg-[#026662] group-hover:text-white"
            >
              <Icon icon="hugeicons:user-id-verification" />
            </div>
            <div>
              <p class="text-sm font-semibold text-gray-950 group-hover:text-[#026662]">
                Who We Are
              </p>
              <p class="mt-0.5 text-xs leading-relaxed text-gray-500">
                AI-led, ecosystem-driven growth and talent platform at the intersection of
                creativity and technology.
              </p>
            </div>
          </NuxtLink>

          <NuxtLink
            to="/portfolio"
            class="group flex items-start gap-3.5 rounded-2xl p-2.5 transition-colors hover:bg-gray-100/70"
            @click="closeDesktopMenu"
          >
            <div
              class="flex size-10 shrink-0 items-center justify-center rounded-xl border border-gray-200/80 bg-gray-50 text-xl text-[#026662] transition-colors group-hover:bg-[#026662] group-hover:text-white"
            >
              <Icon icon="hugeicons:briefcase-02" />
            </div>
            <div>
              <p class="text-sm font-semibold text-gray-950 group-hover:text-[#026662]">
                Our Portfolio
              </p>
              <p class="mt-0.5 text-xs leading-relaxed text-gray-500">
                Explore brand transformations, case studies and creative work we have delivered.
              </p>
            </div>
          </NuxtLink>

          <NuxtLink
            to="/contact"
            class="group flex items-start gap-3.5 rounded-2xl p-2.5 transition-colors hover:bg-gray-100/70"
            @click="closeDesktopMenu"
          >
            <div
              class="flex size-10 shrink-0 items-center justify-center rounded-xl border border-gray-200/80 bg-gray-50 text-xl text-[#026662] transition-colors group-hover:bg-[#026662] group-hover:text-white"
            >
              <Icon icon="hugeicons:mail-01" />
            </div>
            <div>
              <p class="text-sm font-semibold text-gray-950 group-hover:text-[#026662]">
                Contact Us
              </p>
              <p class="mt-0.5 text-xs leading-relaxed text-gray-500">
                Reach our team for partnerships, custom solutions or enterprise enquiries.
              </p>
            </div>
          </NuxtLink>
        </div>

        <div class="mt-4 border-t border-gray-100 pt-3">
          <NuxtLink
            to="/about"
            class="inline-flex items-center gap-2 text-xs font-semibold text-[#026662] hover:underline sm:text-sm"
            @click="closeDesktopMenu"
          >
            Learn about Deagensie
            <Icon icon="hugeicons:arrow-right-02" class="text-base" />
          </NuxtLink>
        </div>
      </div>

      <div
        class="relative flex w-[290px] shrink-0 flex-col justify-between overflow-hidden rounded-2xl border border-[#05DED5]/30 bg-[#E6FEFD] p-5 text-gray-950 lg:w-[310px] lg:p-6"
      >
        <div class="space-y-2">
          <p class="text-lg leading-tight font-bold lg:text-xl">
            Built on Integrity. Driven by Impact.
          </p>
          <NuxtLink
            to="https://app-deagensie-waitlist.vercel.app/"
            target="_blank"
            rel="noopener noreferrer"
            class="inline-flex items-center gap-1.5 text-xs font-semibold text-[#04308F] hover:underline lg:text-sm"
            @click="closeDesktopMenu"
          >
            Join the Ecosystem
            <Icon icon="hugeicons:arrow-right-02" class="text-base" />
          </NuxtLink>
        </div>
        <div class="mt-3 overflow-hidden rounded-xl border border-gray-200/80 bg-white p-1.5">
          <NuxtImg
            src="/images/pages/about/who-we-are.webp"
            class="aspect-16/10 w-full rounded-lg object-cover"
          />
        </div>
      </div>
    </div>

    <div
      v-else-if="activeDesktopMenu === 'subscription'"
      class="flex w-[860px] max-w-[calc(100vw-3rem)] gap-8 rounded-[inherit] p-6 lg:gap-10 lg:p-7"
    >
      <div class="w-[280px] shrink-0 space-y-4">
        <p class="text-xl leading-snug font-semibold">
          <NuxtLink to="/subscription" class="hover:underline" @click="closeDesktopMenu">
            Flexible Subscription Model
          </NuxtLink>
        </p>
        <p class="text-xs leading-relaxed text-gray-500">
          Access business solutions and creative talents on a flexible, project-based basis.
        </p>
      </div>
      <div class="flex flex-1 justify-between gap-6">
        <div class="space-y-4">
          <p class="text-sm leading-snug font-semibold tracking-wider text-gray-800 uppercase">
            Businesses
          </p>
          <ul
            class="space-y-3.5 **:[a]:inline-flex **:[a]:items-center **:[a]:gap-3 **:[a]:text-xs **:[a]:leading-relaxed sm:**:[a]:text-sm **:[svg]:text-base"
          >
            <li>
              <NuxtLink to="/subscription" class="hover:underline" @click="closeDesktopMenu">
                <Icon icon="hugeicons:arrow-right-01" />
                Growth-as-a-Service (GrowthOS)
              </NuxtLink>
            </li>
            <li>
              <NuxtLink to="/subscription" class="hover:underline" @click="closeDesktopMenu">
                <Icon icon="hugeicons:arrow-right-01" />
                Talent-as-a-Service
              </NuxtLink>
            </li>
          </ul>
        </div>
        <div class="space-y-4">
          <p class="text-sm leading-snug font-semibold tracking-wider text-gray-800 uppercase">
            Creatives
          </p>
          <ul
            class="space-y-3.5 **:[a]:inline-flex **:[a]:items-center **:[a]:gap-3 **:[a]:text-xs **:[a]:leading-relaxed sm:**:[a]:text-sm **:[svg]:text-base"
          >
            <li>
              <NuxtLink to="/creatives" class="hover:underline" @click="closeDesktopMenu">
                <Icon icon="hugeicons:arrow-right-01" />
                Creative Match
              </NuxtLink>
            </li>
            <li>
              <NuxtLink to="/creatives" class="hover:underline" @click="closeDesktopMenu">
                <Icon icon="hugeicons:arrow-right-01" />
                Gig Economy
              </NuxtLink>
            </li>
          </ul>
        </div>
      </div>
    </div>

    <div
      v-else-if="activeDesktopMenu === 'resource'"
      class="flex w-[860px] max-w-[calc(100vw-3rem)] gap-6 rounded-[inherit] p-6 lg:gap-8 lg:p-7"
    >
      <div class="flex flex-1 flex-col justify-between">
        <div class="space-y-2">
          <NuxtLink
            to="/blog"
            class="group flex items-start gap-3.5 rounded-2xl p-2.5 transition-colors hover:bg-gray-100/70"
            @click="closeDesktopMenu"
          >
            <div
              class="flex size-10 shrink-0 items-center justify-center rounded-xl border border-gray-200/80 bg-gray-50 text-xl text-[#026662] transition-colors group-hover:bg-[#026662] group-hover:text-white"
            >
              <Icon icon="hugeicons:quill-write-02" />
            </div>
            <div>
              <p class="text-sm font-semibold text-gray-950 group-hover:text-[#026662]">
                Blog & Insights
              </p>
              <p class="mt-0.5 text-xs leading-relaxed text-gray-500">
                Strategy deep-dives, growth lessons, and creative intelligence from our team.
              </p>
            </div>
          </NuxtLink>

          <NuxtLink
            to="/resource"
            class="group flex items-start gap-3.5 rounded-2xl p-2.5 transition-colors hover:bg-gray-100/70"
            @click="closeDesktopMenu"
          >
            <div
              class="flex size-10 shrink-0 items-center justify-center rounded-xl border border-gray-200/80 bg-gray-50 text-xl text-[#026662] transition-colors group-hover:bg-[#026662] group-hover:text-white"
            >
              <Icon icon="hugeicons:book-open-02" />
            </div>
            <div>
              <p class="text-sm font-semibold text-gray-950 group-hover:text-[#026662]">
                eBooks & Guides
              </p>
              <p class="mt-0.5 text-xs leading-relaxed text-gray-500">
                Downloadable playbooks for founders, marketers, and creative professionals.
              </p>
            </div>
          </NuxtLink>

          <NuxtLink
            to="/resource"
            class="group flex items-start gap-3.5 rounded-2xl p-2.5 transition-colors hover:bg-gray-100/70"
            @click="closeDesktopMenu"
          >
            <div
              class="flex size-10 shrink-0 items-center justify-center rounded-xl border border-gray-200/80 bg-gray-50 text-xl text-[#026662] transition-colors group-hover:bg-[#026662] group-hover:text-white"
            >
              <Icon icon="hugeicons:chart-bar-line" />
            </div>
            <div>
              <p class="text-sm font-semibold text-gray-950 group-hover:text-[#026662]">
                White Papers & Reports
              </p>
              <p class="mt-0.5 text-xs leading-relaxed text-gray-500">
                Data-backed research on African creative economy, talent trends, and market
                opportunities.
              </p>
            </div>
          </NuxtLink>
        </div>

        <div class="mt-4 border-t border-gray-100 pt-3">
          <NuxtLink
            to="/resource"
            class="inline-flex items-center gap-2 text-xs font-semibold text-[#026662] hover:underline sm:text-sm"
            @click="closeDesktopMenu"
          >
            Browse all resources
            <Icon icon="hugeicons:arrow-right-02" class="text-base" />
          </NuxtLink>
        </div>
      </div>

      <div
        class="relative flex w-[290px] shrink-0 flex-col justify-between overflow-hidden rounded-2xl border border-[#05DED5]/30 bg-[#E6FEFD] p-5 text-gray-950 lg:w-[310px] lg:p-6"
      >
        <div class="space-y-2">
          <p class="text-lg leading-tight font-bold lg:text-xl">Grow Smarter with Intelligence</p>
          <NuxtLink
            to="/blog"
            class="inline-flex items-center gap-1.5 text-xs font-semibold text-[#04308F] hover:underline lg:text-sm"
            @click="closeDesktopMenu"
          >
            Read Latest Insights
            <Icon icon="hugeicons:arrow-right-02" class="text-base" />
          </NuxtLink>
        </div>
        <div class="mt-3 overflow-hidden rounded-xl border border-gray-200/80 bg-white p-1.5">
          <NuxtImg
            src="/images/pages/why/hero-4.png"
            class="aspect-16/10 w-full rounded-lg object-cover"
          />
        </div>
      </div>
    </div>
  </div>
</template>

<style scoped lang="css">
@reference "../../assets/css/main.css";

.linedblock {
  @apply relative isolate px-2 py-1 before:absolute before:top-0 before:bottom-0 before:left-0 before:w-px before:bg-linear-to-b before:from-current before:from-15% before:to-current/12.5;
}
</style>
