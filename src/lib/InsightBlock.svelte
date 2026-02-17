<script lang="ts">
  import type { Snippet } from 'svelte';

  interface Props {
    number: string;
    title: string;
    tagline: string;
    takeaway: string;
    takeawayLabel?: string;
    children?: Snippet;
  }

  let { number, title, tagline, takeaway, takeawayLabel = "Economic Problem", children }: Props = $props();
</script>

<div class="insight-major">
  <div class="insight-header">
    <span class="insight-number">{number}</span>
    <div>
      <h3>{title}</h3>
      <p class="insight-tagline">{tagline}</p>
    </div>
  </div>

  {#if children}
    <div class="insight-viz-container">
      {@render children()}
    </div>
  {/if}

  <div class="insight-takeaway">
    <strong>{takeawayLabel}:</strong> {takeaway}
  </div>
</div>

<style>
  .insight-major {
    margin: 3rem 0;
    padding: 2rem 0;
    border-bottom: 1px solid #e5e5e5;
  }

  .insight-major:last-child {
    border-bottom: none;
  }

  .insight-header {
    display: flex;
    align-items: flex-start;
    gap: 1.5rem;
    margin-bottom: 1.5rem;
  }

  .insight-number {
    display: flex;
    align-items: center;
    justify-content: center;
    width: 50px;
    height: 50px;
    background: var(--color-navy, #25466A);
    color: white;
    border-radius: 50%;
    font-size: 1.2rem;
    font-weight: bold;
    flex-shrink: 0;
  }

  .insight-header h3 {
    color: var(--color-navy, #25466A);
    font-size: 1.4rem;
    margin: 0 0 0.25rem 0;
    font-weight: 600;
  }

  .insight-tagline {
    color: #c64226;
    font-size: 1rem;
    margin: 0;
    font-weight: 500;
  }

  .insight-viz-container {
    margin: 2rem 0;
  }

  .insight-takeaway {
    background: #f9fafb;
    padding: 1.5rem;
    border-left: 4px solid var(--color-gold, #F4D35E);
    border-radius: 0 8px 8px 0;
    font-size: 1rem;
    line-height: 1.7;
    color: #444;
  }

  .insight-takeaway strong {
    color: var(--color-navy, #25466A);
  }
</style>
