<script setup lang="ts">
import { Icon } from '@iconify/vue';

definePageMeta({
  alias: ['/privacy-policy'],
});

const currentTopic = ref('all');

const topics = [
  { id: 'all', label: 'All Sections' },
  { id: 'collection', label: 'Data Collection' },
  { id: 'ai-engine', label: 'AI & Algorithmic Ethics' },
  { id: 'usage', label: 'Usage & Purposes' },
  { id: 'sharing', label: 'Sharing & Transfers' },
  { id: 'rights', label: 'Your Privacy Rights' },
  { id: 'security', label: 'Security & Retention' },
];

function scrollToSection(id: string) {
  currentTopic.value = id;
  if (id === 'all') {
    window.scrollTo({ top: 0, behavior: 'smooth' });
    return;
  }
  const el = document.getElementById(id);
  if (el) {
    el.scrollIntoView({ behavior: 'smooth', block: 'start' });
  }
}

// Interactive Data Subject Request helper
const requestType = ref('export');
const dpoEmail = 'privacy@deagensie.com';

const requestMailto = computed(() => {
  const subjects: Record<string, string> = {
    export: 'Data Subject Request: Personal Data Export',
    deletion: 'Data Subject Request: Right to Erasure / Account Deletion',
    rectification: 'Data Subject Request: Profile Data Rectification',
    optout: 'Privacy Request: Marketing Opt-Out',
  };
  const bodies: Record<string, string> = {
    export:
      'Hello Deagensie DPO Team,\n\nI would like to request a complete machine-readable copy of the personal data associated with my account.\n\nMy Account Email: \nFull Name: \nRole (Client Venture / Creative Talent): \n\nThank you.',
    deletion:
      'Hello Deagensie DPO Team,\n\nI would like to request the permanent erasure of my personal profile and associated data from the Deagensie platform in accordance with applicable privacy regulations.\n\nMy Account Email: \nFull Name: \nReason (optional): \n\nThank you.',
    rectification:
      'Hello Deagensie DPO Team,\n\nI noticed certain details in my profile or company records need correction. Please assist in updating the following:\n\nMy Account Email: \nDetails to update: \n\nThank you.',
    optout:
      'Hello Deagensie DPO Team,\n\nPlease remove my email address from all promotional marketing communications, research updates, and newsletters.\n\nEmail to opt-out: \n\nThank you.',
  };
  const sub = encodeURIComponent(subjects[requestType.value] || 'Data Subject Request');
  const body = encodeURIComponent(bodies[requestType.value] || '');
  return `mailto:${dpoEmail}?subject=${sub}&body=${body}`;
});
</script>

<template>
  <div class="min-h-screen bg-[#FDFDFE]">
    <!-- Editorial Hero Section matching Home & About Page style -->
    <section class="border-b border-gray-100 bg-white pt-28 pb-16 text-gray-900 lg:pt-36 lg:pb-24">
      <div class="mx-auto w-5/6 max-w-7xl">
        <div v-reveal="'fade-up'" class="mx-auto max-w-4xl space-y-6 text-center">
          <span
            class="inline-block rounded-full bg-[#04308F]/10 px-4 py-1.5 text-xs font-semibold tracking-widest text-[#04308F] uppercase"
          >
            Trust &amp; Governance
          </span>
          <h1
            class="font-serif text-3xl leading-tight font-normal tracking-tight text-gray-900 sm:text-4xl lg:text-6xl"
          >
            Your Data Protected. <br />
            <span class="text-[#04308F]">Your Trust Earned.</span>
          </h1>
          <p
            class="mx-auto max-w-3xl text-base leading-relaxed font-normal text-gray-500 sm:text-lg lg:text-xl"
          >
            A transparent breakdown of how Deagensie collects, safeguards, and ethically processes
            personal information across our Venture Growth Lab and Talent-as-a-Service ecosystem.
          </p>

          <!-- Key trust checkmark list matching homepage hero (0.vue) -->
          <div
            class="flex flex-wrap items-center justify-center gap-4 pt-2 text-xs font-semibold text-gray-700 sm:gap-8 sm:text-sm lg:text-base"
          >
            <div class="flex items-center gap-2">
              <Icon icon="lucide:check" class="text-lg font-bold text-[#05DED5]" />
              <span>Zero Data Selling</span>
            </div>
            <div class="flex items-center gap-2">
              <Icon icon="lucide:check" class="text-lg font-bold text-[#05DED5]" />
              <span>Merit-Based AI Matching</span>
            </div>
            <div class="flex items-center gap-2">
              <Icon icon="lucide:check" class="text-lg font-bold text-[#05DED5]" />
              <span>GDPR &amp; CCPA Compliant</span>
            </div>
            <div class="flex items-center gap-2">
              <Icon icon="lucide:check" class="text-lg font-bold text-[#05DED5]" />
              <span>AES-256 Bit Encryption</span>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- Metadata & Trust Bar -->
    <section class="border-b border-gray-100 bg-gray-50 py-6">
      <div
        class="mx-auto flex w-5/6 max-w-5xl flex-wrap items-center justify-center gap-6 text-xs text-gray-600 sm:justify-between sm:text-sm"
      >
        <div class="flex items-center gap-2">
          <Icon icon="solar:calendar-linear" class="text-base text-[#04308F]" />
          <span>Last Updated: <strong>October 13, 2026</strong></span>
        </div>
        <div class="flex items-center gap-2">
          <Icon icon="solar:shield-check-bold" class="text-base text-emerald-600" />
          <span>Version 2.4 &bull; Global Framework</span>
        </div>
        <div class="flex items-center gap-2">
          <Icon icon="solar:letter-bold" class="text-base text-[#04308F]" />
          <span
            >DPO:
            <a href="mailto:privacy@deagensie.com" class="font-medium text-[#04308F] underline"
              >privacy@deagensie.com</a
            ></span
          >
        </div>
      </div>
    </section>

    <!-- Quick Topic Navigation Pill Bar -->
    <div class="sticky top-20 z-30 border-b border-gray-200 bg-white/90 backdrop-blur-md">
      <div
        class="no-scrollbar mx-auto flex w-5/6 max-w-6xl items-center gap-2 overflow-x-auto py-3 text-xs"
      >
        <span class="mr-2 hidden font-bold tracking-wider text-gray-400 uppercase sm:inline"
          >Jump to:</span
        >
        <button
          v-for="t in topics"
          :key="t.id"
          type="button"
          :class="[
            'shrink-0 rounded-full px-3.5 py-1.5 font-semibold transition-all',
            currentTopic === t.id
              ? 'bg-[#04308F] text-white shadow-xs'
              : 'border border-gray-200 bg-gray-50 text-gray-600 hover:border-gray-300 hover:text-gray-900',
          ]"
          @click="scrollToSection(t.id)"
        >
          {{ t.label }}
        </button>
      </div>
    </div>

    <!-- Main Content Container -->
    <main class="mx-auto w-5/6 max-w-6xl space-y-12 py-12 lg:py-16">
      <!-- Section: Scope & Introduction -->
      <section class="space-y-4 rounded-3xl border border-gray-100 bg-white p-6 shadow-xs sm:p-10">
        <span class="text-xs font-bold tracking-widest text-[#04308F] uppercase"
          >01 / Scope & Purpose</span
        >
        <h2 class="font-serif text-2xl font-normal text-gray-900 sm:text-3xl">
          Introduction & Ecosystem Scope
        </h2>
        <p class="leading-relaxed text-gray-600">
          Deagensie Inc. (&ldquo;Deagensie&rdquo;, &ldquo;we&rdquo;, &ldquo;us&rdquo;) operates an
          integrated venture acceleration platform powering two symbiotic engines:
        </p>
        <div class="grid gap-4 pt-2 sm:grid-cols-2">
          <div class="rounded-2xl border border-blue-50 bg-blue-50/40 p-5">
            <h4 class="font-bold text-gray-900">1. Venture&rsquo;s Growth Lab</h4>
            <p class="mt-1 text-sm text-gray-600">
              Where startups and ventures transform into growth-ready powerhouses through strategic
              architecture, branding, growth marketing, and digital product engineering.
            </p>
          </div>
          <div class="rounded-2xl border border-teal-50 bg-teal-50/40 p-5">
            <h4 class="font-bold text-gray-900">2. Talent-as-a-Service (TaaS)</h4>
            <p class="mt-1 text-sm text-gray-600">
              An AI-powered matching network placing vetted global creative talent into venture
              projects on dedicated, fractional, or sprint-based models.
            </p>
          </div>
        </div>
        <p class="text-sm leading-relaxed text-gray-600">
          This Privacy Policy applies to all individuals and organizations interacting with our
          platform, including client founders, creative professionals, newsletter subscribers,
          waitlist applicants, and casual web visitors.
        </p>
      </section>

      <!-- Section: Data Collection -->
      <section
        id="collection"
        class="scroll-mt-36 space-y-6 rounded-3xl border border-gray-100 bg-white p-6 shadow-xs sm:p-10"
      >
        <span class="text-xs font-bold tracking-widest text-[#04308F] uppercase"
          >02 / Transparent Data Capture</span
        >
        <h2 class="font-serif text-2xl font-normal text-gray-900 sm:text-3xl">
          Information We Collect
        </h2>
        <p class="leading-relaxed text-gray-600">
          We categorize personal and corporate data into three distinct operational streams:
        </p>

        <div class="space-y-4">
          <div class="rounded-2xl border border-gray-100 bg-gray-50/70 p-5">
            <h4 class="flex items-center gap-2 font-bold text-gray-900">
              <Icon icon="solar:buildings-bold" class="text-[#04308F]" />
              A. Client Ventures & Founders
            </h4>
            <p class="mt-1 text-xs text-gray-500">
              Captured through inquiries, discovery meetings, and the Business Registration Flow.
            </p>
            <ul class="mt-3 list-disc space-y-1.5 pl-5 text-sm text-gray-600">
              <li>
                <strong>Organizational Profile:</strong> Company name, registered domain, industry
                sector, stage of venture funding, and headcount.
              </li>
              <li>
                <strong>Contact Information:</strong> Primary contact full name, work email address,
                telephone number, and title.
              </li>
              <li>
                <strong>Project Specifications:</strong> Brand guidelines, design briefs, technical
                product requirements, and allocated budget brackets.
              </li>
              <li>
                <strong>Billing & Invoicing:</strong> Tax IDs, invoicing addresses, and
                transactional records (card numbers are tokenized by PCI-DSS Level 1 certified
                gateways).
              </li>
            </ul>
          </div>

          <div class="rounded-2xl border border-gray-100 bg-gray-50/70 p-5">
            <h4 class="flex items-center gap-2 font-bold text-gray-900">
              <Icon icon="solar:palette-bold" class="text-[#04308F]" />
              B. Creative Talent & Professionals
            </h4>
            <p class="mt-1 text-xs text-gray-500">
              Captured through our Creative Registration Flow and talent vetting interviews.
            </p>
            <ul class="mt-3 list-disc space-y-1.5 pl-5 text-sm text-gray-600">
              <li>
                <strong>Professional Identity:</strong> Full legal name, professional alias, email,
                country of residence, and working timezone.
              </li>
              <li>
                <strong>Portfolio & Credentials:</strong> Verified work samples, GitHub / Behance /
                Dribbble / LinkedIn links, core discipline tags, and years of specialized
                experience.
              </li>
              <li>
                <strong>Availability & Compensation:</strong> Target monthly or hourly engagement
                rates, weekly bandwidth, and preferred venture formats.
              </li>
              <li>
                <strong>Verification Credentials:</strong> Government ID for AML/KYC identity
                confirmation and verified disbursement accounts.
              </li>
            </ul>
          </div>

          <div class="rounded-2xl border border-gray-100 bg-gray-50/70 p-5">
            <h4 class="flex items-center gap-2 font-bold text-gray-900">
              <Icon icon="solar:laptop-bold" class="text-[#04308F]" />
              C. Platform Telemetry & Browsing
            </h4>
            <p class="mt-1 text-xs text-gray-500">
              Automatically collected via our secure server infrastructure and Nuxt edge rendering.
            </p>
            <ul class="mt-3 list-disc space-y-1.5 pl-5 text-sm text-gray-600">
              <li>IP address and approximate regional geolocation.</li>
              <li>Browser User-Agent, operating system version, and display resolution.</li>
              <li>
                Local storage tokens ensuring form persistence across registration wizard stages.
              </li>
            </ul>
          </div>
        </div>
      </section>

      <!-- Section: AI Engine & Ethics -->
      <section
        id="ai-engine"
        class="scroll-mt-36 space-y-6 rounded-3xl border border-gray-100 bg-white p-6 shadow-xs sm:p-10"
      >
        <span class="text-xs font-bold tracking-widest text-[#04308F] uppercase"
          >03 / Algorithmic Transparency</span
        >
        <h2 class="font-serif text-2xl font-normal text-gray-900 sm:text-3xl">
          AI Matching Engine & Algorithmic Ethics
        </h2>
        <p class="leading-relaxed text-gray-600">
          Deagensie operates a proprietary <strong>Predictive AI Matching Engine</strong> to pair
          scaling ventures with world-class creative talent in hours rather than months. We adhere
          to rigorous ethical principles:
        </p>

        <div
          class="space-y-4 rounded-2xl border border-[#04308F]/20 bg-linear-to-br from-[#04308F]/5 to-transparent p-6"
        >
          <div class="flex items-center gap-3">
            <div
              class="flex size-10 items-center justify-center rounded-xl bg-[#04308F] text-white"
            >
              <Icon icon="solar:cpu-bold" class="text-xl" />
            </div>
            <div>
              <h4 class="font-bold text-gray-900">Strictly Non-Discriminatory Vectors</h4>
              <p class="text-xs text-gray-500">Merit-first algorithmic scoring architecture</p>
            </div>
          </div>
          <p class="text-sm leading-relaxed text-gray-700">
            Our algorithms evaluate match viability strictly using objective factors: verified skill
            competency, past deliverable velocity, portfolio stylistic alignment, language fluency,
            and timezone compatibility.
          </p>
          <div
            class="space-y-1 rounded-xl border border-gray-200 bg-white p-4 text-xs text-gray-600"
          >
            <p class="font-bold text-gray-900">Protected Attributes Strictly Excluded:</p>
            <p>
              Gender, race, ethnicity, age, religion, nationality, sexual orientation, marital
              status, and physical disability are strictly prevented from entering the scoring
              weights.
            </p>
          </div>
        </div>
      </section>

      <!-- Section: How We Use Data -->
      <section
        id="usage"
        class="scroll-mt-36 space-y-4 rounded-3xl border border-gray-100 bg-white p-6 shadow-xs sm:p-10"
      >
        <span class="text-xs font-bold tracking-widest text-[#04308F] uppercase"
          >04 / Lawful Processing</span
        >
        <h2 class="font-serif text-2xl font-normal text-gray-900 sm:text-3xl">
          How We Use Collected Data
        </h2>
        <div class="grid gap-4 pt-2 sm:grid-cols-2">
          <div class="space-y-2 rounded-2xl border border-gray-100 p-5">
            <div class="flex items-center gap-2 font-bold text-gray-900">
              <Icon icon="solar:check-circle-bold" class="text-[#04308F]" />
              <span>Project & Engagement Execution</span>
            </div>
            <p class="text-xs leading-relaxed text-gray-600">
              Scoping, delivering, and iterating on Growth Lab deliverables across strategy,
              branding, UI/UX, and web development.
            </p>
          </div>

          <div class="space-y-2 rounded-2xl border border-gray-100 p-5">
            <div class="flex items-center gap-2 font-bold text-gray-900">
              <Icon icon="solar:check-circle-bold" class="text-[#04308F]" />
              <span>Talent Placement & Onboarding</span>
            </div>
            <p class="text-xs leading-relaxed text-gray-600">
              Matching creative candidates to venture briefs and coordinating dedicated or
              fractional team onboarding.
            </p>
          </div>

          <div class="space-y-2 rounded-2xl border border-gray-100 p-5">
            <div class="flex items-center gap-2 font-bold text-gray-900">
              <Icon icon="solar:check-circle-bold" class="text-[#04308F]" />
              <span>Invoicing & Financial Compliance</span>
            </div>
            <p class="text-xs leading-relaxed text-gray-600">
              Processing subscription dues, issuing SOW milestone invoices, and disbursing payments
              to verified creative contractors.
            </p>
          </div>

          <div class="space-y-2 rounded-2xl border border-gray-100 p-5">
            <div class="flex items-center gap-2 font-bold text-gray-900">
              <Icon icon="solar:check-circle-bold" class="text-[#04308F]" />
              <span>Security & Threat Mitigation</span>
            </div>
            <p class="text-xs leading-relaxed text-gray-600">
              Monitoring platform endpoints, preventing CSRF attacks, and detecting bot activity or
              unauthorized scraping.
            </p>
          </div>
        </div>
      </section>

      <!-- Section: Sharing & Transfers -->
      <section
        id="sharing"
        class="scroll-mt-36 space-y-4 rounded-3xl border border-gray-100 bg-white p-6 shadow-xs sm:p-10"
      >
        <span class="text-xs font-bold tracking-widest text-[#04308F] uppercase"
          >05 / Data Disclosure</span
        >
        <h2 class="font-serif text-2xl font-normal text-gray-900 sm:text-3xl">
          Data Sharing & International Transfers
        </h2>
        <p class="leading-relaxed text-gray-600">
          Deagensie operates globally, uniting founders in major venture hubs with top creative
          minds worldwide.
        </p>
        <ul class="list-disc space-y-2 pl-5 text-sm text-gray-600">
          <li>
            <strong>Matched Participants:</strong> Project specifications are shared with
            shortlisted talent, and candidate profiles are shared with hiring ventures upon mutual
            engagement approval.
          </li>
          <li>
            <strong>Vetted Sub-processors:</strong> Cloud infrastructure (AWS, Cloudflare, Supabase,
            Stripe, Resend) bound by Data Processing Agreements (DPAs).
          </li>
          <li>
            <strong>Cross-Border Safeguards:</strong> All cross-border transfers utilize the
            European Commission&rsquo;s Standard Contractual Clauses (SCCs) and UK IDTA to guarantee
            equivalent legal safeguards.
          </li>
        </ul>
      </section>

      <!-- Section: Your Privacy Rights + Interactive Request Helper -->
      <section
        id="rights"
        class="scroll-mt-36 space-y-6 rounded-3xl border border-gray-100 bg-white p-6 shadow-xs sm:p-10"
      >
        <span class="text-xs font-bold tracking-widest text-[#04308F] uppercase"
          >06 / User Sovereignty</span
        >
        <h2 class="font-serif text-2xl font-normal text-gray-900 sm:text-3xl">
          Your Rights (GDPR & CCPA/CPRA)
        </h2>
        <p class="leading-relaxed text-gray-600">
          Under European, UK, and California privacy laws, you possess statutory rights over your
          personal data:
        </p>

        <div class="grid gap-3 text-xs text-gray-600 sm:grid-cols-2">
          <div class="rounded-xl border border-gray-100 bg-gray-50/50 p-4">
            <strong class="text-gray-900">Right of Access & Portability:</strong> Request a complete
            machine-readable copy of your profile and records.
          </div>
          <div class="rounded-xl border border-gray-100 bg-gray-50/50 p-4">
            <strong class="text-gray-900">Right to Erasure (&ldquo;Forget Me&rdquo;):</strong>
            Request complete deletion of your talent or venture account.
          </div>
          <div class="rounded-xl border border-gray-100 bg-gray-50/50 p-4">
            <strong class="text-gray-900">Right to Rectification:</strong> Update inaccurate or
            outdated skills, rates, or contact information.
          </div>
          <div class="rounded-xl border border-gray-100 bg-gray-50/50 p-4">
            <strong class="text-gray-900">Right to Object / Restrict:</strong> Halt marketing
            communications or algorithmic evaluation.
          </div>
        </div>

        <!-- Interactive Data Subject Request Generator -->
        <div
          class="space-y-4 rounded-2xl border border-[#04308F]/20 bg-linear-to-r from-blue-50/60 to-teal-50/60 p-6"
        >
          <div class="flex items-center gap-2 text-sm font-bold text-[#04308F]">
            <Icon icon="solar:letter-bold" class="text-lg" />
            <span>Submit a Data Subject Privacy Request</span>
          </div>
          <p class="text-xs text-gray-600">
            Select your request category below to prepare a formal legal inquiry directly to our
            Data Protection Officer:
          </p>
          <div class="flex flex-wrap items-center gap-2">
            <button
              v-for="opt in [
                { id: 'export', label: 'Export My Data' },
                { id: 'deletion', label: 'Delete My Profile' },
                { id: 'rectification', label: 'Update Info' },
                { id: 'optout', label: 'Opt-Out of Marketing' },
              ]"
              :key="opt.id"
              type="button"
              :class="[
                'rounded-full px-3.5 py-1.5 text-xs font-semibold transition-all',
                requestType === opt.id
                  ? 'bg-[#04308F] text-white shadow-xs'
                  : 'border border-gray-200 bg-white text-gray-600 hover:border-gray-300',
              ]"
              @click="requestType = opt.id"
            >
              {{ opt.label }}
            </button>
          </div>

          <div class="pt-2">
            <a
              :href="requestMailto"
              class="inline-flex items-center gap-2 rounded-full bg-[#04308F] px-5 py-2.5 text-xs font-bold text-white shadow-md shadow-[#04308F]/20 transition-all hover:bg-[#05DED5] hover:text-[#020B1E]"
            >
              <Icon icon="solar:outgoing-call-rounded-bold" />
              <span>Launch Pre-Filled Email to DPO &rarr;</span>
            </a>
          </div>
        </div>
      </section>

      <!-- Section: Security & Retention -->
      <section
        id="security"
        class="scroll-mt-36 space-y-4 rounded-3xl border border-gray-100 bg-white p-6 shadow-xs sm:p-10"
      >
        <span class="text-xs font-bold tracking-widest text-[#04308F] uppercase"
          >07 / Safeguards</span
        >
        <h2 class="font-serif text-2xl font-normal text-gray-900 sm:text-3xl">
          Security & Retention Schedule
        </h2>
        <p class="leading-relaxed text-gray-600">
          All client files, brief submissions, and talent credentials are protected with AES-256
          encryption at rest and TLS 1.3 in transit. Billing and accounting records are maintained
          for statutory periods (up to 7 years) to satisfy regulatory requirements, after which
          records are permanently expunged.
        </p>
      </section>

      <!-- Section: DPO Contact -->
      <section class="space-y-3 rounded-3xl border border-gray-200 bg-gray-50/80 p-6 sm:p-8">
        <h3 class="font-serif text-xl font-normal text-gray-900">Direct Compliance Inquiries</h3>
        <p class="text-sm text-gray-600">
          For formal privacy inquiries, Data Protection Addendums (DPAs), or regulatory audits:
        </p>
        <div class="space-y-1 pt-1 text-xs text-gray-700">
          <p><strong>Entity:</strong> Deagensie Inc. — Data Protection Office</p>
          <p>
            <strong>Email:</strong>
            <a href="mailto:privacy@deagensie.com" class="text-[#04308F] underline"
              >privacy@deagensie.com</a
            >
          </p>
          <p><strong>Response SLA:</strong> Within thirty (30) business days</p>
        </div>
      </section>
    </main>
  </div>
</template>
