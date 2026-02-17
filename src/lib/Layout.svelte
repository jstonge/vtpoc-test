<script lang="ts">
  import { onMount } from 'svelte';
  import type { Snippet } from 'svelte';
  import Header from './Header.svelte';
  import Footer from './Footer.svelte';

  interface Props {
    children: Snippet;
  }

  let { children }: Props = $props();

  let scrollProgress = $state(0);

  onMount(() => {
    const updateProgress = () => {
      const scrollPercentage = (window.scrollY / (document.documentElement.scrollHeight - window.innerHeight)) * 100;
      scrollProgress = scrollPercentage;
    };

    window.addEventListener('scroll', updateProgress);
    return () => window.removeEventListener('scroll', updateProgress);
  });
</script>

<div id="scroll-progress" style="width: {scrollProgress}%"></div>

<Header />

<main class="scroll-container">
  {@render children()}
</main>

<Footer />

<style>
  :global(#scroll-progress) {
    position: fixed;
    top: 0;
    left: 0;
    height: 4px;
    background: linear-gradient(90deg, var(--color-gold, #F6BD32) 0%, var(--color-navy, #25466A) 100%);
    z-index: 9999;
    transition: width 0.2s ease;
  }

  .scroll-container {
    width: 100%;
    overflow-x: hidden;
  }
</style>
