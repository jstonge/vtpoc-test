<script lang="ts">
  import { onMount } from 'svelte';

  interface Props {
    open: boolean;
    onclose: () => void;
    title: string;
    children?: import('svelte').Snippet;
  }

  let { open, onclose, title, children }: Props = $props();

  function handleBackdropClick(e: MouseEvent) {
    if ((e.target as HTMLElement).classList.contains('modal')) {
      onclose();
    }
  }

  function handleKeydown(e: KeyboardEvent) {
    if (e.key === 'Escape' && open) {
      onclose();
    }
  }

  $effect(() => {
    if (open) {
      document.body.style.overflow = 'hidden';
      document.addEventListener('keydown', handleKeydown);
    } else {
      document.body.style.overflow = 'auto';
    }

    return () => {
      document.body.style.overflow = 'auto';
      document.removeEventListener('keydown', handleKeydown);
    };
  });
</script>

{#if open}
  <!-- svelte-ignore a11y_click_events_have_key_events -->
  <!-- svelte-ignore a11y_no_noninteractive_element_interactions -->
  <div class="modal" onclick={handleBackdropClick} role="dialog" aria-modal="true" aria-labelledby="modal-title">
    <div class="modal-content">
      <button class="modal-close" onclick={onclose} aria-label="Close modal">&times;</button>
      <h3 id="modal-title">{title}</h3>
      {@render children?.()}
    </div>
  </div>
{/if}

<style>
  .modal {
    position: fixed;
    z-index: 1000;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    overflow: auto;
    background-color: rgba(26, 58, 82, 0.8);
    backdrop-filter: blur(4px);
  }

  .modal-content {
    background-color: white;
    margin: 5% auto;
    padding: 3rem;
    border-top: 4px solid var(--color-gold, #F6BD32);
    width: 90%;
    max-width: 800px;
    border-radius: 8px;
    box-shadow: 0 4px 24px rgba(0, 0, 0, 0.2);
  }

  .modal-close {
    color: var(--color-navy, #25466A);
    float: right;
    font-size: 2rem;
    font-weight: bold;
    background: none;
    border: none;
    cursor: pointer;
    transition: color 0.3s ease;
  }

  .modal-close:hover {
    color: var(--color-gold, #F6BD32);
  }

  .modal-content h3 {
    color: var(--color-navy, #25466A);
    margin-top: 0;
    margin-bottom: 1.5rem;
    font-size: 1.8rem;
  }

  .modal-content :global(p) {
    line-height: 1.7;
    margin-bottom: 1rem;
    color: #333;
  }

  .modal-content :global(ul) {
    margin: 1rem 0 1.5rem 1.5rem;
    line-height: 1.8;
  }

  .modal-content :global(li) {
    margin-bottom: 0.8rem;
    color: #333;
  }
</style>
