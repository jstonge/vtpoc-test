<script lang="ts">
  interface Props {
    title?: string;
    description?: string;
    onsubmit?: (email: string) => void;
  }

  let {
    title = 'Stay Connected',
    description = 'Get updates on new data releases, community events, and policy developments directly to your inbox.',
    onsubmit
  }: Props = $props();

  let email = $state('');

  function handleSubmit(e: Event) {
    e.preventDefault();
    if (onsubmit) {
      onsubmit(email);
    } else {
      alert('Thank you for subscribing!');
    }
    email = '';
  }
</script>

<div class="newsletter-section">
  <h3>{title}</h3>
  <p>{description}</p>

  <form class="newsletter-form" onsubmit={handleSubmit}>
    <div class="form-group">
      <input
        type="email"
        name="email"
        placeholder="Enter your email address"
        required
        class="newsletter-input"
        bind:value={email}
      >
      <button type="submit" class="newsletter-button">Subscribe</button>
    </div>
    <p class="form-note">We respect your privacy. Unsubscribe anytime. See our <a href="https://www.vtpoc.net/privacy-policy/">privacy policy</a>.</p>
  </form>
</div>

<style>
  .newsletter-section {
    padding: 3rem;
    background: linear-gradient(135deg, var(--color-navy, #25466A) 0%, #2a5a7a 100%);
    border-radius: 12px;
    text-align: center;
    color: white;
  }

  .newsletter-section h3 {
    color: white;
    margin-bottom: 1rem;
  }

  .newsletter-section p {
    color: rgba(255, 255, 255, 0.9);
    max-width: 600px;
    margin: 0 auto 2rem;
  }

  .newsletter-form {
    max-width: 500px;
    margin: 0 auto;
  }

  .form-group {
    display: flex;
    gap: 0.75rem;
    margin-bottom: 1rem;
  }

  .newsletter-input {
    flex: 1;
    padding: 0.875rem 1.25rem;
    font-size: 1rem;
    border: 2px solid rgba(255, 255, 255, 0.2);
    border-radius: 8px;
    background: rgba(255, 255, 255, 0.1);
    color: white;
    transition: all 0.2s ease;
  }

  .newsletter-input::placeholder {
    color: rgba(255, 255, 255, 0.6);
  }

  .newsletter-input:focus {
    outline: none;
    border-color: var(--color-gold, #F6BD32);
    background: rgba(255, 255, 255, 0.15);
  }

  .newsletter-button {
    padding: 0.875rem 2rem;
    font-size: 1rem;
    font-weight: 700;
    background: var(--color-gold, #F6BD32);
    color: var(--color-navy, #25466A);
    border: none;
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.2s ease;
  }

  .newsletter-button:hover {
    background: #f4b035;
    transform: scale(1.05);
  }

  .form-note {
    font-size: 0.875rem;
    color: rgba(255, 255, 255, 0.7);
    margin-top: 1rem;
  }

  .form-note a {
    color: var(--color-gold, #F6BD32);
    text-decoration: underline;
  }

  @media (max-width: 768px) {
    .form-group {
      flex-direction: column;
    }
  }
</style>
