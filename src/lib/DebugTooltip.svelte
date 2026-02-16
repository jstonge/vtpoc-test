<script>
  let { enabled = true } = $props();

  let showDebug = $state(false);

  // Detect WordPress admin bar
  let wpAdminBar = $derived(
    typeof document !== 'undefined' && document.getElementById('wpadminbar')
  );
</script>

{#if enabled}
  <button
    class="vtpoc-debug-toggle"
    onclick={() => (showDebug = !showDebug)}
    aria-label="Toggle z-index debug info"
  >
    z
  </button>

  {#if showDebug}
    <div class="vtpoc-debug-panel">
      <strong>z-index debug</strong>
      <ul>
        <li>sticky-panel: <code>0</code> (mobile)</li>
        <li>scrolly-content: <code>1</code> (mobile)</li>
        <li>scrolly-inner: <code>2</code></li>
        <li>step-box: <code>auto</code></li>
      </ul>
      <hr />
      <strong>WordPress</strong>
      <ul>
        <li>
          Admin bar: {wpAdminBar ? '✓ detected (z: 99999)' : '✗ not found'}
        </li>
      </ul>
      <p class="vtpoc-debug-hint">
        If elements are hidden behind WP UI, increase z-index values above
        99999.
      </p>
    </div>
  {/if}
{/if}

<style>
  .vtpoc-debug-toggle {
    position: fixed;
    bottom: 1rem;
    right: 1rem;
    width: 2rem;
    height: 2rem;
    border-radius: 50%;
    background: #333;
    color: #fff;
    border: none;
    font-family: monospace;
    font-weight: bold;
    cursor: pointer;
    z-index: 999999;
    opacity: 0.7;
    transition: opacity 0.2s;
  }

  .vtpoc-debug-toggle:hover {
    opacity: 1;
  }

  .vtpoc-debug-panel {
    position: fixed;
    bottom: 4rem;
    right: 1rem;
    background: #1a1a1a;
    color: #eee;
    padding: 1rem;
    border-radius: 8px;
    font-family: monospace;
    font-size: 12px;
    z-index: 999999;
    max-width: 280px;
    box-shadow: 0 4px 12px rgba(0, 0, 0, 0.3);
  }

  .vtpoc-debug-panel ul {
    margin: 0.5rem 0;
    padding-left: 1rem;
    list-style: none;
  }

  .vtpoc-debug-panel li {
    margin: 0.25rem 0;
  }

  .vtpoc-debug-panel code {
    background: #333;
    padding: 0.1rem 0.3rem;
    border-radius: 3px;
    color: #4fc3f7;
  }

  .vtpoc-debug-panel hr {
    border: none;
    border-top: 1px solid #444;
    margin: 0.75rem 0;
  }

  .vtpoc-debug-hint {
    margin-top: 0.5rem;
    color: #aaa;
    font-size: 11px;
  }
</style>
