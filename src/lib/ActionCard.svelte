<script lang="ts">
  interface Props {
    label: string;
    title: string;
    description: string;
    buttonText: string;
    href: string;
    impact?: string;
    highlight?: boolean;
    external?: boolean;
  }

  let {
    label,
    title,
    description,
    buttonText,
    href,
    impact,
    highlight = false,
    external = false
  }: Props = $props();
</script>

<div class="action-card" class:highlight>
  <span class="action-label">{label}</span>
  <h4>{title}</h4>
  <p>{description}</p>
  <a
    {href}
    class="action-button"
    class:primary={highlight}
    class:secondary={!highlight}
    target={external ? '_blank' : undefined}
    rel={external ? 'noopener noreferrer' : undefined}
  >
    {buttonText}
  </a>
  {#if impact}
    <span class="action-impact">{impact}</span>
  {/if}
</div>

<style>
  .action-card {
    position: relative;
    background: white;
    border: 2px solid #e5e7eb;
    border-radius: 12px;
    padding: 2rem;
    transition: all 0.3s ease;
    display: flex;
    flex-direction: column;
    gap: 1rem;
  }

  .action-card:hover {
    border-color: var(--color-gold, #F6BD32);
    box-shadow: 0 8px 24px rgba(26, 58, 82, 0.12);
    transform: translateY(-4px);
  }

  .action-card.highlight {
    border-color: var(--color-gold, #F6BD32);
    background: linear-gradient(135deg, #fffef9 0%, white 100%);
  }

  .action-label {
    display: inline-block;
    font-size: 0.75rem;
    font-weight: 700;
    text-transform: uppercase;
    letter-spacing: 0.05em;
    color: var(--color-navy, #25466A);
    background: var(--color-gold, #F6BD32);
    padding: 0.35rem 0.85rem;
    border-radius: 20px;
    align-self: flex-start;
  }

  .action-card h4 {
    font-size: 1.4rem;
    font-weight: 700;
    color: var(--color-navy, #25466A);
    margin: 0;
  }

  .action-card p {
    color: #4b5563;
    line-height: 1.6;
    margin: 0;
    flex-grow: 1;
  }

  .action-button {
    display: inline-flex;
    align-items: center;
    justify-content: center;
    padding: 0.875rem 1.75rem;
    font-weight: 700;
    font-size: 1rem;
    text-decoration: none;
    border-radius: 8px;
    transition: all 0.2s ease;
    border: 2px solid transparent;
    text-align: center;
    margin-top: 0.5rem;
  }

  .action-button.primary {
    background: var(--color-navy, #25466A);
    color: white;
    border-color: var(--color-navy, #25466A);
  }

  .action-button.primary:hover {
    background: #2a5a7a;
    border-color: #2a5a7a;
  }

  .action-button.secondary {
    background: white;
    color: var(--color-navy, #25466A);
    border-color: var(--color-navy, #25466A);
  }

  .action-button.secondary:hover {
    background: var(--color-navy, #25466A);
    color: white;
  }

  .action-impact {
    display: block;
    font-size: 0.875rem;
    color: #6b7280;
    font-style: italic;
    margin-top: 0.75rem;
    padding-top: 0.75rem;
    border-top: 1px solid #e5e7eb;
  }
</style>
