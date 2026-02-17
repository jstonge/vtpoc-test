<script lang="ts">
  import logoImg from '../assets/vtpoc-logo.png';
</script>

<header class="site-header">
  <div class="header-container">
    <div class="logo-section">
      <img src={logoImg} alt="VT PoC Logo" class="logo-img">
      <h2 class="site-title">Vermont Professionals of Color Network</h2>
    </div>
    <nav class="header-nav">
      <a href="#" class="nav-link">Our Work</a>
      <a href="#" class="nav-link">Events</a>
      <a href="#" class="nav-link">Resources</a>
      <a href="#" class="nav-link">Member Directory</a>
      <a href="#" class="nav-link cta-link">Donate</a>
    </nav>
  </div>
  <div class="header-accent"></div>
</header>

<style>
  .site-header {
    background: white;
    color: var(--color-navy, #25466A);
    padding: 0;
    position: sticky;
    top: 0;
    z-index: 500;
    box-shadow: 0 2px 12px rgba(0, 0, 0, 0.15);
  }

  .header-container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 1.5rem 40px;
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  .logo-section {
    display: flex;
    align-items: center;
    gap: 1.5rem;
  }

  .logo-img {
    height: 60px;
    width: auto;
    display: block;
  }

  .site-title {
    font-size: 1rem;
    font-weight: 400;
    color: var(--color-navy, #25466A);
    margin: 0;
  }

  .header-nav {
    display: flex;
    gap: 2rem;
    align-items: center;
  }

  .nav-link {
    color: var(--color-navy, #25466A);
    text-decoration: none;
    font-size: 0.95rem;
    font-weight: 500;
    transition: color 0.3s ease;
  }

  .nav-link:hover {
    color: var(--color-gold, #F6BD32);
  }

  .nav-link.cta-link {
    background: var(--color-gold, #F6BD32);
    color: var(--color-navy, #25466A);
    padding: 0.6rem 1.2rem;
    border-radius: 4px;
    font-weight: 600;
  }

  .nav-link.cta-link:hover {
    background: #ffd93d;
  }

  .header-accent {
    height: 4px;
    background: linear-gradient(90deg, var(--color-gold, #F6BD32) 0%, #ffd93d 50%, var(--color-gold, #F6BD32) 100%);
  }

  @media (max-width: 768px) {
    .header-container {
      flex-direction: column;
      gap: 1rem;
      padding: 1rem 20px;
    }

    .header-nav {
      gap: 1rem;
      flex-wrap: wrap;
      justify-content: center;
    }
  }
</style>
