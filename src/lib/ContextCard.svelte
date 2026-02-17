<script lang="ts">
  interface Props {
    title: string;
    description: string;
    onlearnmore?: () => void;
  }

  let { title, description, onlearnmore }: Props = $props();
</script>

<div class="context-card">
  <h4>{title}</h4>
  <p>{description}</p>
  {#if onlearnmore}
    <button class="learn-more-link" onclick={onlearnmore}>Learn More →</button>
  {/if}
</div>

<style>
  .context-card {
    background: #fafafa;
    padding: 2.5rem;
    border-left: 3px solid var(--color-gold, #F6BD32);
    transition: background 0.3s ease;
  }

  .context-card:hover {
    background: #f5f5f5;
  }

  .context-card h4 {
    color: var(--color-navy, #25466A);
    margin-bottom: 1rem;
    font-size: 1.15rem;
    font-weight: 500;
  }

  .context-card p {
    color: #555;
    font-size: 1rem;
    margin: 0;
    line-height: 1.65;
  }

  .learn-more-link {
    display: inline-block;
    margin-top: 1rem;
    color: var(--color-navy, #25466A);
    font-weight: 600;
    background: none;
    border: none;
    cursor: pointer;
    font-size: 0.95rem;
    padding: 0;
    transition: color 0.3s ease;
  }

  .learn-more-link:hover {
    color: var(--color-gold, #F6BD32);
  }
</style>
