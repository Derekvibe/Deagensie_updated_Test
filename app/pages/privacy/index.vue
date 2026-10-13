<script setup lang="ts">
import { Icon } from '@iconify/vue';

definePageMeta({
  alias: ['/privacy-policy'],
});

const sections = [
  { id: 'introduction', label: '1. Introduction & Ecosystem Scope' },
  { id: 'information-collected', label: '2. Information We Collect' },
  { id: 'ai-matching-engine', label: '3. AI Matching Engine & Ethics' },
  { id: 'how-we-use-data', label: '4. How We Use Collected Data' },
  { id: 'legal-bases', label: '5. Legal Bases for Processing' },
  { id: 'data-sharing', label: '6. Data Sharing & Third Parties' },
  { id: 'international-transfers', label: '7. International Data Transfers' },
  { id: 'data-security', label: '8. Data Security & Storage' },
  { id: 'data-retention', label: '9. Data Retention & Deletion' },
  { id: 'your-rights', label: '10. Your Rights & GDPR/CCPA' },
  { id: 'children-privacy', label: '11. Children’s Privacy' },
  { id: 'contact-dpo', label: '12. Contact & Data Protection Officer' },
];

const activeSection = ref('introduction');

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
      title="Privacy Policy"
      subtitle="How Deagensie collects, processes, and safeguards data for client ventures, creative talent, and platform visitors across our dual growth engines."
      active-page="privacy"
      last-updated="October 13, 2026"
      reading-time="9 min read"
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

            <!-- Quick Contact Callout in Sidebar -->
            <div class="rounded-2xl border border-blue-100 bg-blue-50/60 p-5 text-xs text-gray-700">
              <div class="mb-2 flex items-center gap-2 font-semibold text-[#04308F]">
                <Icon icon="solar:shield-check-bold" class="text-base" />
                <span>Privacy Inquiries</span>
              </div>
              <p class="leading-relaxed text-gray-600">
                Need to submit a data erasure request or inquire about our DPA?
              </p>
              <a
                href="mailto:privacy@deagensie.com"
                class="mt-3 inline-block font-semibold text-[#04308F] hover:underline"
              >
                privacy@deagensie.com &rarr;
              </a>
            </div>
          </div>
        </aside>

        <!-- Document Body -->
        <article class="prose-like space-y-12 text-gray-700">
          <!-- Key Takeaways Highlight Box -->
          <div class="rounded-3xl border border-emerald-100 bg-emerald-50/40 p-6 sm:p-8">
            <div class="mb-3 flex items-center gap-2.5">
              <div
                class="flex h-8 w-8 items-center justify-center rounded-full bg-emerald-600 text-white"
              >
                <Icon icon="solar:check-circle-bold" class="text-lg" />
              </div>
              <h3 class="font-serif text-lg font-bold text-gray-900">
                At a Glance: Our Privacy Commitments
              </h3>
            </div>
            <ul class="grid gap-3 pt-2 text-sm text-gray-700 sm:grid-cols-2">
              <li class="flex items-start gap-2.5">
                <Icon icon="solar:shield-check-linear" class="mt-0.5 shrink-0 text-emerald-600" />
                <span
                  ><strong>Zero Data Selling:</strong> We never sell, rent, or trade your personal
                  information.</span
                >
              </li>
              <li class="flex items-start gap-2.5">
                <Icon icon="solar:lock-password-linear" class="mt-0.5 shrink-0 text-emerald-600" />
                <span
                  ><strong>Enterprise Encryption:</strong> All data is encrypted in transit (TLS
                  1.3) and at rest (AES-256).</span
                >
              </li>
              <li class="flex items-start gap-2.5">
                <Icon icon="solar:cpu-linear" class="mt-0.5 shrink-0 text-emerald-600" />
                <span
                  ><strong>Merit-Based AI Matching:</strong> Our predictive engine uses skills and
                  credentials, never protected demographic attributes.</span
                >
              </li>
              <li class="flex items-start gap-2.5">
                <Icon icon="solar:user-check-linear" class="mt-0.5 shrink-0 text-emerald-600" />
                <span
                  ><strong>Complete User Rights:</strong> Full support for GDPR, UK GDPR, and CCPA
                  data access and deletion requests.</span
                >
              </li>
            </ul>
          </div>

          <!-- Section 1 -->
          <section id="introduction" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              1. Introduction & Ecosystem Scope
            </h2>
            <p class="leading-relaxed">
              Deagensie Inc. (&ldquo;Deagensie&rdquo;, &ldquo;we&rdquo;, &ldquo;our&rdquo;, or
              &ldquo;us&rdquo;) is an AI-led, ecosystem-driven platform designed to power venture
              growth and global creative careers. This Privacy Policy describes how we collect,
              store, utilize, disclose, and protect personal and organizational information through
              our website (including <code>deagensie.com</code> and related subdomains), our web
              applications, and our two primary growth engines:
            </p>
            <ul class="list-disc space-y-2 pl-6">
              <li>
                <strong>Venture&rsquo;s Growth Lab:</strong> Our business accelerator and execution
                arm providing strategy, branding, performance marketing, and digital engineering
                solutions to startups and scaling enterprises.
              </li>
              <li>
                <strong>Talent-as-a-Service (TaaS):</strong> Our predictive AI-powered talent
                matching engine connecting vetted global creative professionals with venture
                opportunities.
              </li>
            </ul>
            <p class="leading-relaxed">
              By accessing our platform, registering a venture or creative profile, submitting
              inquiries, or subscribing to our growth plans, you acknowledge the terms of this
              Privacy Policy.
            </p>
          </section>

          <!-- Section 2 -->
          <section id="information-collected" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              2. Information We Collect
            </h2>
            <p class="leading-relaxed">
              We gather information that identifies, relates to, describes, or is reasonably capable
              of being associated with you. The nature of data collected depends on your role within
              the Deagensie ecosystem:
            </p>

            <div class="space-y-4 pt-2">
              <div class="rounded-2xl border border-gray-100 bg-gray-50/60 p-5">
                <h4 class="font-bold text-gray-900">A. Client Ventures & Business Registrants</h4>
                <p class="mt-1 text-sm text-gray-600">
                  When you engage our Growth Lab, submit a project brief, or apply via the Business
                  Registration Flow (<code>/register/business</code>), we collect:
                </p>
                <ul class="mt-2 list-disc space-y-1 pl-5 text-sm text-gray-600">
                  <li>
                    Company details: Business legal name, industry, funding stage, website, and
                    company size.
                  </li>
                  <li>
                    Contact details: Primary contact full name, corporate email address, phone
                    number, and job title.
                  </li>
                  <li>
                    Project specifications: Growth objectives, target budgets, timelines, design
                    assets, and technical requirements.
                  </li>
                  <li>
                    Billing and invoicing details: Corporate address, tax identification numbers,
                    and transactional payment logs (processed via secure, PCI-DSS compliant
                    third-party gateways).
                  </li>
                </ul>
              </div>

              <div class="rounded-2xl border border-gray-100 bg-gray-50/60 p-5">
                <h4 class="font-bold text-gray-900">B. Creative Professionals & Talent Network</h4>
                <p class="mt-1 text-sm text-gray-600">
                  When applying to join our Talent-as-a-Service roster via the Creative Registration
                  Flow (<code>/register/creative</code>), we collect:
                </p>
                <ul class="mt-2 list-disc space-y-1 pl-5 text-sm text-gray-600">
                  <li>
                    Identity information: Full legal name, professional alias, email, telephone,
                    country of residence, and timezone.
                  </li>
                  <li>
                    Professional profile: Portfolio links, GitHub/Behance/Dribbble/LinkedIn
                    profiles, years of experience, core skill tags, software competencies, and case
                    studies.
                  </li>
                  <li>
                    Work preferences: Availability, preferred engagement models (freelance,
                    dedicated, fractional), target hourly/monthly compensation rates.
                  </li>
                  <li>
                    Verification & Payout data: Government ID for identity verification (where
                    legally required) and banking/disbursement account credentials.
                  </li>
                </ul>
              </div>

              <div class="rounded-2xl border border-gray-100 bg-gray-50/60 p-5">
                <h4 class="font-bold text-gray-900">C. Platform Visitors & Automatic Telemetry</h4>
                <p class="mt-1 text-sm text-gray-600">
                  Whenever you navigate the Deagensie website or waitlist, our systems automatically
                  log:
                </p>
                <ul class="mt-2 list-disc space-y-1 pl-5 text-sm text-gray-600">
                  <li>
                    Device and browser information (User-Agent, screen resolution, operating system,
                    preferred language).
                  </li>
                  <li>IP address and approximate geographic location (country/city level).</li>
                  <li>
                    Navigation telemetry: Page views, click interactions, scroll depth, session
                    duration, and referring URLs.
                  </li>
                  <li>
                    Form state persistence tokens (stored in browser local storage or IndexedDB to
                    prevent data loss during multi-step wizards).
                  </li>
                </ul>
              </div>
            </div>
          </section>

          <!-- Section 3 -->
          <section id="ai-matching-engine" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              3. AI Matching Engine & Algorithmic Ethics
            </h2>
            <p class="leading-relaxed">
              A foundational component of Deagensie is our proprietary
              <strong>Predictive AI Talent Matching Engine</strong>. We believe in total
              transparency regarding how algorithmic intelligence is utilized:
            </p>
            <div class="rounded-2xl border border-[#04308F]/20 bg-[#04308F]/5 p-5">
              <h4 class="font-bold text-[#04308F]">Algorithmic Processing Safeguards</h4>
              <ul class="mt-3 space-y-2 text-sm text-gray-700">
                <li class="flex items-start gap-2">
                  <Icon icon="solar:check-square-bold" class="mt-0.5 shrink-0 text-[#04308F]" />
                  <span
                    ><strong>Merit-Only Vectors:</strong> The matching engine evaluates verified
                    skills, portfolio similarity scores, historical project deliverables, language
                    fluency, and timezone overlap.</span
                  >
                </li>
                <li class="flex items-start gap-2">
                  <Icon icon="solar:check-square-bold" class="mt-0.5 shrink-0 text-[#04308F]" />
                  <span
                    ><strong>Anti-Bias Protection:</strong> Protected personal characteristics
                    (including gender, race, ethnicity, age, religion, sexual orientation, and
                    disability status) are strictly excluded from matching algorithms.</span
                  >
                </li>
                <li class="flex items-start gap-2">
                  <Icon icon="solar:check-square-bold" class="mt-0.5 shrink-0 text-[#04308F]" />
                  <span
                    ><strong>Human-in-the-Loop Oversight:</strong> Automated algorithmic scores
                    assist our curation teams but never trigger unilateral, fully autonomous
                    decisions regarding engagement termination or exclusion.</span
                  >
                </li>
              </ul>
            </div>
          </section>

          <!-- Section 4 -->
          <section id="how-we-use-data" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              4. How We Use Collected Data
            </h2>
            <p class="leading-relaxed">
              Deagensie uses the information we collect solely for defined, legitimate business
              purposes, including:
            </p>
            <ul class="list-disc space-y-2 pl-6">
              <li>
                <strong>Executing Venture Projects:</strong> Scoping, creating, and delivering
                branding, digital platforms, strategy roadmaps, and growth campaigns.
              </li>
              <li>
                <strong>Facilitating Talent Placements:</strong> Presenting anonymized or selected
                creative profiles to prospective client ventures for project matching.
              </li>
              <li>
                <strong>Managing Transactions:</strong> Generating invoices, processing subscription
                dues, and disbursing payments to talent.
              </li>
              <li>
                <strong>Enhancing Platform Performance:</strong> Analyzing user journeys, monitoring
                server health, and optimizing UI/UX responsiveness.
              </li>
              <li>
                <strong>Customer Support & Notices:</strong> Responding to inquiries submitted
                through our contact form (<code>/contact</code>) and transmitting transactional
                notifications.
              </li>
              <li>
                <strong>Fraud Prevention & Legal Compliance:</strong> Safeguarding against malicious
                activity, unauthorized credential sharing, and meeting tax record-keeping
                requirements.
              </li>
            </ul>
          </section>

          <!-- Section 5 -->
          <section id="legal-bases" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              5. Legal Bases for Processing (GDPR & Global Standards)
            </h2>
            <p class="leading-relaxed">
              If you reside within the European Economic Area (EEA), the United Kingdom, or
              Switzerland, our processing of your personal data relies on the following lawful bases
              under the General Data Protection Regulation (GDPR):
            </p>
            <div class="overflow-x-auto rounded-2xl border border-gray-100">
              <table class="w-full text-left text-xs sm:text-sm">
                <thead class="bg-gray-50 text-gray-900">
                  <tr>
                    <th class="p-3.5 font-bold">Legal Ground</th>
                    <th class="p-3.5 font-bold">Context / Use Case</th>
                  </tr>
                </thead>
                <tbody class="divide-y divide-gray-100">
                  <tr>
                    <td class="p-3.5 font-semibold text-gray-900">Contractual Necessity</td>
                    <td class="p-3.5 text-gray-600">
                      Onboarding clients, processing SOWs, placing talent, and distributing
                      contractual payments.
                    </td>
                  </tr>
                  <tr>
                    <td class="p-3.5 font-semibold text-gray-900">Legitimate Interests</td>
                    <td class="p-3.5 text-gray-600">
                      Improving predictive matching algorithms, securing network endpoints, and
                      debugging application errors.
                    </td>
                  </tr>
                  <tr>
                    <td class="p-3.5 font-semibold text-gray-900">Consent</td>
                    <td class="p-3.5 text-gray-600">
                      Sending opt-in marketing newsletters, promotional insights, and optional
                      analytical cookies.
                    </td>
                  </tr>
                  <tr>
                    <td class="p-3.5 font-semibold text-gray-900">Legal Obligation</td>
                    <td class="p-3.5 text-gray-600">
                      Retaining financial accounting books, tax declarations, and complying with
                      court subpoenas.
                    </td>
                  </tr>
                </tbody>
              </table>
            </div>
          </section>

          <!-- Section 6 -->
          <section id="data-sharing" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              6. Data Sharing & Third Parties
            </h2>
            <p class="leading-relaxed">
              We uphold strict confidentiality. We do not sell your personal data. We only share
              information under the following defined circumstances:
            </p>
            <ul class="list-disc space-y-2 pl-6">
              <li>
                <strong>Between Matched Clients and Talent:</strong> When a mutual interest is
                confirmed, client project specifications are shared with creative candidates, and
                talent profile credentials (resumes, portfolios, contact details) are made available
                to the hiring venture.
              </li>
              <li>
                <strong>Vetted Infrastructure Sub-processors:</strong> We engage best-in-class cloud
                providers (e.g., AWS, Supabase, Cloudflare, Stripe, Resend) bound by Data Processing
                Addendums (DPAs) requiring equivalent levels of security.
              </li>
              <li>
                <strong>Business Restructuring:</strong> In the event of a merger, acquisition, or
                sale of company assets, information may be transferred as part of the business
                assets subject to the same privacy commitments.
              </li>
              <li>
                <strong>Legal Compulsion:</strong> When required by enforceable judicial order,
                regulatory inquiry, or to protect the safety, rights, and property of Deagensie, our
                users, or the public.
              </li>
            </ul>
          </section>

          <!-- Section 7 -->
          <section id="international-transfers" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              7. International Data Transfers
            </h2>
            <p class="leading-relaxed">
              Deagensie operates globally, connecting client ventures in North America and Europe
              with top creative talent across Africa, Latin America, Europe, and Asia-Pacific.
              Consequently, personal data may be transferred to and processed in countries outside
              your jurisdiction of residence.
            </p>
            <p class="leading-relaxed">
              Where cross-border transfers occur, we implement appropriate legal transfer
              mechanisms, including the European Commission&rsquo;s
              <strong>Standard Contractual Clauses (SCCs)</strong> and the UK International Data
              Transfer Addendum, coupled with robust transport-layer and data-at-rest encryption.
            </p>
          </section>

          <!-- Section 8 -->
          <section id="data-security" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              8. Data Security & Storage Standards
            </h2>
            <p class="leading-relaxed">
              We employ comprehensive technical, physical, and organizational measures designed to
              protect information from loss, theft, misuse, unauthorized access, disclosure,
              alteration, and destruction:
            </p>
            <ul class="list-disc space-y-2 pl-6">
              <li>
                <strong>Transport Security:</strong> Strict HTTPS with modern TLS 1.3 protocol and
                HSTS headers enforced across all endpoints.
              </li>
              <li>
                <strong>Storage Encryption:</strong> Database records and uploaded client/talent
                assets are protected using AES-256 bit encryption at rest.
              </li>
              <li>
                <strong>Access Control:</strong> Strict Principle of Least Privilege (PoLP),
                role-based authentication, and mandatory Multi-Factor Authentication (MFA) for
                administrative systems.
              </li>
              <li>
                <strong>Audit Logging:</strong> Continuous monitoring of data access, automated
                threat detection, and vulnerability testing.
              </li>
            </ul>
          </section>

          <!-- Section 9 -->
          <section id="data-retention" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              9. Data Retention & Deletion
            </h2>
            <p class="leading-relaxed">
              We retain personal data only for as long as necessary to fulfill the purposes for
              which it was gathered, including satisfying legal, accounting, tax, or regulatory
              requirements.
            </p>
            <ul class="list-disc space-y-2 pl-6">
              <li>
                <strong>Active Account Profiles:</strong> Retained for the duration of your active
                standing with Deagensie.
              </li>
              <li>
                <strong>Transactional and Billing Records:</strong> Retained for up to seven (7)
                years to comply with statutory financial auditing obligations.
              </li>
              <li>
                <strong>Waitlist & Inquiries:</strong> Retained until service onboarding or until
                you request removal.
              </li>
            </ul>
            <p class="leading-relaxed">
              Upon receiving a valid request for erasure, we securely delete or irreversibly
              anonymize personal records within thirty (30) days, except where preservation is
              required by applicable law.
            </p>
          </section>

          <!-- Section 10 -->
          <section id="your-rights" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              10. Your Rights & Choices (GDPR & CCPA/CPRA)
            </h2>
            <p class="leading-relaxed">
              Depending on your jurisdiction, you may have specific statutory rights regarding your
              personal information:
            </p>

            <div class="grid gap-3 pt-2 sm:grid-cols-2">
              <div class="rounded-xl border border-gray-200 p-4">
                <h5 class="font-bold text-gray-900">Right of Access & Portability</h5>
                <p class="mt-1 text-xs text-gray-600">
                  Request a machine-readable copy of all personal records we maintain about you.
                </p>
              </div>
              <div class="rounded-xl border border-gray-200 p-4">
                <h5 class="font-bold text-gray-900">Right to Rectification</h5>
                <p class="mt-1 text-xs text-gray-600">
                  Correct incomplete or outdated professional, portfolio, or profile details.
                </p>
              </div>
              <div class="rounded-xl border border-gray-200 p-4">
                <h5 class="font-bold text-gray-900">
                  Right to Erasure (&ldquo;To Be Forgotten&rdquo;)
                </h5>
                <p class="mt-1 text-xs text-gray-600">
                  Request permanent deletion of your profile and submitted application data.
                </p>
              </div>
              <div class="rounded-xl border border-gray-200 p-4">
                <h5 class="font-bold text-gray-900">Right to Restrict or Object</h5>
                <p class="mt-1 text-xs text-gray-600">
                  Object to direct marketing or request limitation of algorithmic processing.
                </p>
              </div>
            </div>

            <p class="pt-2 leading-relaxed">
              To exercise any of these rights, email us at
              <a href="mailto:privacy@deagensie.com" class="font-semibold text-[#04308F] underline"
                >privacy@deagensie.com</a
              >
              with the subject line <em>&ldquo;Data Subject Rights Request&rdquo;</em>. We do not
              charge a fee and will respond within 30 days.
            </p>
          </section>

          <!-- Section 11 -->
          <section id="children-privacy" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              11. Children&rsquo;s Privacy
            </h2>
            <p class="leading-relaxed">
              Deagensie provides professional business accelerator and talent services intended
              exclusively for individuals aged eighteen (18) and older. We do not knowingly collect
              personal data from minors. If you believe a child under 18 has submitted data to
              Deagensie, please contact us immediately, and we will promptly purge the records.
            </p>
          </section>

          <!-- Section 12 -->
          <section id="contact-dpo" class="scroll-mt-32 space-y-4">
            <h2
              class="border-b border-gray-100 pb-3 font-serif text-2xl font-normal text-gray-900 sm:text-3xl"
            >
              12. Contact & Data Protection Officer
            </h2>
            <p class="leading-relaxed">
              For any questions, concerns, or requests regarding this Privacy Policy or our data
              protection protocols, please reach our Data Protection Officer and compliance team:
            </p>
            <div class="rounded-2xl border border-gray-100 bg-gray-50 p-6 text-sm text-gray-700">
              <p class="font-bold text-gray-900">
                Deagensie Inc. &mdash; Legal & Compliance Division
              </p>
              <p class="mt-1">Attention: Data Protection Officer</p>
              <p class="mt-1">
                Email:
                <a href="mailto:privacy@deagensie.com" class="text-[#04308F] underline"
                  >privacy@deagensie.com</a
                >
              </p>
              <p class="mt-1">
                General Inquiries:
                <a href="mailto:legal@deagensie.com" class="text-[#04308F] underline"
                  >legal@deagensie.com</a
                >
              </p>
              <p class="mt-1">
                Online Contact Form:
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
