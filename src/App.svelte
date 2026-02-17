<script lang="ts">
  import Layout from './lib/Layout.svelte';
  import Section from './lib/Section.svelte';
  import StatBlock from './lib/StatBlock.svelte';
  import ContextCard from './lib/ContextCard.svelte';
  import ActionCard from './lib/ActionCard.svelte';
  import ShareButtons from './lib/ShareButtons.svelte';
  import Newsletter from './lib/Newsletter.svelte';
  import Modal from './lib/Modal.svelte';
  import InsightBlock from './lib/InsightBlock.svelte';
  import DataSuppressionChart from './lib/charts/DataSuppressionChart.svelte';
  import GapChart from './lib/charts/GapChart.svelte';

  import ImpactMetrics from './lib/charts/ImpactMetrics.svelte';

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
      <h1 class="story-title">The State Is Changing</h1>
      <p class="story-subtitle">Vermont's economic future depends on communities we've yet to fully see</p>
      <div class="hook-visual">
        <StatBlock value={12} label="BIPOC population in Vermont" />
        <StatBlock value={40} label="Growth since 2010" />
      </div>
      <p class="hook-text">Vermont's national reputation rests on an outdated narrative. While total population stagnates and the state ages, Black, Asian, Hispanic, and multiracial households are surging—driving workforce renewal and economic stabilization. Yet policy, investment, and data systems have not kept pace with this demographic reality.</p>
      <div class="scroll-indicator">Scroll to explore ↓</div>
    </div>
  </section>

  <!-- QUESTION SECTION -->
  <Section id="question" variant="question" title="The Growth Carrying the Economy" subtitle="Why demographic change is economic infrastructure">
    <div class="question-content">
      <p><strong>Vermont's demographic renewal is not symbolic—it is structural.</strong> While the state's overall population declined by 1.2% between 2010 and 2024, the BIPOC population surged from 4.7% to 8.59% of Vermont's total—an 82.7% relative growth. More critically, BIPOC residents are concentrated in working age and younger cohorts—the exact demographics Vermont needs to stabilize its labor force and tax base.</p>

      <p>This is not a social equity issue alone. This is an economic infrastructure problem. Communities that were numerically invisible a decade ago are now foundational to Vermont's economic future.</p>

      <h4>The Economic Reality:</h4>
      <ul class="question-list">
        <li><strong>Labor Force Participation:</strong> BIPOC Vermonters comprise a growing share of working-age residents. Their economic participation directly impacts total productivity and tax revenue.</li>
        <li><strong>Business Ownership:</strong>  BIPOC entrepreneurs grew businesses at _______ between 2017-2024—outpacing overall business growth. This is new economic capacity, not displacement.</li>
        <li><strong>Household Formation:</strong> BIPOC household formation is driving demand for housing, services, and infrastructure investment—key to economic cycles..</li>
        <li><strong>School Enrollment:</strong> BIPOC students now represent _____ of Vermont school enrollment, up from ____ in 2010. This shapes workforce pipeline and future labor supply.</li>
        <li><strong>Geographic Distribution:</strong> While concentrated in urban areas, BIPOC Vermonters are increasingly visible in rural counties—expanding labor availability where it is most needed.</li>
      </ul>

      <p class="question-callout">The question is not whether BIPOC communities will shape Vermont's future. They already are. The question is whether institutions will align investments, data systems, and policy with that reality.</p>
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

  <!-- VISIBILITY GAP SECTION -->
  <Section id="visibility" variant="exploration" title="The Visibility Gap" subtitle="You cannot govern what you cannot see">
    <div class="implication-intro">
      <p>Vermont's data infrastructure has not adapted at the pace of demographic change. Policymakers are making decisions about the state's future with incomplete visibility into the communities reshaping it.</p>
    </div>

    <!-- Data Gap 1: Suppression -->
    <div class="exploration-item">
      <div class="exploration-text">
        <h4>Data Suppression & Small Sample Sizes</h4>
        <p>Vermont's small BIPOC population in many counties triggers automatic data suppression to protect privacy. This means county-level insights—exactly where rural policymakers need to invest—remain invisible. Aggregate statewide numbers mask where problems and opportunities actually exist.</p>
      </div>
      <div class="exploration-viz">
        <DataSuppressionChart />
      </div>
    </div>

    <!-- Data Gap 2: Aggregation -->
    <div class="exploration-item">
      <div class="exploration-text">
        <h4>Overly Broad Racial Categories</h4>
        <p>Aggregating "Asian/Pacific Islander" or "Latino/Hispanic" erases crucial variation. A Nepalese immigrant faces different barriers than a Taiwanese business owner. Puerto Rican workers experience different labor market realities than Mexican agricultural workers. Collapsed categories hide where targeted policy works.</p>
      </div>
    </div>

    <!-- Data Gap 3: Rural Invisibility -->
    <div class="exploration-item">
      <div class="exploration-text">
        <h4>Rural BIPOC Communities Are Unmapped</h4>
        <p>State data often uses "urban/rural" splits that don't cross-tabulate with race/ethnicity. The result: rural BIPOC Vermonters are statistically flattened into the general rural population, making their specific barriers and assets invisible in policy conversations.</p>
      </div>
    </div>

    <!-- Data Gap 4: Inconsistent Reporting -->
    <div class="exploration-item">
      <div class="exploration-text">
        <h4>Inconsistent Reporting Across Agencies</h4>
        <p>Different state agencies use different racial/ethnic definitions, timeframes, and reporting intervals. Housing data uses different categories than workforce data, which differ from education data. This fragmentation makes statewide policy alignment impossible.</p>
      </div>
    </div>

    <!-- Impact callout -->
    <div class="implication-summary">
      <p><strong>The Result:</strong> When communities are statistically flattened, investment decisions follow incomplete assumptions. Policymakers cannot invest in solutions they cannot measure or locate geographically. This isn't a research problem—it's an economic planning crisis.</p>
    </div>

  </Section>

  <!-- FRICTION SECTION -->
  <Section id="friction" variant="insight" title="Where Friction Emerges" subtitle="Growth without alignment creates economic drag">
    <div class="insight-intro">
      <p>Demographic growth alone does not guarantee economic stability. When labor force capacity exists but systemic barriers limit participation, the result is lost productivity, stagnant incomes, and economic drag that affects all of Vermont. Here's where barriers become fiscal problems.</p>
    </div>

    <!-- Friction Point 1: Housing -->
    <InsightBlock
      number="01"
      title="Housing Gaps Limit Wealth Building"
      tagline="20-point homeownership gap = lost tax base and economic mobility"
      takeaway="Homeownership barriers reduce residential property tax revenue and limit household wealth accumulation. Closing this gap would increase Vermont's tax base while enabling BIPOC Vermonters to participate in wealth building."
    >
      <GapChart
        title="Homeownership & Economic Participation"
        bars={[
          { label: "White", value: 72, displayValue: "72%", color: "#1a3a52" },
          { label: "BIPOC", value: 52, displayValue: "52%", color: "#F4D35E" }
        ]}
        gapLabel="20-pt gap"
        gapPosition={{ from: 0, to: 1 }}
        impactText="Lower tax base • Reduced investment in home improvements • Limited inter-generational wealth transfer • Increased housing instability"
      />
    </InsightBlock>

    <!-- Friction Point 2: Wages -->
    <InsightBlock
      number="02"
      title="Wage Disparities Reduce Economic Capacity"
      tagline="18% wage gap = $180M+ in lost annual purchasing power"
      takeaway="When equally-qualified BIPOC workers earn less, Vermont loses consumer spending, tax revenue, and workforce retention. This is not a sentiment issue—it's a demand-side economic problem. A worker earning $10K less annually spends that $10K less at Vermont businesses, pays less in taxes, and is more likely to relocate to higher-wage markets."
    >
    </InsightBlock>

    <!-- Friction Point 3: Access to Capital -->
    <InsightBlock
      number="03"
      title="Capital Access Barriers Limit Business Scale"
      tagline="BIPOC businesses grow fast but stay small—untapped economic potential"
      takeaway="BIPOC-owned businesses grew 145% between 2017–2024 but remain heavily concentrated in lower-margin sectors. Limited access to growth capital means these businesses cannot scale, hire more workers, or contribute to downstream economic activity. Vermont is leaving growth on the table by not investing in scaling these enterprises."
    />

    <!-- Friction Point 4: Workforce Retention -->
    <InsightBlock
      number="04"
      title="Economic Climate Drives Out-Migration"
      tagline="When barriers persist, BIPOC workers leave for more aligned states"
      takeaway="Young BIPOC professionals and entrepreneurs have options. If homeownership is inaccessible, wages are depressed, and services are sparse, higher-income BIPOC workers will relocate to states with better alignment. Vermont cannot afford to lose the demographic cohort it depends on most."
    />
  </Section>

  <!-- ECONOMIC SCENARIO SECTION -->
  <Section id="scenario" variant="implication" title="The Economic Opportunity Scenario" subtitle="Alignment produces return">
    <div class="implication-intro">
      <p>Demographic change is not a choice—it's happening. The economic outcome is. Strategy determines whether Vermont captures the growth BIPOC communities represent or leaves it on the table. Here are three fiscally conservative scenarios.</p>
    </div>



    <!-- Scenario 1: Housing Alignment -->
    <div class="implication-major">
      <h4>Scenario 1: Close the Homeownership Gap by 50%</h4>
      <p class="implication-description">What if targeted lending programs, discrimination training, and down-payment assistance closed the homeownership gap from 20 points to 10 points over 5 years?</p>
      <ImpactMetrics
        title="5-Year Economic Impact"
        layout="grid"
        metrics={[
          { label: "New BIPOC Homeowners", value: "~3,500" },
          { label: "Estimated Property Tax Revenue", value: "+$42M" },
          { label: "Home Improvement Investment", value: "+$175M" },
          { label: "Construction Job Creation", value: "+280 jobs" }
        ]}
      />
    </div>

    <!-- Scenario 2: Wage Alignment -->
    <div class="implication-major">
      <h4>Scenario 2: Narrow the Wage Gap by 50%</h4>
      <p class="implication-description">What if targeted recruiting, explicit anti-discrimination audits, and professional development closed the wage gap from 18% to 9%?</p>
      <ImpactMetrics
        title="Annual Economic Impact"
        layout="grid"
        metrics={[
          { label: "BIPOC Workers Affected", value: "~8,200" },
          { label: "Annual Wage Increase", value: "+$96M" },
          { label: "Increased Tax Revenue", value: "+$12.8M" },
          { label: "Consumer Spending Increase", value: "+$85M" }
        ]}
      />
    </div>

    <!-- Scenario 3: Capital Access -->
    <div class="implication-major">
      <h4>Scenario 3: Scale BIPOC Business Growth</h4>
      <p class="implication-description">What if targeted small business capital, technical assistance, and procurement preferences enabled 50% of BIPOC businesses to scale to next level?</p>
      <ImpactMetrics
        title="5-Year Economic Impact"
        layout="grid"
        metrics={[
          { label: "Businesses Scaled", value: "~350" },
          { label: "New Jobs Created", value: "~1,200" },
          { label: "Total Economic Activity", value: "+$385M" },
          { label: "Tax Revenue (5 years)", value: "+$48M" }
        ]}
      />
    </div>

    <!-- Combined Impact -->
    <div class="implication-summary">
      <p><strong>Combined Economic Impact:</strong> If Vermont implements all three scenarios, the state generates $186M+ in new tax revenue over 5 years while creating 1,500+ jobs and expanding the consumer base. The investment required is far less than the return. This is fiscal strategy, not charity. The question is not whether Vermont can afford to invest in equity. It is whether Vermont can afford not to.</p>
    </div>
  </Section>

  <!-- POLICY IMPERATIVE SECTION -->
  <Section id="policy" variant="recommendation" title="The Policy Imperative" subtitle="Vermont cannot afford data blind spots">
    <div class="recommendations-container">
      <div class="timeline-item">
        <div class="timeline-marker"><span>1</span></div>
        <div class="timeline-content">
          <h4>Invest in Improved Demographic Data Infrastructure</h4>
          <p><strong>Action:</strong> Fund statewide effort to standardize racial/ethnic data collection across agencies (Housing Finance Agency, Department of Labor, Department of Health, etc.) with detailed geographic and disaggregated categories.</p>
          <p><strong>Fiscal Impact:</strong> ~$2M initial investment, &lt;$500K annually. ROI: Enables targeted investment decisions worth $100M+.</p>
        </div>
      </div>

      <div class="timeline-item">
        <div class="timeline-marker"><span>2</span></div>
        <div class="timeline-content">
          <h4>Implement Equity-Centered Housing & Capital Strategies</h4>
          <p><strong>Actions:</strong> (1) Expand down-payment assistance for BIPOC homebuyers through VT Housing Finance Agency with explicit equity targets. (2) Create targeted small business lending fund for BIPOC entrepreneurs with flexible underwriting. (3) Remove barriers in procurement contracting that disadvantage BIPOC-owned firms.</p>
          <p><strong>Fiscal Impact:</strong> ~$15M initial capital yield $42M+ in tax revenue within 5 years based on homeownership scenario.</p>
        </div>
      </div>

      <div class="timeline-item">
        <div class="timeline-marker"><span>3</span></div>
        <div class="timeline-content">
          <h4>Build Standardized Reporting Requirements</h4>
          <p><strong>Action:</strong> Require all state agencies, nonprofits receiving state funds, and private sector partners (through tax incentives) to report annual demographic outcomes by race/ethnicity aligned to statewide definitions.</p>
          <p><strong>Fiscal Impact:</strong> ~$1M to establish reporting infrastructure. Creates accountability loop for Vermont's BIPOC economic participation.</p>
        </div>
      </div>

      <div class="timeline-item">
        <div class="timeline-marker"><span>4</span></div>
        <div class="timeline-content">
          <h4>Modernize Workforce Development & Hiring</h4>
          <p><strong>Actions:</strong> (1) Integrate BIPOC demographic tracking into Vermont Department of Labor workforce training pipeline. (2) Make equity hiring metrics a requirement for state contracts and tax incentives. (3) Fund cultural competency training for educators, healthcare workers, and government staff.</p>
          <p><strong>Fiscal Impact:</strong> Built into existing budgets with reallocation. Strategic hiring yields higher retention and productivity worth ~$10M over 5 years.</p>
        </div>
      </div>
    </div>

    <!-- Closing Statement -->
    <div class="implication-summary">
      <p><strong>The Future Is Here:</strong> Vermont's BIPOC workforce, entrepreneurs, and families are not hypothetical—they are building the state's future right now. The investments outlined above are not charity. They are fiscal strategy to capture demographic growth worth $180M+ in tax revenue over 5 years while stabilizing a labor force that supports all of Vermont's economy. Demographic change is underway. Policy alignment determines whether it stabilizes or strains Vermont's future.</p>
    </div>

    <div class="cta-section policy-cta">
      <h3>For Policymakers & Institutional Leaders</h3>
      <p>This analysis is a foundation. Your action determines outcomes. Data exists. The question is whether Vermont's policy and investment infrastructure will align with the demographic reality that is already here. The future workforce is already here. The future taxpayers are already here. The future entrepreneurs are already here. The data, policy, and investment must catch up.</p>
      <a href="https://www.vtpoc.net/contact-us/" class="cta-button" target="_blank" rel="noopener noreferrer">Download Full Report & Policy Recommendations →</a>
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
    font-size: 1rem;
    font-weight: 300;
    margin-bottom: 3rem;
    color: var(--color-gold, #F6BD32);
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

  /* Implication & Insight section styles */
  .implication-intro,
  .insight-intro {
    font-size: 1.15rem;
    line-height: 1.8;
    color: #444;
    margin-bottom: 2rem;
    padding: 1.5rem;
    background: #f9fafb;
    border-radius: 8px;
  }

  .implication-intro p,
  .insight-intro p {
    margin: 0;
  }

  .implication-summary {
    background: var(--color-navy, #25466A);
    color: white;
    padding: 2rem;
    border-radius: 8px;
    margin: 3rem 0;
  }

  .implication-summary p {
    margin: 0;
    font-size: 1.1rem;
    line-height: 1.8;
  }

  .implication-summary strong {
    color: var(--color-gold, #F4D35E);
  }

  .implication-major {
    margin: 3rem 0;
    padding: 2rem 0;
    border-bottom: 1px solid #e5e5e5;
  }

  .implication-major:last-of-type {
    border-bottom: none;
  }

  .implication-major h4 {
    color: var(--color-navy, #25466A);
    font-size: 1.4rem;
    margin-bottom: 0.75rem;
    font-weight: 600;
  }

  .implication-description {
    color: #555;
    font-size: 1.05rem;
    line-height: 1.7;
    margin-bottom: 1.5rem;
  }

  .policy-cta {
    margin-top: 3rem;
    border-radius: 8px;
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
