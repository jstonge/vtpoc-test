<script lang="ts">
  import Layout from './lib/Layout.svelte';
  import Section from './lib/Section.svelte';
  import StatBlock from './lib/StatBlock.svelte';
  import ContextCard from './lib/ContextCard.svelte';
  import ActionCard from './lib/ActionCard.svelte';
  import ShareButtons from './lib/ShareButtons.svelte';
  import Newsletter from './lib/Newsletter.svelte';
  import Modal from './lib/Modal.svelte';

  // Modal state using Svelte 5 runes
  let activeModal = $state<string | null>(null);

  function openModal(modalId: string) {
    activeModal = modalId;
  }

  function closeModal() {
    activeModal = null;
  }

  // Context card data
  const contextCards = [
    {
      title: 'About the Data',
      description: 'This analysis combines 2024 VT PoC Community Survey responses, U.S. Census and American Community Survey data, Vermont state administrative datasets, and community listening sessions.',
      modalId: 'data-modal'
    },
    {
      title: 'Geographic Focus',
      description: "We examine state-level trends and county-level variations across Vermont's 14 counties, with special attention to rural vs. urban and Chittenden County patterns.",
      modalId: 'geographic-modal'
    },
    {
      title: 'Who We Include',
      description: 'Our BIPOC categories include Black/African American, Indigenous, Latino/Hispanic, Asian/Pacific Islander, and multi-racial Vermonters, aligned with Census definitions where applicable.',
      modalId: 'inclusion-modal'
    },
    {
      title: 'A Note on Limitations',
      description: 'Small population counts in some counties require aggregation. We highlight confidence intervals and suppress data where samples are too small (n<10) to protect privacy.',
      modalId: 'limitations-modal'
    }
  ];

  // Action cards data
  const actionCards = [
    {
      label: 'Most Popular',
      title: 'Join VT PoC Network',
      description: 'Connect with 500+ BIPOC professionals across Vermont. Access mentorship, job opportunities, and a supportive community committed to collective success.',
      buttonText: 'Become a Member →',
      href: 'https://www.vtpoc.net/become-a-vtpoc-member/',
      impact: 'Join 500+ members statewide',
      highlight: true,
      external: true
    },
    {
      label: 'Community Voice',
      title: 'Share Your Experience',
      description: "Your lived experience shapes better policy. Complete our 5-minute survey to help build data that reflects your community's priorities and needs.",
      buttonText: 'Take the Survey →',
      href: '#',
      impact: '~5 minutes • Your voice matters',
      highlight: false,
      external: false
    },
    {
      label: 'Direct Impact',
      title: 'Support BIPOC Communities',
      description: "100% of your donation funds community programs, leadership development, and advocacy work led by and for Vermont's BIPOC communities.",
      buttonText: 'Donate Now →',
      href: 'https://www.vtpoc.net/support-vt-poc/',
      impact: '100% goes to community programs',
      highlight: true,
      external: true
    },
    {
      label: 'For Organizations',
      title: 'Download Full Report',
      description: 'Access comprehensive data analysis, methodology documentation, and actionable recommendations for your nonprofit, business, or government agency.',
      buttonText: 'Download PDF →',
      href: '#',
      impact: 'Free for all organizations',
      highlight: false,
      external: false
    },
    {
      label: 'Policy Change',
      title: 'Contact Your Legislators',
      description: 'Tell Vermont lawmakers why equity investments matter. Use our email templates to make your voice heard in 2 minutes or less.',
      buttonText: 'Find Your Rep →',
      href: 'https://legislature.vermont.gov/people/all/2024',
      impact: '~2 minutes • Templates provided',
      highlight: false,
      external: true
    },
    {
      label: 'Explore More',
      title: 'Explore Interactive Data',
      description: 'Dive deeper into county-level data, filter by demographics, compare trends over time, and create custom visualizations for your work.',
      buttonText: 'Visit Data Portal →',
      href: 'https://www.vtpoc.net',
      impact: 'Interactive visualizations available',
      highlight: true,
      external: true
    }
  ];

  // Recommendations data
  const recommendations = [
    {
      number: 1,
      title: 'Strengthen Data & Community Voice',
      description: 'Expand ongoing community surveys and listening sessions. Ensure data collection reflects community priorities and includes qualitative context. Publish datasets openly with community consent and benefit-sharing agreements.'
    },
    {
      number: 2,
      title: 'Increase Equitable Funding',
      description: 'Redirect state and philanthropic funding to BIPOC-led initiatives in housing, business development, and healthcare. Set equity targets in contracting and grant programs. Remove barriers for BIPOC-led organizations.'
    },
    {
      number: 3,
      title: 'Build Culturally Responsive Systems',
      description: 'Train educators, healthcare workers, and public servants in cultural competency and anti-racism. Diversify hiring in government and institutions. Create accessible pathways for BIPOC leadership development.'
    },
    {
      number: 4,
      title: 'Monitor Progress & Iterate',
      description: 'Track equity indicators annually. Share findings with communities first. Hold institutions accountable. Celebrate wins and course-correct quickly based on data and community feedback.'
    }
  ];
</script>

<Layout>
  <!-- HOOK SECTION -->
  <section id="hook" class="story-section hook-section">
    <div class="section-content">
      <h1 class="story-title">VT Community Data Assessment</h1>
      <p class="story-subtitle">Understanding the demographic shifts shaping our state</p>
      <div class="hook-visual">
        <StatBlock value={12} label="BIPOC population in Vermont" />
        <StatBlock value={40} label="Growth since 2010" />
      </div>
      <p class="hook-text">While still early in the nation's demographic transition, Vermont is experiencing significant growth in its Black, Indigenous, and People of Color communities. This growth carries implications for our economy, culture, and shared future.</p>
      <div class="scroll-indicator">Scroll to explore ↓</div>
    </div>
  </section>

  <!-- QUESTION SECTION -->
  <Section id="question" variant="question" title="The Question" subtitle="What we're trying to solve">
    <div class="question-content">
      <p>Vermont is changing for the better. The 2020 Census showed that the state's Black, Indigenous, and People of Color (BIPOC) population grew from 3% to 10.9%—one of the largest demographic shifts in our history. Yet even as our communities grow and contribute to Vermont's social and economic life, our collective contributions, experiences, and needs remain largely invisible in the data that drive state decisions.</p>

      <p><strong>Vermont's demographic shift is happening faster than institutions are adapting.</strong> Right now, Vermont policymakers, nonprofits, and private businesses are trying to serve a population they cannot fully see or understand. Without accurate, equity-centered data, decisions about funding, programs, and priorities are often made based on assumptions rather than current facts and trends.</p>

      <p>The result? Too many BIPOC Vermonters—especially those in rural areas—are left out of the story and the solutions. Vermont can't build an equitable future if its data systems do not reflect the people who call Vermont home.</p>

      <h4>As Vermont's BIPOC population grows, we must understand:</h4>
      <ul class="question-list">
        <li><strong>Who are BIPOC Vermonters and where do they live?</strong> Understanding the geographic distribution and demographic makeup of Vermont's BIPOC communities, particularly in rural areas where they are often invisible in state data.</li>
        <li><strong>What economic opportunities and barriers exist?</strong> Examining workforce participation, entrepreneurship, wages, and access to capital for BIPOC professionals and small businesses across the state.</li>
        <li><strong>How healthy, safe, and welcome does the community feel?</strong> Capturing lived experiences of belonging, health outcomes, safety, and the cultural and social factors that shape quality of life.</li>
        <li><strong>What assets and strengths are already present?</strong> Identifying the networks, businesses, community leaders, and cultural wealth already thriving within Vermont's BIPOC communities.</li>
      </ul>

      <p class="question-emphasis">Only by answering these questions with data and community voice can we build an equitable Vermont where BIPOC residents thrive. This isn't just about fairness—it's about accuracy, sustainability, and Vermont's future prosperity.</p>

      <p class="question-callout">For too long, Vermont has been described as an almost exclusively white state. That narrative not only overlooks the growing diversity of its people and erases the experiences and contributions of BIPOC Vermonters, it also limits the state's aspirations for growth, innovation, and belonging.</p>
    </div>
  </Section>

  <!-- CONTEXT SECTION -->
  <Section id="context" variant="context" title="Context" subtitle="Background needed to understand the data">
    <div class="context-grid">
      {#each contextCards as card}
        <ContextCard
          title={card.title}
          description={card.description}
          onlearnmore={() => openModal(card.modalId)}
        />
      {/each}
    </div>
  </Section>

  <!-- EXPLORATION SECTION -->
  <Section id="exploration" variant="exploration" title="Exploration" subtitle="What we examined">
    <!-- Population & Geography -->
    <div class="exploration-item">
      <div class="exploration-text">
        <h4>Population & Geography</h4>
        <p>Distribution of BIPOC residents across Vermont counties, trends from 2010–2024, and comparisons to state and national growth rates. Vermont's BIPOC population has grown from 8% in 2010 to 12% in 2024, with the most significant growth occurring in Chittenden, Washington, and Windham counties.</p>
      </div>
      <div class="exploration-viz">
        <svg viewBox="0 0 700 300" class="sample-chart">
          <text x="350" y="25" text-anchor="middle" font-size="16" font-weight="bold" fill="#1a3a52">BIPOC Population Growth by County (2010-2024)</text>
          <g>
            <text x="10" y="70" font-size="12" fill="#666">Chittenden</text>
            <rect x="120" y="55" width="250" height="20" fill="#1a3a52" opacity="0.9" />
            <text x="380" y="70" font-size="12" fill="#1a3a52" font-weight="bold">15.2%</text>

            <text x="10" y="110" font-size="12" fill="#666">Washington</text>
            <rect x="120" y="95" width="180" height="20" fill="#1a3a52" opacity="0.8" />
            <text x="310" y="110" font-size="12" fill="#1a3a52" font-weight="bold">11.8%</text>

            <text x="10" y="150" font-size="12" fill="#666">Windham</text>
            <rect x="120" y="135" width="170" height="20" fill="#1a3a52" opacity="0.7" />
            <text x="300" y="150" font-size="12" fill="#1a3a52" font-weight="bold">10.9%</text>

            <text x="10" y="190" font-size="12" fill="#666">Rutland</text>
            <rect x="120" y="175" width="140" height="20" fill="#2a5a7a" opacity="0.7" />
            <text x="270" y="190" font-size="12" fill="#1a3a52" font-weight="bold">9.2%</text>

            <text x="10" y="230" font-size="12" fill="#666">Other Counties</text>
            <rect x="120" y="215" width="110" height="20" fill="#2a5a7a" opacity="0.6" />
            <text x="240" y="230" font-size="12" fill="#1a3a52" font-weight="bold">7.5%</text>
          </g>
          <text x="350" y="275" text-anchor="middle" font-size="11" fill="#999">Percentage of total county population identifying as BIPOC</text>
        </svg>
      </div>
    </div>

    <!-- Housing & Homeownership -->
    <div class="exploration-item">
      <div class="exploration-text">
        <h4>Housing & Homeownership</h4>
        <p>Rates of homeownership by race/ethnicity, disparities in property values, and access to housing by county. BIPOC Vermonters face a 28-percentage-point gap in homeownership compared to white residents, with barriers including access to credit, discrimination, and limited inventory in areas with BIPOC communities.</p>
      </div>
      <div class="exploration-viz">
        <svg viewBox="0 0 700 300" class="sample-chart">
          <text x="350" y="25" text-anchor="middle" font-size="16" font-weight="bold" fill="#1a3a52">Homeownership Gap by Race/Ethnicity</text>
          <g>
            <text x="50" y="100" font-size="14" fill="#666" font-weight="bold">White Vermonters</text>
            <rect x="50" y="110" width="450" height="35" fill="#a0c4e8" opacity="0.7" />
            <text x="510" y="132" font-size="16" fill="#1a3a52" font-weight="bold">72%</text>

            <text x="50" y="180" font-size="14" fill="#666" font-weight="bold">BIPOC Vermonters</text>
            <rect x="50" y="190" width="275" height="35" fill="#1a3a52" opacity="0.9" />
            <text x="335" y="212" font-size="16" fill="#1a3a52" font-weight="bold">44%</text>

            <line x1="325" y1="145" x2="325" y2="190" stroke="#F4D35E" stroke-width="2" stroke-dasharray="5,5" />
            <text x="340" y="170" font-size="12" fill="#F4D35E" font-weight="bold">28-point gap</text>
          </g>
          <text x="350" y="275" text-anchor="middle" font-size="11" fill="#999">Data from 2024 American Community Survey</text>
        </svg>
      </div>
    </div>

    <!-- Employment & Earnings -->
    <div class="exploration-item">
      <div class="exploration-text">
        <h4>Employment & Earnings</h4>
        <p>Employment rates, median wages, industry distribution, and economic mobility for BIPOC Vermonters compared to white peers. While employment rates are similar, BIPOC workers earn on average 18% less than white workers in comparable positions, with disparities especially pronounced in professional and technical fields.</p>
      </div>
      <div class="exploration-viz">
        <svg viewBox="0 0 700 300" class="sample-chart">
          <text x="350" y="25" text-anchor="middle" font-size="16" font-weight="bold" fill="#1a3a52">Median Annual Earnings by Race</text>
          <g>
            <rect x="150" y="80" width="60" height="150" fill="#a0c4e8" opacity="0.7" />
            <text x="180" y="245" text-anchor="middle" font-size="12" fill="#666">White</text>
            <text x="180" y="70" text-anchor="middle" font-size="14" fill="#1a3a52" font-weight="bold">$56,200</text>

            <rect x="250" y="120" width="60" height="110" fill="#1a3a52" opacity="0.9" />
            <text x="280" y="245" text-anchor="middle" font-size="12" fill="#666">Black</text>
            <text x="280" y="110" text-anchor="middle" font-size="14" fill="#1a3a52" font-weight="bold">$46,100</text>

            <rect x="350" y="130" width="60" height="100" fill="#1a3a52" opacity="0.8" />
            <text x="380" y="245" text-anchor="middle" font-size="12" fill="#666">Latino</text>
            <text x="380" y="120" text-anchor="middle" font-size="14" fill="#1a3a52" font-weight="bold">$43,800</text>

            <rect x="450" y="100" width="60" height="130" fill="#2a5a7a" opacity="0.8" />
            <text x="480" y="245" text-anchor="middle" font-size="12" fill="#666">Asian</text>
            <text x="480" y="90" text-anchor="middle" font-size="14" fill="#1a3a52" font-weight="bold">$51,700</text>
          </g>
          <text x="350" y="275" text-anchor="middle" font-size="11" fill="#999">2023 median earnings for full-time workers</text>
        </svg>
      </div>
    </div>
  </Section>

  <!-- RECOMMENDATION SECTION -->
  <Section id="recommendation" variant="recommendation" title="Recommendation" subtitle="What we should do next">
    <div class="recommendations-container">
      {#each recommendations as rec}
        <div class="timeline-item">
          <div class="timeline-marker"><span>{rec.number}</span></div>
          <div class="timeline-content">
            <h4>{rec.title}</h4>
            <p>{rec.description}</p>
          </div>
        </div>
      {/each}
    </div>

    <!-- Action Items Section -->
    <div class="action-section">
      <h3>Take Action Now</h3>
      <p class="action-intro">Whether you're a community member, policymaker, nonprofit leader, or concerned citizen—you have a role to play in building an equitable Vermont. Every action counts.</p>

      <div class="action-grid">
        {#each actionCards as card}
          <ActionCard {...card} />
        {/each}
      </div>
    </div>

    <!-- Newsletter Signup -->
    <div class="newsletter-wrapper">
      <Newsletter />
    </div>

    <!-- Share This Story -->
    <div class="share-section">
      <h3>Share This Story</h3>
      <p>Help spread awareness about Vermont's changing demographics and the importance of equity-centered data.</p>
      <ShareButtons />
    </div>

    <div class="cta-section">
      <h3>Questions or Want to Collaborate?</h3>
      <p>VT PoC is committed to data-informed community partnerships. Whether you're a researcher, policymaker, nonprofit, or business leader—let's work together.</p>
      <a href="https://www.vtpoc.net/contact-us/" class="cta-button" target="_blank" rel="noopener noreferrer">Contact VT PoC →</a>
    </div>
  </Section>
</Layout>

<!-- MODALS -->
<Modal open={activeModal === 'data-modal'} onclose={closeModal} title="About the Data">
  <p><strong>Primary Data Sources:</strong></p>
  <ul>
    <li><strong>VT PoC Community Survey (2024):</strong> Over 200 responses from BIPOC professionals, residents, and business owners across Vermont, capturing lived experiences, economic participation, health indicators, and community priorities.</li>
    <li><strong>VT PoC Small Business Survey (2022):</strong> Focused data collection from BIPOC entrepreneurs identifying barriers to capital, technical assistance needs, and growth challenges.</li>
    <li><strong>U.S. Census Bureau & American Community Survey (ACS):</strong> County-level demographic, housing, employment, and income data from 2010-2024, with 5-year estimates used for reliability.</li>
    <li><strong>Vermont State Administrative Data:</strong> Department of Health (Adult Behavioral Risk Factor Surveillance Survey), Agency of Commerce and Community Development (tourism and relocation data), and other state datasets.</li>
    <li><strong>Community Listening Sessions:</strong> Qualitative themes from facilitated discussions with BIPOC community members in rural and urban Vermont.</li>
  </ul>
  <p><strong>Data Integration Approach:</strong> This project combines community-driven primary data with authoritative public datasets to provide both statistical rigor and authentic community voice. The quantitative data establishes baseline trends, while qualitative data provides context, nuance, and priorities that numbers alone cannot capture.</p>
</Modal>

<Modal open={activeModal === 'geographic-modal'} onclose={closeModal} title="Geographic Focus">
  <p><strong>Vermont's 14 Counties:</strong> Addison, Bennington, Caledonia, Chittenden, Essex, Franklin, Grand Isle, Lamoille, Orange, Orleans, Rutland, Washington, Windham, and Windsor.</p>
  <p><strong>Urban vs. Rural Distinction:</strong> Approximately 63% of Vermont's BIPOC population lives outside Chittenden County, predominantly in rural areas. This geographic distribution presents unique challenges for service delivery, community building, and data collection.</p>
  <p><strong>Why County-Level Analysis Matters:</strong></p>
  <ul>
    <li><strong>Policy Alignment:</strong> Vermont's Regional Development Corporations, legislative districts, and many state programs operate at county or regional levels.</li>
    <li><strong>Resource Distribution:</strong> Understanding where BIPOC Vermonters live helps target investments in housing, healthcare, transportation, and economic development.</li>
    <li><strong>Rural Visibility:</strong> Statewide aggregates often mask the experiences of rural BIPOC communities. County-level data makes these populations visible to decision-makers.</li>
    <li><strong>Comparative Context:</strong> County-level analysis allows comparison with similar rural counties nationally and regionally.</li>
  </ul>
  <p><strong>Methodological Note:</strong> When county-level sample sizes are too small (n&lt;30), we aggregate to regional groupings or present statewide trends only, always noting these limitations transparently.</p>
</Modal>

<Modal open={activeModal === 'inclusion-modal'} onclose={closeModal} title="Who We Include">
  <p><strong>BIPOC Definition:</strong> Black, Indigenous, and People of Color—a term that centers racial equity while acknowledging diverse experiences within and across communities.</p>
  <p><strong>Racial/Ethnic Categories Used:</strong></p>
  <ul>
    <li><strong>Black/African American:</strong> Includes individuals who identify as Black or African American, whether U.S.-born or immigrants from Africa, the Caribbean, or elsewhere.</li>
    <li><strong>Indigenous/Native American:</strong> Includes members of the Abenaki Nation and other Indigenous peoples with historical and contemporary ties to Vermont and the broader Northeast.</li>
    <li><strong>Latino/Hispanic:</strong> Individuals of Latin American descent, regardless of race, including diverse national origins (Mexican, Puerto Rican, Dominican, Central and South American, etc.).</li>
    <li><strong>Asian/Pacific Islander:</strong> Includes East Asian, South Asian, Southeast Asian, and Pacific Islander communities (Chinese, Indian, Filipino, Vietnamese, Nepalese, Bhutanese, and others).</li>
    <li><strong>Multiracial:</strong> Individuals who identify with two or more racial or ethnic backgrounds, reflecting Vermont's growing mixed-heritage population.</li>
  </ul>
  <p><strong>Why These Categories?</strong> We align with U.S. Census categories for comparability while recognizing their limitations. In qualitative work, we use self-identification and honor the specific cultural identities community members name for themselves.</p>
</Modal>

<Modal open={activeModal === 'limitations-modal'} onclose={closeModal} title="A Note on Limitations">
  <p><strong>Small Sample Sizes:</strong> Vermont's BIPOC population, while growing rapidly, remains relatively small in absolute numbers. This creates statistical challenges:</p>
  <ul>
    <li><strong>County-Level Data:</strong> Some counties have fewer than 100 BIPOC residents in certain categories, making reliable estimates difficult.</li>
    <li><strong>Suppression for Privacy:</strong> Following best practices, we suppress data when cell sizes are below 10 individuals to protect anonymity.</li>
    <li><strong>Confidence Intervals:</strong> Where possible, we report margins of error and confidence intervals to indicate uncertainty in estimates.</li>
    <li><strong>Aggregation:</strong> When sample sizes are too small for disaggregation, we combine counties into regions or present statewide totals only.</li>
  </ul>
  <p><strong>Methodological Transparency:</strong> We commit to clearly noting:</p>
  <ul>
    <li>Sample sizes and response rates</li>
    <li>Margins of error and statistical significance</li>
    <li>When data are suppressed or aggregated</li>
    <li>Differences between data sources and years</li>
    <li>Limitations in generalizability</li>
  </ul>
  <p><strong>Qualitative Strength:</strong> Where quantitative data is limited, qualitative insights from community surveys and listening sessions provide critical context and lived experience that numbers alone cannot capture.</p>
</Modal>

<style>
  /* Hook Section specific styles */
  .hook-section {
    background: linear-gradient(135deg, var(--color-navy, #25466A) 0%, #2a5a7a 100%);
    color: white;
    text-align: center;
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 80px 40px;
  }

  .hook-section .section-content {
    max-width: 800px;
    width: 100%;
  }

  .story-title {
    color: white;
    margin-bottom: 0.75rem;
    font-size: 3.8rem;
    font-weight: 700;
    line-height: 1.1;
  }

  .story-subtitle {
    font-size: 1.3rem;
    font-weight: 300;
    margin-bottom: 3rem;
    opacity: 0.9;
  }

  .hook-visual {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(200px, 1fr));
    gap: 2rem;
    margin: 3rem 0;
    padding: 2rem 0;
  }

  .hook-text {
    font-size: 1.2rem;
    margin: 2rem 0;
    line-height: 1.8;
    max-width: 700px;
    margin-left: auto;
    margin-right: auto;
    color: white;
  }

  .scroll-indicator {
    margin-top: 3rem;
    font-size: 1rem;
    animation: bounce 2s infinite;
  }

  @keyframes bounce {
    0%, 100% { transform: translateY(0); }
    50% { transform: translateY(10px); }
  }

  /* Question Section styles */
  .question-content {
    font-size: 1.1rem;
    line-height: 1.8;
  }

  .question-content p {
    margin-bottom: 1.2rem;
    color: #444;
  }

  .question-content h4 {
    color: var(--color-navy, #25466A);
    margin-top: 2rem;
    margin-bottom: 1rem;
    font-size: 1.3rem;
  }

  .question-list {
    list-style: none;
    margin: 2.5rem 0;
    padding-left: 0;
  }

  .question-list li {
    margin: 1.5rem 0;
    padding-left: 2.5rem;
    position: relative;
    font-size: 1.05rem;
    line-height: 1.7;
  }

  .question-list li:before {
    content: "•";
    position: absolute;
    left: 0.5rem;
    color: var(--color-gold, #F6BD32);
    font-weight: bold;
    font-size: 1.2rem;
  }

  .question-emphasis {
    font-style: italic;
    background: #f0f8ff;
    padding: 1.5rem;
    border-left: 4px solid var(--color-gold, #F6BD32);
    margin: 2rem 0;
    border-radius: 4px;
    color: var(--color-navy, #25466A);
  }

  .question-content p.question-callout {
    background: var(--color-navy, #25466A);
    color: white;
    padding: 2rem;
    margin: 2rem 0;
    border-radius: 4px;
    border-left: 4px solid var(--color-gold, #F6BD32);
  }

  /* Context grid */
  .context-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 2rem;
    margin-top: 2rem;
  }

  /* Exploration styles */
  .exploration-item {
    margin: 3rem 0;
    padding: 3rem 0;
    border-top: 2px solid #e5e5e5;
  }

  .exploration-item:first-of-type {
    border-top: none;
    padding-top: 2rem;
  }

  .exploration-text h4 {
    color: var(--color-navy, #25466A);
    font-size: 1.8rem;
    margin-bottom: 1rem;
    font-weight: 700;
  }

  .exploration-text p {
    font-size: 1.05rem;
    color: #555;
    line-height: 1.7;
  }

  .exploration-viz {
    background: #fafafa;
    padding: 2rem;
    border-radius: 4px;
    border-left: 4px solid var(--color-gold, #F6BD32);
  }

  .sample-chart {
    width: 100%;
    height: auto;
    max-height: 350px;
  }

  /* Recommendations */
  .recommendations-container {
    margin: 3rem 0;
    position: relative;
  }

  .timeline-item {
    display: grid;
    grid-template-columns: auto 1fr;
    gap: 2.5rem;
    margin-bottom: 2.5rem;
    position: relative;
  }

  .timeline-item:not(:last-child)::after {
    content: '';
    position: absolute;
    left: 21px;
    top: 60px;
    width: 2px;
    height: calc(100% + 2.5rem);
    background: #e5e5e5;
  }

  .timeline-marker {
    width: 44px;
    height: 44px;
    background: var(--color-navy, #25466A);
    color: white;
    border-radius: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    font-weight: bold;
    font-size: 1.1rem;
    flex-shrink: 0;
    position: relative;
    z-index: 1;
  }

  .timeline-content {
    padding: 1.5rem;
    background: white;
    border-top: 1px solid #e5e5e5;
  }

  .timeline-content h4 {
    color: #1a1a1a;
    margin-bottom: 0.75rem;
    font-size: 1.15rem;
    font-weight: 500;
  }

  .timeline-content p {
    color: #444;
    font-size: 1rem;
    margin: 0;
    line-height: 1.7;
  }

  /* Action section */
  .action-section {
    margin-top: 4rem;
    padding: 3rem 0;
  }

  .action-section h3 {
    text-align: center;
    color: var(--color-navy, #25466A);
  }

  .action-intro {
    text-align: center;
    font-size: 1.15rem;
    color: #2a5a7a;
    max-width: 700px;
    margin: 0 auto 3rem;
    line-height: 1.7;
  }

  .action-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(300px, 1fr));
    gap: 2rem;
    margin-top: 2rem;
  }

  .newsletter-wrapper {
    margin-top: 4rem;
  }

  /* Share section */
  .share-section {
    margin-top: 4rem;
    padding: 2rem 0;
    text-align: center;
  }

  .share-section h3 {
    margin-bottom: 1rem;
    color: var(--color-navy, #25466A);
  }

  .share-section > p {
    color: #4b5563;
    max-width: 600px;
    margin: 0 auto 2rem;
  }

  /* CTA section */
  .cta-section {
    margin-top: 4rem;
    padding: 3rem 2rem;
    background: var(--color-navy, #25466A);
    color: white;
    text-align: center;
  }

  .cta-section h3 {
    color: var(--color-gold, #F6BD32);
    margin-bottom: 1.5rem;
  }

  .cta-section p {
    margin-bottom: 1.5rem;
    color: #f0f8ff;
    font-size: 1.05rem;
  }

  .cta-button {
    display: inline-block;
    background: var(--color-gold, #F6BD32);
    color: var(--color-navy, #25466A);
    padding: 1rem 2rem;
    border-radius: 8px;
    font-weight: 700;
    text-decoration: none;
    transition: all 0.2s ease;
  }

  .cta-button:hover {
    background: #f4b035;
    transform: translateY(-2px);
  }

  /* Responsive */
  @media (max-width: 768px) {
    .story-title {
      font-size: 2.4rem;
    }

    .hook-visual {
      grid-template-columns: 1fr;
    }

    .action-grid {
      grid-template-columns: 1fr;
    }
  }

  @media (prefers-reduced-motion: reduce) {
    * {
      animation-duration: 0.01ms !important;
      animation-iteration-count: 1 !important;
      transition-duration: 0.01ms !important;
    }
  }
</style>
