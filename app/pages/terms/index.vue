<script setup lang="ts">
import { Icon } from '@iconify/vue';

definePageMeta({
  alias: ['/terms-of-service'],
});

const articles = [
  { id: 'art-1', num: 'Article I', title: 'Acceptance, Authority & Capacity' },
  { id: 'art-2', num: 'Article II', title: 'The Deagensie Dual Engines' },
  { id: 'art-3', num: 'Article III', title: 'Accounts & Talent Vetting' },
  { id: 'art-4', num: 'Article IV', title: 'Growth Lab SOWs & Delivery' },
  { id: 'art-5', num: 'Article V', title: 'Subscriptions & Billing Terms' },
  { id: 'art-6', num: 'Article VI', title: 'TaaS Independent Contractor Rules' },
  { id: 'art-7', num: 'Article VII', title: 'Non-Circumvention & Conversion' },
  { id: 'art-8', num: 'Article VIII', title: 'Intellectual Property Ownership' },
  { id: 'art-9', num: 'Article IX', title: 'Mutual NDAs & Confidentiality' },
  { id: 'art-10', num: 'Article X', title: 'Acceptable Platform Conduct' },
  { id: 'art-11', num: 'Article XI', title: 'Disclaimers & Liability Limits' },
  { id: 'art-12', num: 'Article XII', title: 'Indemnification' },
  { id: 'art-13', num: 'Article XIII', title: 'Term & Termination' },
  { id: 'art-14', num: 'Article XIV', title: 'Governing Law & Arbitration' },
  { id: 'art-15', num: 'Article XV', title: 'Amendments & Legal Notices' },
];

const selectedArticle = ref('art-1');

function scrollToArticle(id: string) {
  selectedArticle.value = id;
  const el = document.getElementById(id);
  if (el) {
    el.scrollIntoView({ behavior: 'smooth', block: 'start' });
  }
}
</script>

<template>
  <div class="min-h-screen bg-[#FAFAFC]">
    <!-- Formal Legal Agreement Hero (Distinct from Privacy and Cookies) -->
    <header class="border-b border-gray-200 bg-white pt-28 pb-14 lg:pt-36 lg:pb-20">
      <div class="mx-auto w-5/6 max-w-6xl space-y-6">
        <!-- Breadcrumbs -->
        <div
          class="flex items-center gap-2 text-xs font-semibold tracking-widest text-gray-400 uppercase"
        >
          <NuxtLink to="/" class="transition-colors hover:text-gray-900">Home</NuxtLink>
          <span>/</span>
          <span class="text-[#04308F]">Master Agreement</span>
        </div>

        <div class="max-w-3xl space-y-4">
          <div
            class="inline-flex items-center gap-2 rounded-full bg-[#04308F]/10 px-3.5 py-1 text-xs font-semibold tracking-wider text-[#04308F] uppercase"
          >
            <Icon icon="solar:scale-bold" class="text-base" />
            <span>Binding Legal Contract</span>
          </div>

          <h1
            class="font-serif text-3xl font-normal tracking-tight text-gray-900 sm:text-4xl lg:text-5xl"
          >
            Deagensie Terms of Service
          </h1>

          <p class="text-base leading-relaxed text-gray-600 sm:text-lg">
            The master contractual agreement governing all venture engagements, Growth
            Subscriptions, and Talent-as-a-Service partnerships between Deagensie Inc., Client
            Ventures, and Creative Professionals.
          </p>
        </div>

        <!-- Contract Specification Strip -->
        <div
          class="flex flex-wrap items-center gap-4 border-t border-gray-100 pt-6 text-xs text-gray-500 sm:text-sm"
        >
          <div class="flex items-center gap-1.5">
            <Icon icon="solar:document-text-bold" class="text-[#04308F]" />
            <span>Contract Version: <strong>2026.2</strong></span>
          </div>
          <span>&bull;</span>
          <div class="flex items-center gap-1.5">
            <Icon icon="solar:calendar-linear" class="text-[#04308F]" />
            <span>Effective Date: <strong>October 13, 2026</strong></span>
          </div>
          <span>&bull;</span>
          <div class="flex items-center gap-1.5">
            <Icon icon="solar:global-linear" class="text-[#04308F]" />
            <span>Governing Law: <strong>State of Delaware, USA</strong></span>
          </div>
          <span>&bull;</span>
          <div class="flex items-center gap-1.5">
            <Icon icon="solar:shield-check-bold" class="text-emerald-600" />
            <span>Dispute Forum: <strong>Binding AAA Arbitration</strong></span>
          </div>
        </div>
      </div>
    </header>

    <!-- Key Terms Executive Summary for Founders & Creatives -->
    <section class="border-b border-gray-200 bg-gray-50/70 py-10">
      <div class="mx-auto w-5/6 max-w-6xl space-y-6">
        <h3 class="text-xs font-bold tracking-widest text-gray-500 uppercase">
          Contract Highlights at a Glance
        </h3>

        <div class="grid gap-6 md:grid-cols-3">
          <div class="space-y-3 rounded-2xl border border-gray-200 bg-white p-6 shadow-xs">
            <div
              class="flex size-10 items-center justify-center rounded-xl bg-[#04308F]/10 text-[#04308F]"
            >
              <Icon icon="solar:buildings-bold" class="text-xl" />
            </div>
            <h4 class="font-bold text-gray-900">For Client Ventures</h4>
            <ul class="space-y-2 text-xs text-gray-600">
              <li>
                &bull; <strong>Full IP Transfer:</strong> Complete deliverable ownership transfers
                upon invoice settlement.
              </li>
              <li>
                &bull; <strong>7-Day Placement Guarantee:</strong> Free replacement candidate if
                talent does not match benchmark.
              </li>
              <li>
                &bull; <strong>Mutual Confidentiality:</strong> Proprietary roadmap and code
                protected under built-in NDA.
              </li>
            </ul>
          </div>

          <div class="space-y-3 rounded-2xl border border-gray-200 bg-white p-6 shadow-xs">
            <div
              class="flex size-10 items-center justify-center rounded-xl bg-teal-50 text-teal-700"
            >
              <Icon icon="solar:user-bold" class="text-xl" />
            </div>
            <h4 class="font-bold text-gray-900">For Creative Talent</h4>
            <ul class="space-y-2 text-xs text-gray-600">
              <li>
                &bull; <strong>Independent Contractor:</strong> Flexible, autonomous professional
                classification.
              </li>
              <li>
                &bull; <strong>Guaranteed Disbursement:</strong> Prompt milestone payouts via secure
                channels.
              </li>
              <li>
                &bull; <strong>Portfolio Rights:</strong> Reasonable display rights for delivered
                case studies (unless barred by NDA).
              </li>
            </ul>
          </div>

          <div class="space-y-3 rounded-2xl border border-gray-200 bg-white p-6 shadow-xs">
            <div
              class="flex size-10 items-center justify-center rounded-xl bg-amber-50 text-amber-700"
            >
              <Icon icon="solar:shield-warning-bold" class="text-xl" />
            </div>
            <h4 class="font-bold text-gray-900">Platform Protections</h4>
            <ul class="space-y-2 text-xs text-gray-600">
              <li>
                &bull; <strong>Non-Circumvention:</strong> 12-month direct hire restriction outside
                Deagensie.
              </li>
              <li>
                &bull; <strong>Conversion Fee:</strong> Standard 20% annualized fee for converting
                talent into full-time staff.
              </li>
              <li>
                &bull; <strong>Anti-Scraping:</strong> Reverse engineering or bot extraction
                strictly prohibited.
              </li>
            </ul>
          </div>
        </div>
      </div>
    </section>

    <!-- Main Contract Layout: Sticky Article Index + Articles Column -->
    <div class="mx-auto w-5/6 max-w-6xl py-12 lg:py-16">
      <div class="grid grid-cols-1 gap-10 lg:grid-cols-[280px_1fr] lg:gap-14">
        <!-- Sticky Left Index -->
        <aside class="hidden lg:block">
          <div
            class="sticky top-28 space-y-4 rounded-2xl border border-gray-200 bg-white p-5 shadow-xs"
          >
            <h4 class="text-xs font-bold tracking-wider text-gray-900 uppercase">
              Articles of Agreement
            </h4>
            <nav class="space-y-1">
              <button
                v-for="art in articles"
                :key="art.id"
                type="button"
                :class="[
                  'block w-full rounded-lg px-2.5 py-1.5 text-left text-xs transition-colors',
                  selectedArticle === art.id
                    ? 'bg-[#04308F] font-semibold text-white'
                    : 'text-gray-600 hover:bg-gray-100 hover:text-gray-900',
                ]"
                @click="scrollToArticle(art.id)"
              >
                <span class="block font-mono text-[10px] opacity-75">{{ art.num }}</span>
                <span>{{ art.title }}</span>
              </button>
            </nav>
          </div>
        </aside>

        <!-- Articles Legal Text -->
        <div class="space-y-10 text-sm leading-relaxed text-gray-700">
          <!-- Article 1 -->
          <article
            id="art-1"
            class="scroll-mt-32 space-y-3 rounded-2xl border border-gray-200 bg-white p-6 shadow-xs sm:p-8"
          >
            <span class="font-mono text-xs font-bold text-[#04308F] uppercase">Article I</span>
            <h3 class="font-serif text-xl font-normal text-gray-900">
              Acceptance of Terms, Authority & Capacity
            </h3>
            <p>
              By accessing the Deagensie website (including <code>deagensie.com</code>), executing a
              Statement of Work (&ldquo;SOW&rdquo;), registering via
              <code>/register/business</code> or <code>/register/creative</code>, or subscribing to
              a growth plan, you agree to be bound by these Terms of Service.
            </p>
            <p>
              You represent and warrant that: (a) you are at least eighteen (18) years of age; (b)
              you possess legal authority to bind yourself or the corporate entity you represent;
              and (c) your use of our platform complies with all applicable local, national, and
              international laws.
            </p>
          </article>

          <!-- Article 2 -->
          <article
            id="art-2"
            class="scroll-mt-32 space-y-3 rounded-2xl border border-gray-200 bg-white p-6 shadow-xs sm:p-8"
          >
            <span class="font-mono text-xs font-bold text-[#04308F] uppercase">Article II</span>
            <h3 class="font-serif text-xl font-normal text-gray-900">The Deagensie Dual Engines</h3>
            <p>
              Deagensie delivers venture acceleration services through two integrated mechanisms:
            </p>
            <ul class="list-disc space-y-1 pl-5 text-gray-600">
              <li>
                <strong>Venture's Growth Lab:</strong> Execution across Strategy, Branding, Growth
                Marketing, and Digital Product Engineering on a project or subscription basis.
              </li>
              <li>
                <strong>Talent-as-a-Service (TaaS):</strong> AI-assisted placement engine matching
                vetted global creative professionals with ventures for sprint or embedded bandwidth.
              </li>
            </ul>
          </article>

          <!-- Article 3 -->
          <article
            id="art-3"
            class="scroll-mt-32 space-y-3 rounded-2xl border border-gray-200 bg-white p-6 shadow-xs sm:p-8"
          >
            <span class="font-mono text-xs font-bold text-[#04308F] uppercase">Article III</span>
            <h3 class="font-serif text-xl font-normal text-gray-900">
              Accounts, Onboarding & Talent Vetting
            </h3>
            <p>
              Users must provide accurate, current, and verifiable information during onboarding.
              Acceptance into our TaaS network is discretionary, subject to portfolio reviews,
              technical benchmarks, and background confirmations. Deagensie reserves the right to
              suspend any account submitting falsified credentials.
            </p>
          </article>

          <!-- Article 4 -->
          <article
            id="art-4"
            class="scroll-mt-32 space-y-3 rounded-2xl border border-gray-200 bg-white p-6 shadow-xs sm:p-8"
          >
            <span class="font-mono text-xs font-bold text-[#04308F] uppercase">Article IV</span>
            <h3 class="font-serif text-xl font-normal text-gray-900">
              Growth Lab SOWs & Delivery Milestone Review
            </h3>
            <p>
              Project engagements are governed by bespoke Statements of Work detailing deliverables,
              timelines, and milestones. Clients have five (5) business days upon deliverable
              submission to review and submit change requests within the agreed SOW scope. In the
              absence of written rejection, deliverables are deemed accepted.
            </p>
          </article>

          <!-- Article 5 -->
          <article
            id="art-5"
            class="scroll-mt-32 space-y-3 rounded-2xl border border-gray-200 bg-white p-6 shadow-xs sm:p-8"
          >
            <span class="font-mono text-xs font-bold text-[#04308F] uppercase">Article V</span>
            <h3 class="font-serif text-xl font-normal text-gray-900">
              Growth Subscriptions & Billing Terms
            </h3>
            <p>
              Subscriptions (<code>/subscription</code>) are billed in advance on recurring monthly
              or quarterly cycles. Subscriptions renew automatically unless cancelled in writing at
              least fourteen (14) days prior to renewal. Delivered sprint bandwidth is
              non-refundable.
            </p>
          </article>

          <!-- Article 6 -->
          <article
            id="art-6"
            class="scroll-mt-32 space-y-3 rounded-2xl border border-gray-200 bg-white p-6 shadow-xs sm:p-8"
          >
            <span class="font-mono text-xs font-bold text-[#04308F] uppercase">Article VI</span>
            <h3 class="font-serif text-xl font-normal text-gray-900">
              TaaS Independent Contractor Rules
            </h3>
            <p>
              Creative professionals placed through Deagensie operate strictly as independent
              contractors. Neither talent nor Client shall represent the relationship as
              employer-employee, agency, or partnership unless governed by a dedicated Employer of
              Record (EOR) addendum.
            </p>
          </article>

          <!-- Article 7 -->
          <article
            id="art-7"
            class="scroll-mt-32 space-y-3 rounded-2xl border border-amber-200 bg-amber-50/40 p-6 shadow-xs sm:p-8"
          >
            <span class="font-mono text-xs font-bold text-amber-800 uppercase">Article VII</span>
            <h3 class="font-serif text-xl font-normal text-amber-950">
              Non-Circumvention & Talent Conversion Covenant
            </h3>
            <p class="text-amber-950">
              Clients agree not to bypass Deagensie by contracting directly with introduced talent
              for twelve (12) months following introduction or project completion.
            </p>
            <p class="font-semibold text-amber-950">
              To convert a Deagensie creative into a direct full-time employee or direct contractor,
              Client must pay Deagensie a Talent Conversion Fee equal to twenty percent (20%) of the
              annualized compensation or negotiated buyout fee.
            </p>
          </article>

          <!-- Article 8 -->
          <article
            id="art-8"
            class="scroll-mt-32 space-y-3 rounded-2xl border border-gray-200 bg-white p-6 shadow-xs sm:p-8"
          >
            <span class="font-mono text-xs font-bold text-[#04308F] uppercase">Article VIII</span>
            <h3 class="font-serif text-xl font-normal text-gray-900">
              Intellectual Property Ownership & Handover
            </h3>
            <p>
              Upon complete payment of all applicable fees, all right, title, and interest in
              bespoke final deliverables (custom design, logos, marketing copy, and software code)
              produced specifically for Client shall transfer exclusively to Client as &ldquo;work
              made for hire&rdquo;.
            </p>
            <p>
              Deagensie retains proprietary rights to its underlying AI models, frameworks, and
              pre-existing code libraries.
            </p>
          </article>

          <!-- Article 9 -->
          <article
            id="art-9"
            class="scroll-mt-32 space-y-3 rounded-2xl border border-gray-200 bg-white p-6 shadow-xs sm:p-8"
          >
            <span class="font-mono text-xs font-bold text-[#04308F] uppercase">Article IX</span>
            <h3 class="font-serif text-xl font-normal text-gray-900">
              Mutual Non-Disclosure & Confidentiality
            </h3>
            <p>
              Both parties agree to hold all proprietary business plans, code, investor decks, and
              customer data in strict confidence. Neither party shall disclose confidential
              materials to third parties without prior authorization.
            </p>
          </article>

          <!-- Article 10 -->
          <article
            id="art-10"
            class="scroll-mt-32 space-y-3 rounded-2xl border border-gray-200 bg-white p-6 shadow-xs sm:p-8"
          >
            <span class="font-mono text-xs font-bold text-[#04308F] uppercase">Article X</span>
            <h3 class="font-serif text-xl font-normal text-gray-900">
              Acceptable Platform Conduct & Prohibited Acts
            </h3>
            <p>
              Users shall not decompile or reverse engineer the AI matching engine, deploy scraping
              bots, upload infringing materials, harass ecosystem participants, or attempt fee
              evasion.
            </p>
          </article>

          <!-- Article 11 -->
          <article
            id="art-11"
            class="scroll-mt-32 space-y-3 rounded-2xl border border-gray-200 bg-white p-6 shadow-xs sm:p-8"
          >
            <span class="font-mono text-xs font-bold text-[#04308F] uppercase">Article XI</span>
            <h3 class="font-serif text-xl font-normal text-gray-900">
              Disclaimers & Limitation of Liability
            </h3>
            <p class="text-xs font-bold text-gray-500 uppercase">Standard Commercial Limitation</p>
            <p class="text-xs leading-relaxed text-gray-600">
              TO THE MAXIMUM EXTENT PERMITTED BY LAW, DEAGENSIE’S TOTAL AGGREGATE LIABILITY ARISING
              OUT OF OR RELATING TO THESE TERMS SHALL BE CAPPED AT THE FEES ACTUALLY PAID BY CLIENT
              TO DEAGENSIE DURING THE SIX (6) MONTHS PRECEDING THE CLAIM.
            </p>
          </article>

          <!-- Article 12, 13, 14, 15 -->
          <article
            id="art-12"
            class="scroll-mt-32 space-y-3 rounded-2xl border border-gray-200 bg-white p-6 shadow-xs sm:p-8"
          >
            <span class="font-mono text-xs font-bold text-[#04308F] uppercase"
              >Article XII &bull; XIII &bull; XIV &bull; XV</span
            >
            <h3 class="font-serif text-xl font-normal text-gray-900">
              Indemnification, Governing Law & Binding Arbitration
            </h3>
            <p>
              These Terms are governed by the laws of the State of Delaware, United States. Any
              disputes unresolved through informal negotiations shall be settled through
              confidential, binding arbitration administered by the American Arbitration Association
              (AAA). Both parties waive the right to participate in class action litigation.
            </p>
            <div class="border-t border-gray-100 pt-4 text-xs text-gray-600">
              <p>
                <strong>Formal Legal Notices:</strong>
                <a href="mailto:legal@deagensie.com" class="text-[#04308F] underline"
                  >legal@deagensie.com</a
                >
              </p>
              <p><strong>Physical Inquiries:</strong> Deagensie Inc., Legal Affairs Division</p>
            </div>
          </article>
        </div>
      </div>
    </div>
  </div>
</template>
