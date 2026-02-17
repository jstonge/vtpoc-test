<script lang="ts">
  interface BarData {
    label: string;
    value: number;
    displayValue: string;
    color?: string;
  }

  interface Props {
    title: string;
    bars: BarData[];
    maxValue?: number;
    gapLabel?: string;
    gapPosition?: { from: number; to: number };
    subtitle?: string;
    impactText?: string;
  }

  let {
    title,
    bars,
    maxValue = 100,
    gapLabel,
    gapPosition,
    subtitle,
    impactText
  }: Props = $props();

  const barWidth = 300;
  const scale = (value: number) => (value / maxValue) * barWidth;
</script>

<div class="gap-chart">
  <svg viewBox="0 0 600 {impactText ? 220 : 180}" class="gap-viz">
    <text x="300" y="25" text-anchor="middle" font-size="14" fill="#666" font-weight="600">{title}</text>

    {#each bars as bar, i (i)}
      {@const y = 55 + i * 50}
      <!-- Background bar -->
      <rect x="50" y={y} width={barWidth} height="30" fill={bar.color || "#1a3a52"} opacity="0.2"/>
      <!-- Value bar -->
      <rect x="50" y={y} width={scale(bar.value)} height="30" fill={bar.color || "#1a3a52"}/>
      <!-- Label -->
      <text x={60 + scale(bar.value)} y={y + 20} font-size="13" fill="#1a3a52" font-weight="bold">{bar.label}: {bar.displayValue}</text>
    {/each}

    {#if gapLabel && gapPosition}
      {@const fromY = 55 + gapPosition.from * 50 + 15}
      {@const toY = 55 + gapPosition.to * 50 + 15}
      <path d="M {50 + scale(bars[gapPosition.from].value)} {fromY + 15} L {50 + scale(bars[gapPosition.to].value)} {toY - 15}" stroke="#c64226" stroke-width="2"/>
      <text x="{(50 + scale(bars[gapPosition.from].value) + 50 + scale(bars[gapPosition.to].value)) / 2 + 20}" y="{(fromY + toY) / 2 + 5}" font-size="12" fill="#c64226" font-weight="bold">{gapLabel}</text>
    {/if}

    {#if impactText}
      <text x="300" y="170" font-size="12" fill="#666" font-weight="600" text-anchor="middle">Economic Impact:</text>
      <text x="300" y="190" font-size="11" fill="#666" text-anchor="middle">{impactText}</text>
    {/if}

    {#if subtitle}
      <text x="300" y="{impactText ? 210 : 170}" text-anchor="middle" font-size="11" fill="#999">{subtitle}</text>
    {/if}
  </svg>
</div>

<style>
  .gap-chart {
    margin: 20px 0;
  }

  .gap-viz {
    width: 100%;
    height: auto;
    max-width: 600px;
    display: block;
    margin: 0 auto;
  }
</style>
