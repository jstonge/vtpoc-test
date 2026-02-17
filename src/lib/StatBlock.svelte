<script lang="ts">
  import { onMount } from 'svelte';

  interface Props {
    value: number;
    label: string;
    suffix?: string;
    animate?: boolean;
    duration?: number;
  }

  let { value, label, suffix = '%', animate = true, duration = 2000 }: Props = $props();

  let displayValue = $state(animate ? 0 : value);
  let hasAnimated = $state(false);
  let element: HTMLElement;

  function animateNumber(start: number, end: number, dur: number) {
    const range = end - start;
    const increment = range / (dur / 16);
    let current = start;

    const timer = setInterval(() => {
      current += increment;
      if (current >= end) {
        displayValue = end;
        clearInterval(timer);
      } else {
        displayValue = Math.floor(current);
      }
    }, 16);
  }

  onMount(() => {
    if (!animate) return;

    const observer = new IntersectionObserver(
      (entries) => {
        entries.forEach((entry) => {
          if (entry.isIntersecting && !hasAnimated) {
            hasAnimated = true;
            animateNumber(0, value, duration);
            observer.unobserve(entry.target);
          }
        });
      },
      { threshold: 0.5 }
    );

    observer.observe(element);

    return () => observer.disconnect();
  });
</script>

<div class="stat-block" bind:this={element}>
  <div class="stat-number">{displayValue}{suffix}</div>
  <p class="stat-label">{label}</p>
</div>

<style>
  .stat-block {
    background: rgba(255, 255, 255, 0.1);
    backdrop-filter: blur(10px);
    border-radius: 12px;
    padding: 2rem;
    border: 1px solid rgba(255, 255, 255, 0.2);
  }

  .stat-number {
    font-size: 3rem;
    font-weight: 700;
    margin-bottom: 0.5rem;
    color: var(--color-gold, #F6BD32);
  }

  .stat-label {
    font-size: 1rem;
    color: white;
    margin: 0;
  }
</style>
