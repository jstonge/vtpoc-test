<script lang="ts">
  interface Props {
    title?: string;
    message?: string;
    submessage?: string;
  }

  let {
    title = "Data Visibility by County",
    message = "Data Suppressed: n<10",
    submessage = "Rural counties cannot see their own patterns"
  }: Props = $props();
</script>

<div class="suppression-chart">
  <svg viewBox="0 0 700 200" class="sample-chart">
    <text x="350" y="25" text-anchor="middle" font-size="16" font-weight="bold" fill="#1a3a52">{title}</text>
    <rect x="100" y="50" width="500" height="120" fill="#1a3a52" opacity="0.1" rx="8"/>
    <text x="350" y="110" text-anchor="middle" font-size="16" fill="#c64226" font-weight="bold">{message}</text>
    <text x="350" y="135" text-anchor="middle" font-size="12" fill="#666">{submessage}</text>
  </svg>
</div>

<style>
  .suppression-chart {
    margin: 20px 0;
  }

  .sample-chart {
    width: 100%;
    height: auto;
    max-width: 700px;
    display: block;
    margin: 0 auto;
  }
</style>
