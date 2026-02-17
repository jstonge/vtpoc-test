<script lang="ts">
  interface Metric {
    label: string;
    value: string;
    color?: 'alert' | 'primary' | 'gold';
  }

  interface Props {
    title: string;
    metrics: Metric[];
    layout?: 'horizontal' | 'grid';
  }

  let { title, metrics, layout = 'horizontal' }: Props = $props();

  const colorMap = {
    alert: { bg: '#FFE5E5', border: '#c64226', text: '#c64226' },
    primary: { bg: '#E8F4F8', border: '#1a3a52', text: '#1a3a52' },
    gold: { bg: '#FFF8E5', border: '#F4D35E', text: '#1a3a52' }
  };
</script>

<div class="impact-metrics">
  <svg viewBox="0 0 600 {layout === 'grid' ? 160 : 120}" class="impact-viz">
    <text x="300" y="20" text-anchor="middle" font-size="12" fill="#666" font-weight="bold">{title}</text>

    {#if layout === 'horizontal'}
      {@const boxWidth = 140}
      {@const gap = 20}
      {@const totalWidth = metrics.length * boxWidth + (metrics.length - 1) * gap}
      {@const startX = (600 - totalWidth) / 2}

      {#each metrics as metric, i (i)}
        {@const colors = colorMap[metric.color || 'alert']}
        {@const x = startX + i * (boxWidth + gap)}
        <rect x={x} y="40" width={boxWidth} height="65" fill={colors.bg} rx="4" stroke={colors.border} stroke-width="1"/>
        <text x={x + boxWidth / 2} y="58" text-anchor="middle" font-size="10" font-weight="bold" fill={colors.text}>{metric.label}</text>
        <text x={x + boxWidth / 2} y="85" text-anchor="middle" font-size="16" font-weight="bold" fill="#1a3a52">{metric.value}</text>
      {/each}
    {:else}
      {@const cols = 2}
      {@const boxWidth = 200}
      {@const boxHeight = 50}
      {@const gapX = 40}
      {@const gapY = 15}
      {@const startX = (600 - (cols * boxWidth + (cols - 1) * gapX)) / 2}

      {#each metrics as metric, i (i)}
        {@const colors = colorMap[metric.color || 'primary']}
        {@const col = i % cols}
        {@const row = Math.floor(i / cols)}
        {@const x = startX + col * (boxWidth + gapX)}
        {@const y = 40 + row * (boxHeight + gapY)}
        <g>
          <text x={x} y={y + 15} font-size="11" fill="#666">{metric.label}</text>
          <text x={x} y={y + 38} font-size="16" fill="#1a3a52" font-weight="bold">{metric.value}</text>
        </g>
      {/each}
    {/if}
  </svg>
</div>

<style>
  .impact-metrics {
    margin: 20px 0;
  }

  .impact-viz {
    width: 100%;
    height: auto;
    max-width: 600px;
    display: block;
    margin: 0 auto;
  }
</style>
