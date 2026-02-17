<script lang="ts">
  // Footer component - no props needed for now
</script>

<footer class="story-footer">
  <div class="footer-content">
    <h3>About This Story</h3>
    <p>This data story is a prototype created for the Vermont Professionals of Color Network (VT PoC) by UVM VERSO. It demonstrates how interactive data storytelling can communicate complex equity issues to diverse audiences.</p>

    <div class="footer-grid">
      <div class="footer-column">
        <h4>Data Sources</h4>
        <ul>
          <li>VT PoC Community Survey (2024)</li>
          <li>U.S. Census & ACS (2023)</li>
          <li>Vermont Department of Labor</li>
          <li>Vermont Housing Finance Agency</li>
          <li>Additional state and community datasets</li>
        </ul>
      </div>
      <div class="footer-column">
        <h4>Methods</h4>
        <ul>
          <li>Confidence intervals displayed where available</li>
          <li>Small counts (n&lt;10) suppressed for privacy</li>
          <li>Data aggregated to county level when needed</li>
          <li>Qualitative themes coded by community voice principles</li>
        </ul>
      </div>
      <div class="footer-column">
        <h4>Learn More</h4>
        <ul>
          <li><a href="#">Full Data Portal</a></li>
          <li><a href="#">Technical Documentation</a></li>
          <li><a href="#">Methodology & Ethics</a></li>
          <li><a href="#">Contact & Feedback</a></li>
        </ul>
      </div>
    </div>

    <div class="footer-bottom">
      <p>&copy; 2026 Vermont Professionals of Color Network. Data and stories are shared under a Creative Commons license.</p>
    </div>
  </div>
</footer>

<style>
  .story-footer {
    background: #1a1a1a;
    color: white;
    padding: 4rem 20px;
  }

  .footer-content {
    max-width: 1200px;
    margin: 0 auto;
  }

  .footer-content h3 {
    color: white;
    margin-bottom: 1rem;
    font-size: 1.8rem;
  }

  .footer-content > p {
    margin-bottom: 2rem;
    color: #ccc;
    max-width: 700px;
    font-size: 1rem;
  }

  .footer-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 2rem;
    margin: 2rem 0;
    padding: 2rem 0;
    border-top: 1px solid rgba(255, 255, 255, 0.1);
    border-bottom: 1px solid rgba(255, 255, 255, 0.1);
  }

  .footer-column h4 {
    color: white;
    margin-bottom: 1rem;
    font-size: 1rem;
  }

  .footer-column ul {
    list-style: none;
    padding: 0;
    margin: 0;
  }

  .footer-column li {
    margin: 0.5rem 0;
    color: #ccc;
  }

  .footer-column a {
    color: var(--color-gold, #F6BD32);
    font-size: 0.95rem;
  }

  .footer-column a:hover {
    color: white;
    text-decoration: underline;
  }

  .footer-bottom {
    text-align: center;
    padding-top: 2rem;
    color: #999;
    font-size: 0.9rem;
  }
</style>
