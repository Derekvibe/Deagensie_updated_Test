<script setup lang="ts">
import { Icon } from '@iconify/vue';
import { push } from 'notivue';

interface ArticleItem {
  id: string;
  category:
    'Press releases' | 'Media coverage' | 'Analyst reports' | 'Company news' | 'Product releases';
  title: string;
  description: string;
  source?: string;
  sourceLogo?: string;
  date: string;
  isoDate?: string;
  readTime: string;
  image: string;
  featured?: boolean;
  externalUrl?: string;
  fullContent: string;
  keyPoints?: string[];
}

// -------------------------------------------------------------
// Articles Dataset (Patterned on Andela Newsroom & Media Coverage)
// -------------------------------------------------------------
const heroFeaturedArticle: ArticleItem = {
  id: 'hero-openai-partner',
  category: 'Press releases',
  title: 'Deagensie named an AI Creative Innovation Partner',
  description:
    'Recognized for pioneering predictive AI talent matching and human-in-the-loop creative squad workflows for scaling global ventures and enterprise digital platforms.',
  date: 'Sep 9, 2026',
  isoDate: '2026-09-09',
  readTime: '3 min',
  image: '/images/pages/about/hero-2.png',
  featured: true,
  fullContent:
    'Deagensie today announced its designation as an AI Creative Innovation Partner, solidifying its position at the forefront of AI-enabled design, engineering, and venture growth systems. Through this strategic alignment, Deagensie expands its proprietary matching algorithms and accelerates squad deployment for fast-scaling global brands.',
  keyPoints: [
    'Expands human-in-the-loop agentic workflows across 12 creative and tech disciplines.',
    'Provides vetted enterprise teams with guaranteed 72-hour talent onboarding.',
    'Sets new industry benchmarks for combining predictive intelligence with high-fidelity creative output.',
  ],
};

const topThreeFeatured: ArticleItem[] = [
  {
    id: 'top-1-emerging-skills',
    category: 'Press releases',
    title:
      'Deagensie research finds that 53% of AI job postings seek skills that don’t match job title; also identifies new emerging tech roles',
    description:
      'Our bi-annual global analysis reveals substantial misalignment between traditional job descriptions and actual project demands, creating massive friction in modern hiring.',
    date: 'Sep 10, 2026',
    readTime: '3 min',
    image: '/images/pages/about/who-we-are.webp',
    fullContent:
      'A study conducted across 45,000 enterprise tech and creative postings found that more than half demand hybrid competencies absent from traditional titles. Deagensie’s Talent-as-a-Service model addresses this by cataloging verified competencies rather than arbitrary seniority labels.',
    keyPoints: [
      'Over 53% of job specifications request emerging agentic capabilities that no traditional degree certifies.',
      'Elastic squads reduce project ramp-up delays by an average of 68%.',
      'Identifies 7 new hybrid creative-technologist roles leading enterprise adoption in 2026.',
    ],
  },
  {
    id: 'top-2-it-brew',
    category: 'Media coverage',
    source: 'IT Brew',
    title: 'The tech industry is inventing roles faster than companies can name them',
    description:
      'From AI orchestrators to synthetic brand directors, corporate titles are scrambling to keep pace with rapid workflow automation.',
    date: 'Sep 17, 2026',
    readTime: '3 min',
    image: '/images/pages/(home)/hero.webp',
    fullContent:
      'IT Brew spoke with Deagensie leadership about the unbundling of traditional agency departments. As cross-disciplinary squads replace siloed design and development silos, agile businesses are turning to on-demand talent platforms to stay competitive.',
    keyPoints: [
      'Why traditional rigid hiring pipelines are collapsing under rapid technological shifts.',
      'How on-demand squad orchestration eliminates hiring overhead for early and growth-stage ventures.',
    ],
  },
  {
    id: 'top-3-whistic',
    category: 'Company news',
    source: 'Deagensie & Anthropic',
    title:
      'How Whistic is building an AI-powered risk operations platform with Deagensie & Anthropic',
    description:
      'By integrating agentic workflows and specialized engineering talent, Whistic accelerated product release cycles by 4x without sacrificing safety.',
    date: 'Sep 30, 2026',
    readTime: '7 min',
    image: '/images/pages/why/hero.webp',
    fullContent:
      'Case study examining how cloud security leader Whistic embedded high-velocity Deagensie engineering squads alongside Anthropic model infrastructure to pioneer real-time risk assessment tooling.',
    keyPoints: [
      'Reduced audit cycle timelines from 3 weeks to under 48 hours.',
      'Implemented robust human-oversight verification layers for all automated customer assessments.',
    ],
  },
];

const categoryArticles: ArticleItem[] = [
  {
    id: 'cat-1-stackoverflow',
    category: 'Media coverage',
    source: 'Stack Overflow',
    title:
      'Your next job doesn’t have a title yet: Emerging role skills Q&A with Corey Hymel of Deagensie',
    description:
      'In-depth conversation exploring how agent-first development environments are redefining creative engineering careers.',
    date: 'Oct 14, 2026',
    readTime: '8 min',
    image: '/images/pages/blog/hero.webp',
    fullContent:
      'Speaking with Stack Overflow’s editorial team, Deagensie’s head of talent strategy explained why versatility, architectural judgment, and prompt synthesis now outweigh single-language syntax expertise in top-tier teams.',
  },
  {
    id: 'cat-2-nexford',
    category: 'Company news',
    title: 'How Nexford University is building an AI-native university with Deagensie & Anthropic',
    description:
      'Transforming higher education curricula into adaptive, real-time learning modules using generative systems.',
    date: 'Oct 1, 2026',
    readTime: '8 min',
    image: '/images/pages/about/who-we-are.webp',
    fullContent:
      'Nexford partnered with Deagensie Growth Lab to design, build, and deploy an adaptive learning ecosystem serving thousands of international students across 110 countries.',
  },
  {
    id: 'cat-3-location-live',
    category: 'Company news',
    title:
      'How Location Live is using Claude to speed up development and keep its marketplace innovating',
    description:
      'Case study on how distributed creative squads delivered an AI-assisted marketplace search engine ahead of schedule.',
    date: 'Oct 1, 2026',
    readTime: '6 min',
    image: '/images/pages/about/hero-2.png',
    fullContent:
      'Location Live cut venue recommendation response times by 82% while tripling user engagement through bespoke natural language query parsing developed by Deagensie talent squads.',
  },
  {
    id: 'cat-4-atlantic-council',
    category: 'Analyst reports',
    source: 'Atlantic Council',
    title: 'Technology and the global south: A US strategy for competitiveness',
    description:
      'Comprehensive policy research detailing why borderless talent mobility and distributed African tech hubs are essential to global economic health.',
    date: 'Sep 30, 2026',
    readTime: '15 min',
    image: '/images/pages/why/hero.webp',
    fullContent:
      'A deep dive report co-authored with policy researchers examining how borderless talent platforms such as Deagensie bridge international venture capital with world-class emerging-market technical talent.',
  },
  {
    id: 'cat-5-whistic-comp',
    category: 'Company news',
    title:
      'How Whistic is building an AI-powered risk operations platform with Deagensie & Anthropic',
    description:
      'Operational blueprint for enterprise risk management teams scaling through hybrid AI squads.',
    date: 'Sep 30, 2026',
    readTime: '7 min',
    image: '/images/pages/(home)/hero.webp',
    fullContent:
      'Detailed architectural breakdown of the security validation pipelines created to handle multi-tenant vendor risk scoring using specialized agentic models.',
  },
  {
    id: 'cat-6-eci',
    category: 'Analyst reports',
    source: 'ECI Research',
    title: 'Why job titles are failing enterprise tech hiring | ECI Research',
    description:
      'Data-driven white paper highlighting the $42B cost of misdirected talent searches and the shift toward skills-based verification.',
    date: 'Sep 29, 2026',
    readTime: '2 min',
    image: '/images/pages/about/hero.webp',
    fullContent:
      'ECI Research outlines how competency-graph matching outperforms traditional keyword resume screening by 4.3x in predictive 12-month retention rates.',
  },
  {
    id: 'cat-7-althea',
    category: 'Company news',
    title: 'How Althea is building an AI-native engineering model with Deagensie & Anthropic',
    description:
      'Scaling decentralized telecom infrastructure with high-velocity product squads deployed across three continents.',
    date: 'Sep 25, 2026',
    readTime: '6 min',
    image: '/images/pages/about/who-we-are.webp',
    fullContent:
      'Althea Telecom shares the operational playbooks developed with Deagensie to coordinate asynchronous engineering sprints across multiple time zones without documentation decay.',
  },
  {
    id: 'cat-8-silicon-republic',
    category: 'Media coverage',
    source: 'Silicon Republic',
    title: 'Global research highlights growing AI and job fears among undergraduates',
    description:
      'New findings reveal where students feel prepared—and where academic curricula are failing to equip future innovators.',
    date: 'Sep 18, 2026',
    readTime: '3 min',
    image: '/images/pages/why/hero.webp',
    fullContent:
      'Silicon Republic covers Deagensie’s international university survey, spotlighting student demand for apprenticeship-style project learning and direct exposure to real-world venture tools.',
  },
  {
    id: 'cat-9-channel-dive',
    category: 'Media coverage',
    source: 'Channel Dive',
    title: 'AI makes a mess of the tech job market: Navigating the new hybrid creative reality',
    description:
      'Industry analysis on why organizations that hire for adaptability and judgment outperform those hiring solely for static legacy skillsets.',
    date: 'Sep 15, 2026',
    readTime: '3 min',
    image: '/images/pages/(home)/hero.webp',
    fullContent:
      'Channel Dive outlines the emergence of fractional talent squads and explains why enterprises are turning away from monolithic agencies in favor of modular platforms.',
  },
  {
    id: 'cat-10-computer-weekly',
    category: 'Media coverage',
    source: 'Computer Weekly',
    title: 'Deagensie skills index exposes AI talent misdirection in creative agencies',
    description:
      'Investigation into agency retainer bloat and how modern platforms deliver 3x output with focused, AI-assisted specialist squads.',
    date: 'Sep 14, 2026',
    readTime: '4 min',
    image: '/images/pages/about/hero-2.png',
    fullContent:
      'Computer Weekly examines Deagensie’s Talent Index, documenting how creative directors and lead engineers achieve superior project velocity when supported by intelligent workflow automation.',
  },
  {
    id: 'cat-11-silicon-postings',
    category: 'Media coverage',
    source: 'Silicon Republic',
    title: 'More than half of AI job postings seek skills beyond job titles, research finds',
    description:
      'A breakdown of the mismatch between HR search queries and actual project engineering requirements.',
    date: 'Sep 11, 2026',
    readTime: '4 min',
    image: '/images/pages/about/who-we-are.webp',
    fullContent:
      'Analysis of recruitment trends indicating that portfolio proof-of-work and verified dynamic problem solving now hold twice the hiring weight of conventional certifications.',
  },
  {
    id: 'cat-12-cncf-training',
    category: 'Press releases',
    title: 'Deagensie and CNCF Developer Training Program trains more than 5,600 technologists',
    description:
      'Milestone report on empowering emerging-market engineers with production cloud-native and generative AI development skills.',
    date: 'Aug 29, 2026',
    readTime: '4 min',
    image: '/images/pages/why/hero.webp',
    fullContent:
      'Deagensie celebrated the graduation of 5,600 technologists certified in container orchestration, microservice architectures, and modern platform engineering across Africa and Latin America.',
  },
  {
    id: 'cat-13-idc-techbrief',
    category: 'Analyst reports',
    source: 'IDC',
    title: 'IDC TechBrief: AI-Empowered Candidate Assessment & Talent Matching',
    description:
      'IDC analyst review evaluating next-generation talent platforms and the economic impact of algorithmic squad assembly.',
    date: 'Aug 15, 2026',
    readTime: '12 min',
    image: '/images/pages/(home)/hero.webp',
    fullContent:
      'Independent IDC research evaluating Deagensie’s predictive matching engine, documenting a 94% first-time project satisfaction rating among participating venture clients.',
  },
  {
    id: 'cat-14-github-training',
    category: 'Press releases',
    title: 'Deagensie to train 3,000 technologists in AI creative coding with GitHub',
    description:
      'Partnership initiative bringing advanced Copilot workflows and modern software engineering practices to global talent hubs.',
    date: 'Jul 20, 2026',
    readTime: '5 min',
    image: '/images/pages/about/hero-2.png',
    fullContent:
      'Collaborative initiative providing thousands of emerging developers with GitHub Copilot access, hands-on architectural mentorship, and fast-track placement into Deagensie TaaS squads.',
  },
  {
    id: 'cat-15-forward-deployed',
    category: 'Press releases',
    title:
      'The forward-deployed engineer: Why talent, not technology, is the true bottleneck for enterprise AI',
    description:
      'Executive white paper analyzing why organizational change management and embedded domain talent dictate AI implementation success.',
    date: 'Jul 2, 2026',
    readTime: '6 min',
    image: '/images/pages/blog/hero.webp',
    fullContent:
      'Drawing on implementations across 80+ companies, this report demonstrates that enterprise AI fails when treated as a software package rather than an operational discipline backed by forward-deployed engineers.',
  },
  {
    id: 'cat-16-gartner-guide',
    category: 'Analyst reports',
    source: 'Gartner',
    title: 'Gartner Market Guide: Elastic Engineering & Creative Talent Platforms',
    description:
      'Industry analysis examining how high-growth tech ventures leverage fractional squads to bypass 6-month recruiting cycles.',
    date: 'Jun 18, 2026',
    readTime: '14 min',
    image: '/images/pages/about/hero.webp',
    fullContent:
      'Gartner’s annual market guide outlines the shift from traditional staffing agencies to programmatic talent platforms that deliver vetted, managed squads within days.',
  },
  {
    id: 'cat-17-founders-os',
    category: 'Company news',
    title: 'Founder’s Growth OS: The 0-to-1 Brand Scaling Roadmap released by Deagensie Growth Lab',
    description:
      'Operational toolkit, brand positioning matrices, and conversion funnels for venture founders ready to scale.',
    date: 'Jun 05, 2026',
    readTime: '10 min',
    image: '/images/pages/why/hero.webp',
    fullContent:
      'Deagensie Growth Lab released its proprietary Growth OS toolkit, providing founders with battle-tested templates for positioning statements, design token architecture, and market-entry automation.',
  },
  {
    id: 'cat-18-design-systems',
    category: 'Company news',
    title: 'Maintaining Brand Consistency with Enterprise Design Systems at Scale',
    description:
      'Best practices for multi-brand architecture, accessible Vue components, and cross-platform UI tokens.',
    date: 'May 22, 2026',
    readTime: '7 min',
    image: '/images/pages/about/who-we-are.webp',
    fullContent:
      'Step-by-step case study exploring how Deagensie unified digital identity across 4 corporate subsidiaries using headless design tokens and automated accessibility CI checks.',
  },
];

// -------------------------------------------------------------
// Interactive Category Filters & Counts (matching Andela pattern)
// -------------------------------------------------------------
type FilterCategory =
  | 'All articles'
  | 'Media coverage'
  | 'Analyst reports'
  | 'Press releases'
  | 'Company news'
  | 'Product releases';

const selectedCategory = ref<FilterCategory>('All articles');
const searchQuery = ref('');

const categoriesList: {
  name: FilterCategory;
  count: number;
  disabled?: boolean;
  tooltip?: string;
}[] = [
  { name: 'All articles', count: 0 }, // computed dynamically
  { name: 'Media coverage', count: 157 },
  { name: 'Analyst reports', count: 20 },
  { name: 'Press releases', count: 29 },
  { name: 'Company news', count: 83 },
  { name: 'Product releases', count: 0, disabled: true, tooltip: 'Coming soon' },
];

// Filter logic
const filteredArticles = computed(() => {
  return categoryArticles.filter((item) => {
    const matchesCategory =
      selectedCategory.value === 'All articles' || item.category === selectedCategory.value;
    const q = searchQuery.value.trim().toLowerCase();
    const matchesSearch =
      q === '' ||
      item.title.toLowerCase().includes(q) ||
      item.description.toLowerCase().includes(q) ||
      item.category.toLowerCase().includes(q) ||
      (item.source && item.source.toLowerCase().includes(q));
    return matchesCategory && matchesSearch;
  });
});

// Dynamic pagination
const itemsPerPage = 6;
const currentPage = ref(1);

const totalPages = computed(() => {
  return Math.max(1, Math.ceil(filteredArticles.value.length / itemsPerPage));
});

const paginatedArticles = computed(() => {
  const start = (currentPage.value - 1) * itemsPerPage;
  return filteredArticles.value.slice(start, start + itemsPerPage);
});

const handleCategoryChange = (cat: FilterCategory) => {
  if (cat === 'Product releases') return;
  selectedCategory.value = cat;
  currentPage.value = 1;
};

const goToPage = (page: number) => {
  if (page < 1 || page > totalPages.value) return;
  currentPage.value = page;
  const section = document.getElementById('explore-categories');
  if (section) {
    section.scrollIntoView({ behavior: 'smooth', block: 'start' });
  }
};

// -------------------------------------------------------------
// Modals & Interactive Actions
// -------------------------------------------------------------
const activeModalArticle = ref<ArticleItem | null>(null);
const showPressContactModal = ref(false);

const openArticleModal = (article: ArticleItem) => {
  activeModalArticle.value = article;
};

const closeArticleModal = () => {
  activeModalArticle.value = null;
};

// Media & Brand downloads
const handleDownloadBrandBook = () => {
  push.success({
    title: 'Brand Book Downloaded',
    message: 'Deagensie Brand Guidelines 2026 (PDF • 24.8 MB) download started.',
  });
};

const handleDownloadLogoKit = () => {
  push.success({
    title: 'Logo Kit Downloaded',
    message: 'Deagensie Official Logo Assets (SVG, PNG, EPS package) download started.',
  });
};

const copyPressEmail = async () => {
  try {
    await navigator.clipboard.writeText('support@deagensie.com');
    push.success({
      title: 'Email Copied!',
      message: 'support@deagensie.com copied to your clipboard.',
    });
  } catch {
    push.info({
      title: 'Press Inquiries',
      message: 'Please send your media inquiries to support@deagensie.com',
    });
  }
};

// Newsletter
const newsletterEmail = ref('');
const isSubscribing = ref(false);

const handleNewsletterSubmit = () => {
  if (!newsletterEmail.value) return;
  isSubscribing.value = true;
  setTimeout(() => {
    push.success({
      title: 'Subscribed to Deagensie Insights!',
      message: `Thank you for subscribing with ${newsletterEmail.value}. You will receive our bi-weekly edition.`,
    });
    newsletterEmail.value = '';
    isSubscribing.value = false;
  }, 600);
};
</script>

<template>
  <div class="min-h-screen bg-white text-[#132128]">
    <!-- Top Padding Spacer to clear sticky site header -->
    <div class="h-24 sm:h-28 lg:h-32"></div>

    <!-- ============================================================== -->
    <!-- 1. HERO SECTION & FEATURED STORIES (Screenshots 3 & 2)          -->
    <!-- ============================================================== -->
    <section class="mx-auto w-11/12 max-w-7xl pt-4 pb-12 sm:pt-8 sm:pb-16">
      <!-- Centered Header -->
      <div v-reveal="'fade-up'" class="mx-auto max-w-3xl text-center">
        <h1 class="type-display-title mx-auto max-w-[24ch] font-serif text-gray-900">
          Deagensie <span class="text-[#04308F] italic">Newsroom</span>
        </h1>
        <p class="mt-4 text-base leading-relaxed text-[#717A7E] sm:text-lg lg:text-xl">
          The latest media coverage on Deagensie and the future of human-led AI transformation.
        </p>
      </div>

      <!-- Hero Featured Card (Screenshot 3) -->
      <div
        v-reveal="'scale-in'"
        class="group relative mt-10 cursor-pointer overflow-hidden rounded-3xl bg-[#091D1A] text-white shadow-xl transition-all duration-500 hover:shadow-2xl sm:mt-12"
        @click="openArticleModal(heroFeaturedArticle)"
      >
        <!-- Background Hero Visual / Graphic with Partner Badge Overlay -->
        <div
          class="relative min-h-[380px] w-full overflow-hidden sm:min-h-[460px] lg:min-h-[520px]"
        >
          <!-- Ambient dynamic background gradient -->
          <div
            class="absolute inset-0 bg-gradient-to-br from-[#0c2e27] via-[#091D1A] to-[#041014] opacity-95"
          ></div>

          <!-- Abstract tech wave contours -->
          <svg
            class="absolute inset-0 size-full opacity-30 mix-blend-screen"
            viewBox="0 0 1200 600"
            fill="none"
            xmlns="http://www.w3.org/2000/svg"
            preserveAspectRatio="none"
          >
            <path
              d="M0,350 C300,450 600,250 1200,420 L1200,600 L0,600 Z"
              fill="url(#greenWaveGrad)"
            />
            <path
              d="M0,420 C400,320 800,480 1200,380 L1200,600 L0,600 Z"
              fill="#104D3F"
              opacity="0.4"
            />
            <defs>
              <linearGradient id="greenWaveGrad" x1="0%" y1="0%" x2="100%" y2="100%">
                <stop offset="0%" stop-color="#338632" stop-opacity="0.6" />
                <stop offset="100%" stop-color="#05DED5" stop-opacity="0.3" />
              </linearGradient>
            </defs>
          </svg>

          <!-- Centered Floating Badge (OpenAI / AI Innovation Partner Graphic) -->
          <div
            class="absolute top-1/2 left-1/2 flex -translate-x-1/2 -translate-y-2/3 items-center justify-center transition-transform duration-700 group-hover:scale-105 sm:-translate-y-1/2"
          >
            <div
              class="flex flex-col items-center rounded-2xl border border-white/20 bg-white/95 px-8 py-6 text-gray-900 shadow-2xl backdrop-blur-md sm:flex-row sm:gap-6 sm:px-12 sm:py-8"
            >
              <div
                class="flex size-14 items-center justify-center rounded-xl bg-[#10292C] text-white sm:size-16"
              >
                <Icon icon="lucide:cpu" class="text-3xl text-[#05DED5] sm:text-4xl" />
              </div>
              <div class="text-center sm:text-left">
                <div class="text-xs font-semibold tracking-widest text-[#338632] uppercase">
                  Global Innovation
                </div>
                <div class="text-xl font-bold tracking-tight text-gray-900 sm:text-3xl">
                  AI Creative Partner
                </div>
              </div>
            </div>
          </div>

          <!-- Bottom Content Overlay -->
          <div
            class="absolute inset-x-0 bottom-0 bg-gradient-to-t from-black/90 via-black/50 to-transparent p-6 sm:p-10 lg:p-12"
          >
            <div class="max-w-4xl space-y-3 sm:space-y-4">
              <!-- Pill Tag -->
              <div
                class="inline-flex items-center gap-2 rounded-md bg-white/15 px-3 py-1 text-xs font-semibold tracking-wider text-white uppercase backdrop-blur-sm"
              >
                {{ heroFeaturedArticle.category }}
              </div>

              <!-- Main Title Headline -->
              <h2
                class="font-serif text-2xl leading-tight font-normal text-white transition-colors group-hover:underline sm:text-4xl lg:text-5xl"
              >
                {{ heroFeaturedArticle.title }}
              </h2>

              <!-- Details & Metadata -->
              <div class="flex items-center gap-3 text-xs font-medium text-gray-300 sm:text-sm">
                <span>{{ heroFeaturedArticle.date }}</span>
                <span class="opacity-40">|</span>
                <span class="inline-flex items-center gap-1.5">
                  <Icon icon="lucide:clock" class="text-base text-gray-300" />
                  {{ heroFeaturedArticle.readTime }}
                </span>
              </div>
            </div>
          </div>
        </div>
      </div>

      <!-- Top 3 Featured Articles Row (Screenshots 2 & 5) -->
      <div class="mt-8 grid grid-cols-1 gap-6 sm:gap-8 md:grid-cols-2 lg:grid-cols-3">
        <article
          v-for="(item, idx) in topThreeFeatured"
          :key="item.id"
          v-reveal="{ animation: 'fade-up', delay: idx * 100 }"
          class="group flex cursor-pointer flex-col justify-between"
          @click="openArticleModal(item)"
        >
          <!-- Image Container -->
          <div
            class="relative aspect-16/10 w-full overflow-hidden rounded-2xl bg-gray-100 shadow-xs"
          >
            <NuxtImg
              :src="item.image"
              :alt="item.title"
              class="size-full object-cover transition-transform duration-500 group-hover:scale-105"
            />
            <!-- Dark Overlay on hover -->
            <div
              class="absolute inset-0 bg-black/10 opacity-0 transition-opacity duration-300 group-hover:opacity-100"
            ></div>
            <div
              v-if="item.source"
              class="absolute bottom-3 left-4 text-xs font-bold tracking-wider text-white uppercase drop-shadow-md"
            >
              {{ item.source }}
            </div>
          </div>

          <!-- Article Text Details -->
          <div class="mt-4 flex flex-1 flex-col justify-between space-y-3">
            <div>
              <span
                class="inline-block rounded-xs bg-[#F0F2F3] px-2.5 py-1 text-[11px] font-semibold tracking-wider text-[#132128] uppercase"
              >
                {{ item.category }}
              </span>
              <h3
                class="mt-2 text-base leading-snug font-semibold text-[#132128] transition-colors group-hover:underline sm:text-lg"
              >
                {{ item.title }}
              </h3>
            </div>

            <!-- Date & Read Time -->
            <div class="flex items-center gap-2 pt-1 text-xs text-[#717A7E]">
              <span>{{ item.date }}</span>
              <span class="opacity-40">|</span>
              <span class="inline-flex items-center gap-1">
                <Icon icon="lucide:clock" class="text-sm text-[#717A7E]" />
                {{ item.readTime }}
              </span>
            </div>
          </div>
        </article>
      </div>
    </section>

    <!-- ============================================================== -->
    <!-- 2. EXPLORE BY CATEGORY SECTION (Screenshots 2 & 4)              -->
    <!-- ============================================================== -->
    <section
      id="explore-categories"
      class="mx-auto w-11/12 max-w-7xl pt-12 pb-16 sm:pt-16 sm:pb-24"
    >
      <!-- Section Title -->
      <div v-reveal="'fade-up'" class="text-center">
        <h2
          class="mx-auto w-full max-w-3xl text-center font-serif text-2xl leading-tight font-normal tracking-tight text-gray-900 sm:text-4xl lg:text-5xl 2xl:text-6xl"
        >
          Explore by <span class="text-[#04308F] italic">category</span>
        </h2>
      </div>

      <!-- Filter Radio Pills & Search Bar (Screenshot 2) -->
      <div class="mt-8 flex flex-col items-center gap-6 sm:mt-10">
        <!-- Category Filter Pills -->
        <div class="flex flex-wrap items-center justify-center gap-2 sm:gap-3">
          <button
            v-for="cat in categoriesList"
            :key="cat.name"
            type="button"
            :disabled="cat.disabled"
            class="group relative inline-flex items-center gap-2 rounded-full px-4 py-2 text-xs font-medium transition-all sm:px-5 sm:py-2.5 sm:text-sm"
            :class="[
              cat.disabled
                ? 'cursor-not-allowed bg-[#F0F2F3] text-gray-400'
                : selectedCategory === cat.name
                  ? 'bg-[#132128] text-white shadow-sm'
                  : 'bg-[#F0F2F3] text-[#132128] hover:bg-[#E5E7EB]',
            ]"
            @click="handleCategoryChange(cat.name)"
          >
            <span>{{ cat.name }}</span>

            <!-- Tooltip for Disabled / Coming soon -->
            <span
              v-if="cat.tooltip"
              class="relative flex items-center text-gray-400"
              title="Coming soon"
            >
              <Icon icon="lucide:info" class="text-sm" />
            </span>

            <!-- Count badge -->
            <span
              v-if="cat.count > 0 || cat.name === 'All articles'"
              class="text-xs font-semibold"
              :class="selectedCategory === cat.name ? 'text-[#7FC87C]' : 'text-[#717A7E]'"
            >
              {{ cat.name === 'All articles' ? categoryArticles.length : cat.count }}
            </span>
          </button>
        </div>

        <!-- Optional Instant Search Bar -->
        <div class="relative w-full max-w-md">
          <Icon
            icon="lucide:search"
            class="absolute top-1/2 left-4 -translate-y-1/2 text-lg text-gray-400"
          />
          <input
            v-model="searchQuery"
            type="text"
            placeholder="Search all articles, news & reports..."
            class="w-full rounded-full border border-gray-200 bg-gray-50/80 py-2.5 pr-10 pl-11 text-sm text-[#132128] transition-colors placeholder:text-gray-400 focus:border-[#132128] focus:bg-white focus:outline-none"
            @input="currentPage = 1"
          />
          <button
            v-if="searchQuery"
            type="button"
            class="absolute top-1/2 right-3 -translate-y-1/2 text-gray-400 hover:text-gray-600"
            @click="
              searchQuery = '';
              currentPage = 1;
            "
          >
            <Icon icon="lucide:x" class="text-base" />
          </button>
        </div>
      </div>

      <!-- Article Grid (3 columns, Screenshots 2 & 4 & 5) -->
      <div class="mt-12 sm:mt-16">
        <!-- Empty State -->
        <div
          v-if="filteredArticles.length === 0"
          class="rounded-3xl border border-gray-100 bg-[#F7F8F9] py-16 text-center"
        >
          <Icon icon="lucide:search-x" class="mx-auto text-4xl text-gray-400" />
          <p class="mt-3 font-serif text-lg text-gray-700">No articles found in this category.</p>
          <button
            type="button"
            class="mt-4 rounded-full bg-[#132128] px-6 py-2 text-xs font-semibold text-white hover:bg-black"
            @click="
              selectedCategory = 'All articles';
              searchQuery = '';
              currentPage = 1;
            "
          >
            Reset Filters
          </button>
        </div>

        <!-- Grid of Articles -->
        <div v-else class="grid grid-cols-1 gap-8 md:grid-cols-2 lg:grid-cols-3">
          <article
            v-for="(item, aIdx) in paginatedArticles"
            :key="item.id"
            v-reveal="{ animation: 'fade-up', delay: (aIdx % 3) * 80 }"
            class="group flex cursor-pointer flex-col justify-between"
            @click="openArticleModal(item)"
          >
            <!-- Card Image -->
            <div class="relative aspect-16/10 w-full overflow-hidden rounded-2xl bg-[#0B1A24]">
              <NuxtImg
                :src="item.image"
                :alt="item.title"
                class="size-full object-cover transition-transform duration-500 group-hover:scale-105"
              />
              <div
                class="absolute inset-0 bg-black/10 opacity-0 transition-opacity duration-300 group-hover:opacity-100"
              ></div>
              <!-- Source Badge if present (like Atlantic Council, ECI, Silicon Republic) -->
              <div
                v-if="item.source"
                class="absolute bottom-3 left-4 text-xs font-bold tracking-wide text-white uppercase drop-shadow-md"
              >
                {{ item.source }}
              </div>
            </div>

            <!-- Card Body -->
            <div class="mt-4 flex flex-1 flex-col justify-between space-y-3">
              <div>
                <span
                  class="inline-block rounded-xs bg-[#F0F2F3] px-2.5 py-1 text-[11px] font-semibold tracking-wider text-[#132128] uppercase"
                >
                  {{ item.category }}
                </span>
                <h3
                  class="mt-2 text-base leading-snug font-semibold text-[#132128] transition-colors group-hover:underline sm:text-lg"
                >
                  {{ item.title }}
                </h3>
              </div>

              <!-- Date & Read Time with clock icon -->
              <div class="flex items-center gap-2 pt-1 text-xs text-[#717A7E]">
                <span>{{ item.date }}</span>
                <span class="opacity-40">|</span>
                <span class="inline-flex items-center gap-1">
                  <Icon icon="lucide:clock" class="text-sm text-[#717A7E]" />
                  {{ item.readTime }}
                </span>
              </div>
            </div>
          </article>
        </div>
      </div>

      <!-- Pagination (Screenshot 4) -->
      <div v-if="totalPages > 1" class="mt-14 flex items-center justify-center gap-2 sm:gap-3">
        <!-- Prev Button -->
        <button
          type="button"
          :disabled="currentPage === 1"
          class="rounded-full border border-[#E7E9EA] px-4 py-2 text-xs font-medium text-[#132128] transition-colors hover:border-[#132128] disabled:cursor-not-allowed disabled:border-[#E7E9EA] disabled:text-gray-300 sm:text-sm"
          @click="goToPage(currentPage - 1)"
        >
          Prev
        </button>

        <!-- Dynamic Numeric Page Buttons -->
        <template v-for="p in totalPages" :key="p">
          <button
            type="button"
            class="flex size-9 items-center justify-center rounded-full text-xs font-medium transition-all sm:size-10 sm:text-sm"
            :class="[
              currentPage === p
                ? 'bg-[#132128] font-bold text-white shadow-xs'
                : 'text-[#132128] hover:bg-gray-100',
            ]"
            @click="goToPage(p)"
          >
            {{ p }}
          </button>
        </template>

        <!-- Next Button -->
        <button
          type="button"
          :disabled="currentPage === totalPages"
          class="rounded-full border border-[#E7E9EA] px-4 py-2 text-xs font-medium text-[#132128] transition-colors hover:border-[#132128] disabled:cursor-not-allowed disabled:border-[#E7E9EA] disabled:text-gray-300 sm:text-sm"
          @click="goToPage(currentPage + 1)"
        >
          Next
        </button>
      </div>
    </section>

    <!-- ============================================================== -->
    <!-- 3. PRESS & MEDIA RESOURCES (Screenshot 1)                       -->
    <!-- ============================================================== -->
    <section class="border-t border-gray-100 bg-white py-16 sm:py-24">
      <div class="mx-auto w-11/12 max-w-7xl">
        <!-- Section Header -->
        <div v-reveal="'fade-up'" class="mx-auto max-w-2xl text-center">
          <h2
            class="mx-auto w-full max-w-3xl text-center font-serif text-2xl leading-tight font-normal tracking-tight text-gray-900 sm:text-4xl lg:text-5xl 2xl:text-6xl"
          >
            Press &amp; media resources
          </h2>
          <p class="mt-3 text-base text-[#717A7E] sm:text-lg">
            Resources and contact information for journalists and media professionals.
          </p>
        </div>

        <!-- 2 Side-by-Side Resource Cards (Screenshot 1) -->
        <div class="mt-12 grid grid-cols-1 gap-8 lg:grid-cols-2">
          <!-- Card 1: Brand book -->
          <div
            v-reveal="'fade-up'"
            class="group relative flex flex-col justify-between overflow-hidden rounded-3xl bg-gradient-to-br from-[#EBF5EE] via-[#E2F2E7] to-[#D5EDE0] p-8 shadow-xs transition-shadow duration-300 hover:shadow-lg sm:p-10"
          >
            <div class="grid grid-cols-1 items-center gap-6 sm:grid-cols-[1.2fr_1fr]">
              <div class="space-y-4">
                <h3 class="text-2xl font-bold tracking-tight text-[#132128] sm:text-3xl">
                  Deagensie brand book
                </h3>
                <p class="text-sm leading-relaxed text-[#10292C]/80 sm:text-base">
                  Access brand guidelines, colors, typography, and core assets.
                </p>
                <div class="pt-2">
                  <button
                    type="button"
                    class="inline-flex items-center gap-2 text-sm font-semibold text-[#1B5E20] transition-colors hover:text-[#0D3812]"
                    @click="handleDownloadBrandBook"
                  >
                    Download brand book
                    <span
                      class="flex size-6 items-center justify-center rounded-md bg-[#2E7D32] text-white"
                    >
                      <Icon icon="lucide:arrow-right" class="text-sm" />
                    </span>
                  </button>
                </div>
              </div>

              <!-- Graphic / Photo Mockup (Screenshot 1) -->
              <div
                class="relative overflow-hidden rounded-2xl border border-white/60 bg-white/60 shadow-md"
              >
                <NuxtImg
                  src="/images/pages/about/who-we-are.webp"
                  alt="Deagensie Brand Book Preview"
                  class="size-full object-cover transition-transform duration-500 group-hover:scale-105"
                />
                <div
                  class="absolute right-3 bottom-3 rounded-lg border border-white/40 bg-white/90 p-2.5 shadow-sm backdrop-blur-xs"
                >
                  <div class="text-[10px] font-semibold text-gray-500 uppercase">Brand OS</div>
                  <div class="text-xs font-bold text-[#132128]">2026 Edition</div>
                </div>
              </div>
            </div>
          </div>

          <!-- Card 2: The logo -->
          <div
            v-reveal="{ animation: 'fade-up', delay: 150 }"
            class="group relative flex flex-col justify-between overflow-hidden rounded-3xl border border-gray-100 bg-[#F7F8F9] p-8 shadow-xs transition-shadow duration-300 hover:shadow-lg sm:p-10"
          >
            <div class="grid grid-cols-1 items-center gap-6 sm:grid-cols-[1.2fr_1fr]">
              <div class="space-y-4">
                <h3 class="text-2xl font-bold tracking-tight text-[#132128] sm:text-3xl">
                  The Deagensie logo
                </h3>
                <p class="text-sm leading-relaxed text-[#717A7E] sm:text-base">
                  Download official logo files and review logo usage guidelines.
                </p>
                <div class="pt-2">
                  <button
                    type="button"
                    class="inline-flex items-center gap-2 text-sm font-semibold text-[#1B5E20] transition-colors hover:text-[#0D3812]"
                    @click="handleDownloadLogoKit"
                  >
                    Download logo kit
                    <span
                      class="flex size-6 items-center justify-center rounded-md bg-[#2E7D32] text-white"
                    >
                      <Icon icon="lucide:arrow-right" class="text-sm" />
                    </span>
                  </button>
                </div>
              </div>

              <!-- Graphic: Logo Stack Mockup (Screenshot 1) -->
              <div
                class="flex flex-col items-center justify-center gap-3 rounded-2xl border border-gray-200 bg-white p-6 shadow-md transition-transform duration-500 group-hover:scale-105"
              >
                <div class="flex items-center gap-2 text-gray-300">
                  <Icon icon="lucide:sparkles" class="text-sm" />
                  <span class="text-xs font-bold tracking-widest uppercase">deagensie</span>
                </div>
                <div class="flex items-center gap-2 rounded-lg bg-gray-50 px-4 py-2 text-[#132128]">
                  <Icon icon="lucide:sparkles" class="text-sm text-[#05DED5]" />
                  <span class="text-sm font-bold tracking-wider uppercase">deagensie</span>
                </div>
                <div class="flex items-center gap-2 text-gray-300">
                  <Icon icon="lucide:sparkles" class="text-sm" />
                  <span class="text-xs font-bold tracking-widest uppercase">deagensie</span>
                </div>
              </div>
            </div>
          </div>
        </div>

        <!-- Media Inquiries Block (Screenshot 1) -->
        <div v-reveal="'fade-up'" class="mt-14 text-center sm:mt-16">
          <p class="text-base font-normal text-[#132128] sm:text-lg">
            For media inquiries, contact us
          </p>
          <div class="mt-4">
            <button
              type="button"
              class="inline-flex items-center gap-2 rounded-full bg-[#132128] px-7 py-3 text-sm font-semibold text-white shadow-md transition-all duration-300 hover:scale-105 hover:bg-black"
              @click="showPressContactModal = true"
            >
              Send us an email
              <Icon icon="lucide:arrow-right" class="text-base" />
            </button>
          </div>
        </div>
      </div>
    </section>

    <!-- ============================================================== -->
    <!-- 4. FOOTER CTA SECTION (matching Andela & Deagensie)             -->
    <!-- ============================================================== -->
    <section class="border-t border-gray-100 bg-[#FAFAFA] py-16 sm:py-24">
      <div class="mx-auto w-11/12 max-w-7xl">
        <div
          v-reveal="'fade-up'"
          class="relative overflow-hidden rounded-3xl bg-[#0F2326] p-8 text-white shadow-xl sm:p-12 lg:p-16"
        >
          <div class="grid grid-cols-1 items-center gap-10 lg:grid-cols-2 lg:gap-16">
            <!-- Left Info -->
            <div class="space-y-6">
              <h3
                class="font-serif text-3xl leading-tight font-normal text-white sm:text-4xl lg:text-5xl"
              >
                Accelerate how your organization builds and scales venture growth
              </h3>
              <p class="text-sm leading-relaxed text-gray-300 sm:text-base">
                Deploy specialized creative squads, build scalable digital platforms, and upskill
                teams to power high-impact venture execution.
              </p>
              <div>
                <NuxtLink
                  to="/contact"
                  class="inline-flex items-center gap-2 rounded-full bg-white px-7 py-3 text-sm font-semibold text-gray-900 shadow-md transition-all duration-300 hover:scale-105 hover:bg-[#05DED5]"
                >
                  Book a discovery call
                  <Icon icon="lucide:arrow-right" class="text-base" />
                </NuxtLink>
              </div>
            </div>

            <!-- Right: Collaborative team image -->
            <div
              class="relative overflow-hidden rounded-2xl border border-white/10 bg-white/5 p-6 backdrop-blur-xs"
            >
              <div class="overflow-hidden rounded-xl">
                <NuxtImg
                  src="/images/pages/business/hero.webp"
                  alt="Creative team collaborating around a table"
                  class="aspect-video w-full object-cover"
                />
              </div>
              <div
                class="mt-4 flex flex-wrap items-center justify-between gap-4 border-t border-white/10 pt-4 text-xs text-gray-400"
              >
                <span>Venture Growth Lab</span>
                <span>•</span>
                <span>Talent-as-a-Service</span>
                <span>•</span>
                <span>AI Matching</span>
              </div>
            </div>
          </div>

          <!-- Bottom Newsletter Bar -->
          <div class="mt-12 border-t border-white/10 pt-8">
            <div class="flex flex-col items-center justify-between gap-6 lg:flex-row">
              <p class="text-center text-sm text-gray-200 sm:text-base lg:text-left">
                Subscribe for insights on building and scaling creative systems.
              </p>
              <form
                class="flex w-full max-w-md flex-col gap-3 sm:flex-row"
                @submit.prevent="handleNewsletterSubmit"
              >
                <input
                  v-model="newsletterEmail"
                  type="email"
                  placeholder="Enter your email"
                  required
                  class="flex-1 rounded-full border border-white/20 bg-white/10 px-5 py-3 text-sm text-white placeholder:text-gray-400 focus:border-[#05DED5] focus:outline-none"
                />
                <button
                  type="submit"
                  :disabled="isSubscribing"
                  class="inline-flex items-center justify-center gap-2 rounded-full bg-[#338632] px-6 py-3 text-sm font-semibold text-white transition-all hover:bg-[#286e27] disabled:opacity-50"
                >
                  <template v-if="isSubscribing">
                    <span>Subscribing</span>
                    <Icon icon="svg-spinners:3-dots-fade" class="text-lg" />
                  </template>
                  <template v-else>
                    <span>Subscribe</span>
                    <Icon icon="lucide:arrow-right" class="text-sm" />
                  </template>
                </button>
              </form>
            </div>
          </div>
        </div>
      </div>
    </section>

    <!-- ============================================================== -->
    <!-- 5. INTERACTIVE ARTICLE DETAIL MODAL                             -->
    <!-- ============================================================== -->
    <Transition name="fade-scale">
      <div
        v-if="activeModalArticle"
        class="fixed inset-0 z-50 flex items-center justify-center bg-black/60 p-4 backdrop-blur-xs"
        @click.self="closeArticleModal"
      >
        <div
          class="relative max-h-[90vh] w-full max-w-2xl space-y-6 overflow-y-auto rounded-3xl bg-white p-6 shadow-2xl sm:p-8"
        >
          <!-- Close button -->
          <button
            type="button"
            class="absolute top-6 right-6 flex size-10 items-center justify-center rounded-full bg-gray-100 text-gray-600 transition-colors hover:bg-gray-200"
            @click="closeArticleModal"
          >
            <Icon icon="lucide:x" class="text-xl" />
          </button>

          <!-- Category and Read Time -->
          <div class="flex items-center gap-3">
            <span
              class="rounded-xs bg-[#F0F2F3] px-3 py-1 text-xs font-semibold text-[#132128] uppercase"
            >
              {{ activeModalArticle.category }}
            </span>
            <span class="text-xs text-gray-400">• {{ activeModalArticle.readTime }}</span>
            <span v-if="activeModalArticle.source" class="text-xs font-semibold text-[#10292C]">
              • {{ activeModalArticle.source }}
            </span>
          </div>

          <!-- Headline -->
          <h3 class="font-serif text-2xl leading-tight font-normal text-[#132128] sm:text-3xl">
            {{ activeModalArticle.title }}
          </h3>

          <!-- Featured Image -->
          <div class="aspect-16/9 overflow-hidden rounded-2xl bg-gray-100">
            <NuxtImg
              :src="activeModalArticle.image"
              :alt="activeModalArticle.title"
              class="size-full object-cover"
            />
          </div>

          <!-- Description / Full Content -->
          <div class="space-y-4 text-sm leading-relaxed text-gray-700 sm:text-base">
            <p>{{ activeModalArticle.description }}</p>
            <p>{{ activeModalArticle.fullContent }}</p>

            <!-- Key points if available -->
            <div
              v-if="activeModalArticle.keyPoints && activeModalArticle.keyPoints.length"
              class="rounded-xl border border-gray-100 bg-gray-50 p-4"
            >
              <h4 class="mb-2 text-xs font-bold tracking-wider text-gray-900 uppercase">
                Key Highlights
              </h4>
              <ul class="space-y-2 text-xs text-gray-600 sm:text-sm">
                <li
                  v-for="(kp, kIndex) in activeModalArticle.keyPoints"
                  :key="kIndex"
                  class="flex items-start gap-2"
                >
                  <Icon icon="lucide:check-circle" class="mt-0.5 shrink-0 text-[#338632]" />
                  <span>{{ kp }}</span>
                </li>
              </ul>
            </div>
          </div>

          <!-- Modal Footer Actions -->
          <div
            class="flex flex-wrap items-center justify-between gap-4 border-t border-gray-100 pt-4"
          >
            <span class="text-xs text-gray-400">Published: {{ activeModalArticle.date }}</span>
            <div class="flex gap-3">
              <button
                type="button"
                class="rounded-full border border-gray-300 px-5 py-2 text-xs font-semibold text-gray-700 hover:border-[#132128] hover:text-[#132128]"
                @click="closeArticleModal"
              >
                Close
              </button>
              <NuxtLink
                to="/contact"
                class="rounded-full bg-[#132128] px-6 py-2 text-xs font-semibold text-white shadow-xs transition-colors hover:bg-black"
                @click="closeArticleModal"
              >
                Contact Press Team
              </NuxtLink>
            </div>
          </div>
        </div>
      </div>
    </Transition>

    <!-- ============================================================== -->
    <!-- 6. PRESS CONTACT MODAL                                          -->
    <!-- ============================================================== -->
    <Transition name="fade-scale">
      <div
        v-if="showPressContactModal"
        class="fixed inset-0 z-50 flex items-center justify-center bg-black/60 p-4 backdrop-blur-xs"
        @click.self="showPressContactModal = false"
      >
        <div class="relative w-full max-w-lg space-y-6 rounded-3xl bg-white p-8 shadow-2xl">
          <button
            type="button"
            class="absolute top-6 right-6 flex size-10 items-center justify-center rounded-full bg-gray-100 text-gray-600 transition-colors hover:bg-gray-200"
            @click="showPressContactModal = false"
          >
            <Icon icon="lucide:x" class="text-xl" />
          </button>

          <div
            class="flex size-14 items-center justify-center rounded-2xl bg-[#EBF5EE] text-[#2E7D32]"
          >
            <Icon icon="lucide:mail" class="text-3xl" />
          </div>

          <div class="space-y-2">
            <h3 class="font-serif text-2xl font-normal text-[#132128]">
              Media &amp; Press Inquiries
            </h3>
            <p class="text-sm text-gray-600">
              For interview requests, executive quotes, media kits, or brand inquiries, get in touch
              with our communications team.
            </p>
          </div>

          <div class="rounded-2xl border border-gray-200 bg-gray-50 p-4">
            <div class="text-xs font-semibold text-gray-500 uppercase">Press Email</div>
            <div class="mt-1 flex items-center justify-between gap-3">
              <span class="font-mono text-base font-semibold text-[#132128]"
                >support@deagensie.com</span
              >
              <button
                type="button"
                class="inline-flex items-center gap-1 rounded-md bg-white px-3 py-1.5 text-xs font-semibold text-gray-700 shadow-xs hover:bg-gray-100"
                @click="copyPressEmail"
              >
                <Icon icon="lucide:copy" class="text-sm" /> Copy
              </button>
            </div>
          </div>

          <div class="flex gap-3 pt-2">
            <a
              href="mailto:support@deagensie.com?subject=Media%20Inquiry%20-%20Deagensie%20Newsroom"
              class="flex-1 rounded-full bg-[#132128] py-3 text-center text-sm font-semibold text-white shadow-xs transition-colors hover:bg-black"
            >
              Open Email Client
            </a>
            <button
              type="button"
              class="rounded-full border border-gray-300 px-6 py-3 text-sm font-semibold text-gray-700 hover:bg-gray-50"
              @click="showPressContactModal = false"
            >
              Done
            </button>
          </div>
        </div>
      </div>
    </Transition>
  </div>
</template>

<style scoped>
.fade-scale-enter-active,
.fade-scale-leave-active {
  transition: all 0.25s ease-out;
}

.fade-scale-enter-from,
.fade-scale-leave-to {
  opacity: 0;
  transform: scale(0.96);
}
</style>
