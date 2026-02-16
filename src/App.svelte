<script lang="ts">
  import Scrolly from './lib/Scrolly.svelte'
  import ScrollyPlot from './lib/ScrollyPlot.svelte'
  import DebugTooltip from './lib/DebugTooltip.svelte'
  import data from './copy.json'

  let scrollyIndex = $state(undefined);

  // Debug mode - set to false in production
  const DEBUG_ZINDEX = true;
</script>

<article class="vtpoc-story">
  <h1>Scrolly App</h1>
  <p>A scrollytelling demo built with <a href="https://svelte.dev/">Svelte</a> and <a href="https://d3js.org/">D3.js</a>. Scroll through to see how the visualization responds to each step - sorting data, changing chart types, and adapting to your screen.</p>
  <p> I left a little tooltip widget to test whether there will be z-index conflict inbetween the app and the worpress site. We should also be mindful of the styling, as already i could see some of the vanilla local styling was being overriden by the global wordpress preferences.</p>

  <section id="scrolly" class="vtpoc-split-layout">
		<div class="vtpoc-sticky-panel">
			<ScrollyPlot {scrollyIndex} />
		</div>

    <div class="vtpoc-scrolly-content">
		<div class="vtpoc-scrolly-inner-content">
      <div class="vtpoc-spacer"></div>
        <Scrolly bind:value={scrollyIndex}>
            {#each data.steps as step, i}
                {@const active = scrollyIndex === i}
                <div class="vtpoc-step" class:active>
                    <div class="vtpoc-step-box">
                        {@html step.value}
                    </div>
                </div>
            {/each}
        </Scrolly>
        <div class="vtpoc-spacer"></div>
      </div>
    </div>
	</section>

</article>

<DebugTooltip enabled={DEBUG_ZINDEX} />

<style>
  .vtpoc-story {
    --vtpoc-panel-top-offset: calc((100vh - var(--vtpoc-panel-height)) / 2);
    --vtpoc-panel-height: min(80vh, 600px);
    --vtpoc-panel-min-width: 450px;
    --vtpoc-panel-width: 65%;
    --vtpoc-layout-gap: 2rem;
    --vtpoc-content-padding-inline: 2rem;
    --vtpoc-content-max-width: 400px;
    --vtpoc-story-max-width: 600px;
    --vtpoc-space-md: 1rem;

    width: 100%;
    padding-top: 5.5rem;
    padding-bottom: 7.5rem;
  }

  @media (max-width: 768px) {
    .vtpoc-story {
      padding-top: 0rem;
    }
  }

  .vtpoc-story > h1,
  .vtpoc-story > p,
  .vtpoc-story > section {
    width: 100%;
    max-width: var(--vtpoc-story-max-width);
    margin-inline: auto;
    padding-inline: var(--vtpoc-space-md);
  }

  .vtpoc-story p {
    text-align: left;
  }

  .vtpoc-split-layout {
    position: relative;
    display: grid;
    grid-template-columns: 1fr minmax(var(--vtpoc-panel-min-width), var(--vtpoc-panel-width));
    gap: var(--vtpoc-layout-gap);
    align-items: start;
    padding-inline: var(--vtpoc-content-padding-inline, 2rem);
    --vtpoc-content-max-width: none;
  }

  .vtpoc-story > .vtpoc-split-layout {
    max-width: none;
    padding-inline: 0;
  }

  .vtpoc-split-layout .vtpoc-sticky-panel {
    position: sticky;
    top: var(--vtpoc-panel-top-offset);
    height: var(--vtpoc-panel-height);
    grid-column: 2;
    display: flex;
    align-items: center;
    justify-content: center;
  }

  .vtpoc-split-layout .vtpoc-scrolly-content {
    grid-column: 1;
    margin: 0;
  }

  .vtpoc-scrolly-inner-content {
    position: relative;
    z-index: 2;
    pointer-events: none;
  }

  .vtpoc-spacer {
    height: 65vh;
  }

  .vtpoc-step-box {
    width: 100%;
    max-width: 400px;
    padding: 1rem;
    background-color: #f5f5f5;
    color: #ccc;
    border-radius: 5px;
    box-shadow: 1px 1px 10px rgba(0, 0, 0, 0.2);
    transition: background-color 400ms ease, color 400ms ease;
    text-align: center;
    pointer-events: auto;
  }

  .vtpoc-step {
    min-height: 90vh;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 1rem;
  }

  .vtpoc-step.active .vtpoc-step-box {
    background-color: #fff;
    color: #333;
  }

  @media (max-width: 768px) {
    .vtpoc-split-layout {
      grid-template-columns: 1fr;
      padding-inline: 0;
      --vtpoc-step-max-width: 100%;
      max-width: 100vw;
      overflow-x: clip;
    }

    .vtpoc-split-layout .vtpoc-sticky-panel {
      position: sticky;
      top: 0;
      height: 100vh;
      grid-column: 1;
      grid-row: 1;
      width: 100%;
      min-width: 0;
      z-index: 0;
      display: flex;
      align-items: center;
      justify-content: center;
    }

    .vtpoc-split-layout .vtpoc-scrolly-content {
      grid-column: 1;
      grid-row: 1;
      z-index: 1;
      pointer-events: none;
      padding-inline: 0.5rem;
    }
  }
</style>