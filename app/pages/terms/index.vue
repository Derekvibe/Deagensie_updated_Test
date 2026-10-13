<script setup lang="ts">
import { Icon } from '@iconify/vue';

definePageMeta({
  alias: ['/terms-of-service'],
});

const sections = [
  { id: 'agreement-eligibility', label: '1. Agreement & Eligibility' },
  { id: 'ecosystem-scope', label: '2. The Deagensie Dual Engines' },
  { id: 'user-accounts', label: '3. Accounts & Vetting' },
  { id: 'growth-lab-terms', label: '4. Growth Lab & SOW Engagements' },
  { id: 'subscriptions-billing', label: '5. Subscriptions & Payment Terms' },
  { id: 'taas-marketplace', label: '6. TaaS & Talent Placement Terms' },
  { id: 'non-circumvention', label: '7. Non-Circumvention & Conversion' },
  { id: 'intellectual-property', label: '8. Intellectual Property Rights' },
  { id: 'confidentiality-nda', label: '9. Mutual Confidentiality & NDAs' },
  { id: 'acceptable-use', label: '10. Acceptable Use & Conduct' },
  { id: 'disclaimers-liability', label: '11. Disclaimers & Liability Limits' },
  { id: 'indemnification', label: '12. Indemnification' },
  { id: 'termination', label: '13. Term & Termination' },
  { id: 'governing-law', label: '14. Dispute Resolution & Governing Law' },
  { id: 'modifications-contact', label: '15. Modifications & Inquiries' },
];

const activeSection = ref('agreement-eligibility');

onMounted(() => {
  const observer = new IntersectionObserver(
    (entries) => {
      for (const entry of entries) {
        if (entry.isIntersecting) {
          activeSection.value = entry.target.id;
          break;
        }
      }
    },
    {
      rootMargin: '-100px 0px -60% 0px',
      threshold: 0,
    }
  );

  for (const s of sections) {
    const el = document.getElementById(s.id);
    if (el) observer.observe(el);
  }

  onUnmounted(() => observer.disconnect());
});
</script>

<template>
  <div class="min-h-screen bg-white">
    <!-- Hero & Tabs -->
    <PagesLegalLegalHero
      title="Terms of Service"
      subtitle="Terms and conditions governing access to Deagensie's Venture Growth Lab, Talent-as-a-Service (TaaS) placements, subscriptions, and digital platforms."
      active-page="terms"
      last-updated="October 13, 2026"
      reading-time="11 min read"
    />

    <!-- Main Content Layout -->
    <div class="mx-auto w-5/6 max-w-7xl py-12 lg:py-16">
      <div class="grid grid-cols-1 gap-12 lg:grid-cols-[280px_1fr] lg:gap-16">
        <!-- Sidebar Navigation (Desktop Sticky) -->
        <aside class="hidden lg:block">
          <div class="sticky top-28 space-y-6">
            <div class="rounded-2xl border border-gray-100 bg-gray-50/80 p-5">
              <h3 class="mb-4 text-xs font-bold tracking-wider text-gray-900 uppercase">
                Contents
              </h3>
              <nav aria-label="Table of Contents" class="space-y-1">
                <a
                  v-for="item in sections"
                  :key="item.id"
                  :href="`#${item.id}`"
                  :class="[
                    'block rounded-lg px-3 py-2 text-xs font-medium transition-all duration-150',
                    activeSection === item.id
                      ? 'bg-[#04308F] font-semibold text-white shadow-xs'
                      : 'text-gray-600 hover:bg-gray-200/60 hover:text-gray-900',
                  ]"
                >
                  {{ item.label }}
                </a>
              </nav>
            </div>

            <!-- Sidebar Legal Note -->
            <div class="rounded-2xl border border-blue-100 bg-blue-50/60 p-5 text-xs text-gray-700">
              <div class="mb-2 flex items-center gap-2 font-semibold text-[#04308F]">
                <Icon icon="solar:document-text-bold" class="text-base" />
                <span>Enterprise MSAs</span>
              </div>
              <p class="leading-relaxed text-gray-600">
                Are you an enterprise venture requiring a custom Master Services Agreement?
              </p>
              <NuxtLink
                to="/contact"
                class="mt-3 inline-block font-semibold text-[#04308F] hover:underline"
              >
                Schedule Legal Discussion &rarr;
              </NuxtLink>
            </div>
          </div>
        </aside>

        <!-- Document Body -->
        <article class="prose-like space-y-12 text-gray-700">
          <!-- Key Takeaways Highlight Box -->
          <div class="rounded-3xl border border-blue-100 bg-blue-50/40 p-6 sm:p-8">
            <div class="mb-3 flex items-center gap-2.5">
              <div
                class="flex h-8 w-8 items-center justify-center rounded-full bg-[#04308F] text-white"
              >
                <Icon icon="solar:scale-bold" class="text-lg" />
              </div>
              <h3 class="font-serif text-lg font-bold text-gray-900">Key Terms Summary</h3>
            </div>
            <ul class="grid gap-3 pt-2 text-sm text-gray-700 sm:grid-cols-2">
              <li class="flex items-start gap-2.5">
                <Icon icon="solar:check-circle-bold" class="mt-0.5 shrink-0 text-[#04308F]" />
                <span
                  ><strong>Deliverable Ownership:</strong> Clients gain complete IP ownership over
                  final deliverables upon full invoice payment.</span
                >
              </li>
              <li class="flex items-start gap-2.5">
                <Icon icon="solar:check-circle-bold" class="mt-0.5 shrink-0 text-[#04308F]" />
                <span
                  ><strong>Contractor Relationship:</strong> Creative professionals in our TaaS
                  network operate as independent contractors, not employees.</span
                >
              </li>
              <li class="flex items-start gap-2.5">
                <Icon icon="solar:check-circle-bold" class="mt-0.5 shrink-0 text-[#04308F]" />
                <span
                  ><strong>Non-Circumvention:</strong> Clients and matched talent agree not to
                  bypass Deagensie for direct unmediated contracts without a buyout fee.</span
                >
              </li>
              <li class="flex items-start gap-2.5">
                <Icon icon="solar:check-circle-bold" class="mt-0.5 shrink-0 text-[#04308F]" />
                <span
                  ><strong>Built-In Confidentiality:</strong> Proprietary client strategies, source
                  code, and brand secrets are shielded under mutual NDA terms.</span
                >
              </li>
            </ul>
          </div>

          <!-- Section 1 -->
          <section id="agreement-eligibility" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              1. Agreement to Terms & Eligibility
            </h2>
            <p class="leading-relaxed">
              These Terms of Service (&ldquo;Terms&rdquo;) constitute a legally binding agreement
              between you (&ldquo;User&rdquo;, &ldquo;Client&rdquo;, &ldquo;Creative&rdquo;, or
              &ldquo;You&rdquo;) and Deagensie Inc. (&ldquo;Deagensie&rdquo;, &ldquo;Company&rdquo;,
              &ldquo;we&rdquo;, &ldquo;our&rdquo;, or &ldquo;us&rdquo;). These Terms govern your
              access to and use of Deagensie's website, web applications, project management
              portals, subscription services, and related offerings.
            </p>
            <p class="leading-relaxed">
              By accessing our website, creating an account, registering as a business or creative,
              or executing a Statement of Work, you represent and warrant that:
            </p>
            <ul class="list-disc space-y-2 pl-6">
              <li>
                You are at least eighteen (18) years of age and possess full legal capacity to enter
                into binding agreements.
              </li>
              <li>
                If you represent a corporate entity or organization, you hold the requisite
                corporate power and authorization to bind that entity to these Terms.
              </li>
              <li>
                All information provided during onboarding is accurate, current, and complete.
              </li>
            </ul>
          </section>

          <!-- Section 2 -->
          <section id="ecosystem-scope" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              2. The Deagensie Dual Engines
            </h2>
            <p class="leading-relaxed">
              Deagensie operates through two distinct, synergistic engines designed to scale modern
              businesses:
            </p>
            <div class="grid gap-4 pt-2 sm:grid-cols-2">
              <div class="rounded-2xl border border-gray-100 bg-gray-50/70 p-5">
                <h4 class="flex items-center gap-2 font-bold text-gray-900">
                  <Icon icon="solar:rocket-bold" class="text-[#04308F]" />
                  Engine 1: Venture&rsquo;s Growth Lab
                </h4>
                <p class="mt-2 text-sm text-gray-600">
                  Full-stack venture execution across 01 Strategy (market analysis, growth
                  architecture), 02 Branding (identity, visual language), 03 Marketing (performance
                  campaigns, funnels), and 04 Digital Platforms (web apps, product design,
                  engineering). Engagements are delivered via bespoke Statements of Work (SOW) or
                  Growth Subscriptions.
                </p>
              </div>
              <div class="rounded-2xl border border-gray-100 bg-gray-50/70 p-5">
                <h4 class="flex items-center gap-2 font-bold text-gray-900">
                  <Icon icon="solar:cpu-bold" class="text-[#05DED5]" />
                  Engine 2: Talent-as-a-Service (TaaS)
                </h4>
                <p class="mt-2 text-sm text-gray-600">
                  A predictive AI-matched talent network placing vetted global creative
                  professionals (designers, engineers, copywriters, creative directors) into
                  fast-scaling ventures on dedicated, fractional, or sprint-based models.
                </p>
              </div>
            </div>
          </section>

          <!-- Section 3 -->
          <section id="user-accounts" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              3. User Accounts & Vetting Process
            </h2>
            <p class="leading-relaxed">
              Certain features require registration via our dedicated flows (<code
                >/register/business</code
              >
              or <code>/register/creative</code>) or joining the early access waitlist
              (<code>/waitlist</code>).
            </p>
            <ul class="list-disc space-y-2 pl-6">
              <li>
                <strong>Account Security:</strong> You are responsible for safeguarding your
                credentials and for all activities occurring under your account. You must notify
                Deagensie immediately of any unauthorized access.
              </li>
              <li>
                <strong>Vetting Standards:</strong> Acceptance into our creative talent network is
                discretionary and subject to portfolio review, skills verification, identity
                confirmation, and professional references. Deagensie reserves the right to decline
                or suspend any application that fails to meet quality benchmarks.
              </li>
              <li>
                <strong>Accurate Representation:</strong> Creative talent must accurately represent
                their past project contributions, technical proficiencies, and geographical
                residency. Misrepresentation constitutes material breach and causes immediate
                expulsion.
              </li>
            </ul>
          </section>

          <!-- Section 4 -->
          <section id="growth-lab-terms" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              4. Growth Lab Engagements & Statements of Work
            </h2>
            <p class="leading-relaxed">
              When a Client engages the Venture Growth Lab for project-based initiatives, the
              specific deliverables, milestones, pricing, and schedules are governed by an executed
              Statement of Work (&ldquo;SOW&rdquo;) or digital service agreement:
            </p>
            <ul class="list-disc space-y-2 pl-6">
              <li>
                <strong>Scope of Deliverables:</strong> Deagensie will perform the strategic,
                design, branding, and technical services outlined in the applicable SOW in
                accordance with high industry standards.
              </li>
              <li>
                <strong>Client Cooperation:</strong> Timely project completion requires prompt
                Client feedback, asset handovers, and milestone sign-offs. Delays in Client
                approvals will automatically extend project schedules.
              </li>
              <li>
                <strong>Review & Acceptance:</strong> Clients have five (5) business days following
                deliverable submission to review and submit revision requests within the agreed SOW
                scope. In the absence of written feedback within this period, deliverables are
                deemed accepted.
              </li>
            </ul>
          </section>

          <!-- Section 5 -->
          <section id="subscriptions-billing" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              5. Growth Subscriptions & Payment Terms
            </h2>
            <p class="leading-relaxed">
              Deagensie offers Growth Subscriptions (<code>/subscription</code>) providing dedicated
              monthly creative bandwidth and ongoing venture support:
            </p>
            <ul class="list-disc space-y-2 pl-6">
              <li>
                <strong>Billing Cycle:</strong> Subscriptions are billed in advance on a recurring
                monthly or quarterly cycle via credit card, wire transfer, or authorized automated
                payment gateway.
              </li>
              <li>
                <strong>Auto-Renewal:</strong> Subscriptions renew automatically unless cancelled in
                writing at least fourteen (14) days prior to the start of the next billing cycle.
              </li>
              <li>
                <strong>Pause & Cancellation:</strong> Clients in good standing may pause their
                subscription bandwidth for up to thirty (30) days per calendar year with advance
                notice.
              </li>
              <li>
                <strong>Taxes:</strong> All quoted prices are exclusive of federal, state, local, or
                value-added taxes (VAT/GST), which are the sole responsibility of the Client.
              </li>
              <li>
                <strong>No Refunds for Delivered Sprints:</strong> Because creative bandwidth and
                strategic resources are allocated upon subscription commencement, payments for
                active or past sprint cycles are non-refundable.
              </li>
            </ul>
          </section>

          <!-- Section 6 -->
          <section id="taas-marketplace" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              6. Talent-as-a-Service (TaaS) & Placement Terms
            </h2>
            <p class="leading-relaxed">
              The following terms govern engagements facilitated through our Talent-as-a-Service
              (<code>/creatives</code>) engine:
            </p>
            <div class="space-y-3 rounded-2xl border border-gray-100 bg-gray-50/70 p-5">
              <h4 class="font-bold text-gray-900">Independent Contractor Classification</h4>
              <p class="text-sm text-gray-600">
                Creative professionals placed through Deagensie operate strictly as independent
                contractors. Nothing in these Terms shall be construed as creating an
                employer-employee, agency, partnership, or joint venture relationship between
                Deagensie and talent, or between Client and talent, unless an explicit formal
                Employer of Record (EOR) addendum is executed.
              </p>
              <h4 class="pt-2 font-bold text-gray-900">Talent Quality Guarantee</h4>
              <p class="text-sm text-gray-600">
                If a Client notifies Deagensie within the first seven (7) business days of an
                embedded placement that the matched creative does not meet the specified skill
                benchmarks, Deagensie will provide a replacement candidate at no additional matching
                charge, or credit the unused placement hours.
              </p>
            </div>
          </section>

          <!-- Section 7 -->
          <section id="non-circumvention" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              7. Non-Circumvention & Direct Hiring Restrictions
            </h2>
            <p class="leading-relaxed">
              Deagensie invests substantial capital, algorithmic engineering, and vetting resources
              to discover, evaluate, and present top global creative talent to client ventures:
            </p>
            <div class="rounded-2xl border border-amber-200 bg-amber-50/50 p-5">
              <div class="flex items-center gap-2 font-bold text-amber-900">
                <Icon icon="solar:shield-warning-bold" class="text-lg" />
                <span>Non-Circumvention Covenant</span>
              </div>
              <p class="mt-2 text-sm leading-relaxed text-amber-950">
                During the term of any engagement and for a period of twelve (12) months following
                the introduction of a creative professional or completion of an engagement, Clients
                agree not to solicit, recruit, employ, or contract directly with that talent outside
                of the Deagensie platform without Deagensie&rsquo;s prior written consent.
              </p>
              <p class="mt-2 text-sm leading-relaxed text-amber-950">
                If a Client desires to convert a Deagensie creative into a direct full-time employee
                or direct independent contractor, the Client must pay Deagensie a
                <strong>Talent Conversion Fee</strong> equal to twenty percent (20%) of the
                professional&rsquo;s first-year annualized compensation or agreed enterprise buyout
                fee.
              </p>
            </div>
          </section>

          <!-- Section 8 -->
          <section id="intellectual-property" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              8. Intellectual Property Rights & Deliverable Handover
            </h2>
            <p class="leading-relaxed">
              We maintain crystal-clear boundaries regarding intellectual property ownership:
            </p>
            <ul class="list-disc space-y-2 pl-6">
              <li>
                <strong>Client Deliverables (Work Made for Hire):</strong> Upon complete payment of
                all applicable fees and invoices, all right, title, and interest in bespoke
                deliverables produced specifically for Client (including custom brand logos,
                typography systems, marketing copy, UI design assets, and custom source code) shall
                vest exclusively in the Client.
              </li>
              <li>
                <strong>Deagensie Pre-Existing IP:</strong> Deagensie retains full ownership of its
                proprietary tools, algorithmic models, predictive AI matching software, reusable UI
                frameworks, and methodologies (&ldquo;Company Pre-Existing IP&rdquo;). Clients
                receive a perpetual, non-exclusive, royalty-free license to use any Company
                Pre-Existing IP embedded within deliverables.
              </li>
              <li>
                <strong>Portfolio Display Rights:</strong> Unless protected by a strict, pre-signed
                Non-Disclosure Agreement (NDA), Deagensie and participating creative talent retain
                the reasonable right to showcase delivered work, client logos, and non-confidential
                case studies in marketing materials and portfolio presentations (as seen on
                <code>/portfolio</code>).
              </li>
            </ul>
          </section>

          <!-- Section 9 -->
          <section id="confidentiality-nda" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              9. Mutual Confidentiality & NDAs
            </h2>
            <p class="leading-relaxed">
              Both parties agree that any proprietary information disclosed during registrations,
              discovery calls, SOW execution, or platform messaging marked as confidential (or which
              by its nature should reasonably be understood to be confidential) shall be held in
              strict confidence.
            </p>
            <p class="leading-relaxed">
              Confidential information includes business strategies, investor pitch decks,
              unreleased product features, customer lists, financial data, and technical
              specifications. Neither party shall disclose confidential information to any third
              party without prior written consent, except to employees, subcontractors, and legal
              counsel bound by equivalent confidentiality covenants.
            </p>
          </section>

          <!-- Section 10 -->
          <section id="acceptable-use" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              10. Acceptable Use & Prohibited Conduct
            </h2>
            <p class="leading-relaxed">
              You agree to utilize Deagensie solely for lawful, professional purposes. You shall
              not:
            </p>
            <ul class="list-disc space-y-2 pl-6">
              <li>
                Reverse engineer, decompile, or extract the source code or AI matching algorithms of
                the Deagensie platform.
              </li>
              <li>
                Deploy automated bots, scrapers, or crawlers to extract platform listings, creative
                portfolios, or pricing frameworks.
              </li>
              <li>
                Submit false, plagiarized, infringing, defamatory, or unlawful materials in
                registration profiles or project briefs.
              </li>
              <li>
                Circumvent or manipulate payment mechanisms, invoicing structures, or fee
                obligations.
              </li>
              <li>
                Engage in harassment, discrimination, or abusive conduct toward talent, clients, or
                Deagensie staff.
              </li>
            </ul>
          </section>

          <!-- Section 11 -->
          <section id="disclaimers-liability" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              11. Disclaimers & Limitation of Liability
            </h2>
            <div class="space-y-3 rounded-2xl border border-gray-200 bg-gray-50/70 p-5 text-sm">
              <p class="text-xs font-bold tracking-wider text-gray-900 uppercase">
                A. Warranty Disclaimer
              </p>
              <p class="leading-relaxed text-gray-600">
                EXCEPT AS EXPRESSLY SET FORTH IN AN EXECUTED STATEMENT OF WORK, THE DEAGENSIE
                PLATFORM AND SERVICES ARE PROVIDED &ldquo;AS IS&rdquo; AND &ldquo;AS
                AVAILABLE&rdquo; WITHOUT WARRANTIES OF ANY KIND, EXPRESS OR IMPLIED. WHILE WE STRIVE
                FOR UNMATCHED EXCELLENCE, WE DO NOT GUARANTEE THAT SPECIFIC BRANDING, MARKETING
                CAMPAIGNS, OR PLATFORM BUILDS WILL YIELD SPECIFIC REVENUE, CAPITAL RAISING, OR USER
                ACQUISITION OUTCOMES.
              </p>
              <p class="pt-2 text-xs font-bold tracking-wider text-gray-900 uppercase">
                B. Liability Limitation
              </p>
              <p class="leading-relaxed text-gray-600">
                TO THE MAXIMUM EXTENT PERMITTED BY LAW, IN NO EVENT SHALL DEAGENSIE, ITS DIRECTORS,
                EMPLOYEES, OR AGENTS BE LIABLE FOR ANY INDIRECT, INCIDENTAL, SPECIAL, CONSEQUENTIAL,
                OR PUNITIVE DAMAGES (INCLUDING LOSS OF PROFITS, DATA, GOODWILL, OR BUSINESS
                INTERRUPTION) ARISING FROM OR RELATED TO THESE TERMS. DEAGENSIE&rsquo;S TOTAL
                AGGREGATE LIABILITY UNDER THESE TERMS SHALL BE CAPPED AT THE FEES ACTUALLY PAID BY
                CLIENT TO DEAGENSIE DURING THE SIX (6) MONTHS PRECEDING THE CLAIM.
              </p>
            </div>
          </section>

          <!-- Section 12 -->
          <section id="indemnification" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              12. Indemnification
            </h2>
            <p class="leading-relaxed">
              You agree to defend, indemnify, and hold harmless Deagensie, its affiliates, officers,
              directors, and contractors from and against any third-party claims, liabilities,
              damages, losses, and reasonable legal fees arising out of or related to: (a) your
              breach of these Terms; (b) any materials or content provided by you that infringe upon
              third-party intellectual property or privacy rights; or (c) your willful misconduct or
              violation of applicable laws.
            </p>
          </section>

          <!-- Section 13 -->
          <section id="termination" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              13. Term & Termination
            </h2>
            <p class="leading-relaxed">
              These Terms remain in full force while you access our website or maintain an active
              account. Either party may terminate an engagement for cause if the other party
              materially breaches these Terms and fails to cure such breach within fourteen (14)
              days of written notice.
            </p>
            <p class="leading-relaxed">
              Upon termination, Client shall pay for all completed work and approved hours incurred
              up to the effective termination date. Provisions concerning IP ownership of paid
              deliverables, non-circumvention, confidentiality, liability limits, and dispute
              resolution shall survive termination.
            </p>
          </section>

          <!-- Section 14 -->
          <section id="governing-law" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              14. Dispute Resolution, Arbitration & Governing Law
            </h2>
            <p class="leading-relaxed">
              These Terms shall be governed by and construed in accordance with the laws of the
              State of Delaware, United States, without regard to conflict of law principles.
            </p>
            <ul class="list-disc space-y-2 pl-6">
              <li>
                <strong>Informal Negotiation:</strong> In the event of any controversy or dispute,
                the parties agree to first attempt in good faith to resolve the matter amicably
                through executive negotiations for at least thirty (30) days.
              </li>
              <li>
                <strong>Binding Arbitration:</strong> Any dispute unresolved through negotiations
                shall be resolved through confidential binding arbitration administered by the
                American Arbitration Association (AAA) under its Commercial Arbitration Rules.
              </li>
              <li>
                <strong>Class Action Waiver:</strong> All proceedings shall be conducted on an
                individual basis. You and Deagensie agree to waive any right to bring or participate
                in any class action or representative proceeding.
              </li>
            </ul>
          </section>

          <!-- Section 15 -->
          <section id="modifications-contact" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              15. Modifications & Legal Inquiries
            </h2>
            <p class="leading-relaxed">
              Deagensie reserves the right to amend these Terms periodically. We will provide notice
              of material updates by posting the revised version on this page with an updated
              &ldquo;Effective Date&rdquo; or via direct email communication. Continued
              participation in the ecosystem following modifications constitutes acceptance of the
              revised Terms.
            </p>
            <div class="rounded-2xl border border-gray-100 bg-gray-50 p-6 text-sm text-gray-700">
              <p class="font-bold text-gray-900">
                Deagensie Inc. &mdash; Legal & Governance Department
              </p>
              <p class="mt-1">
                Inquiries & Formal Legal Notices:
                <a href="mailto:legal@deagensie.com" class="text-[#04308F] underline"
                  >legal@deagensie.com</a
                >
              </p>
              <p class="mt-1">
                Contract Questions:
                <a href="mailto:contracts@deagensie.com" class="text-[#04308F] underline"
                  >contracts@deagensie.com</a
                >
              </p>
              <p class="mt-1">
                Direct Discovery Call:
                <NuxtLink to="/contact" class="text-[#04308F] underline"
                  >deagensie.com/contact</NuxtLink
                >
              </p>
            </div>
          </section>
        </article>
      </div>
    </div>

    <!-- Bottom CTA -->
    <PagesLegalLegalCta />
  </div>
</template>
