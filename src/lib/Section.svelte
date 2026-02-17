<script lang="ts">
  import type { Snippet } from 'svelte';

  interface Props {
    id: string;
    variant?: 'hook' | 'question' | 'context' | 'exploration' | 'insight' | 'implication' | 'recommendation';
    title?: string;
    subtitle?: string;
    children: Snippet;
  }

  let { id, variant = 'question', title, subtitle, children }: Props = $props();
</script>

<section {id} class="story-section {variant}-section">
  <div class="section-content">
    {#if title}
      <h2 class="section-title">{title}</h2>
    {/if}
    {#if subtitle}
      <h3 class="section-subtitle">{subtitle}</h3>
    {/if}
    {@render children()}
  </div>
</section>

<style>
  .story-section {
    min-height: 100vh;
    display: flex;
    align-items: center;
    justify-content: center;
    padding: 80px 40px;
    position: relative;
    overflow: hidden;
  }

  .section-content {
    max-width: 800px;
    width: 100%;
  }

  .section-title {
    color: var(--color-navy, #25466A);
    margin-bottom: 0.5rem;
    font-size: 2.8rem;
    font-weight: 400;
  }

  .section-subtitle {
    color: #666;
    font-weight: 400;
    font-size: 1.2rem;
    margin-bottom: 2.5rem;
  }

  /* Variant styles */
  .hook-section {
    background: linear-gradient(135deg, var(--color-navy, #25466A) 0%, #2a5a7a 100%);
    color: white;
    text-align: center;
  }

  .hook-section .section-title {
    color: white;
  }

  .question-section {
    background-color: #fff;
    color: #333;
  }

  .context-section {
    background-color: #f9fafb;
  }

  .exploration-section {
    background-color: white;
  }

  .insight-section {
    background: white;
  }

  .implication-section {
    background: #f9fafb;
  }

  .recommendation-section {
    background: #ffffff;
  }

  @media (max-width: 768px) {
    .story-section {
      min-height: auto;
      padding: 50px 20px;
    }

    .section-title {
      font-size: 2rem;
    }
  }
</style>
