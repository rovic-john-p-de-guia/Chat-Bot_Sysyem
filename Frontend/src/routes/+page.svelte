<script lang="ts">
  import { onMount } from 'svelte';

  // Features section data
  const features = [
    {
      icon: '🎓',
      title: 'Quality Education',
      description: 'Providing excellent academic programs since 1962'
    },
    {
      icon: '🤖',
      title: 'AI Chat Assistant',
      description: 'Get instant answers to your questions about Gordon College'
    },
    {
      icon: '📚',
      title: 'Modern Facilities',
      description: 'State-of-the-art laboratories and learning spaces'
    },
    {
      icon: '🌟',
      title: 'Student Success',
      description: 'Dedicated support for your academic journey'
    }
  ];

  // Programs offered
  const programs = [
    {
      title: 'Information Technology',
      description: 'Learn cutting-edge technology and software development',
      icon: '💻'
    },
    {
      title: 'Business Administration',
      description: 'Develop business acumen and leadership skills',
      icon: '📊'
    },
    {
      title: 'Education',
      description: 'Shape the future through teaching excellence',
      icon: '📖'
    },
    {
      title: 'Criminology',
      description: 'Study criminal justice and law enforcement',
      icon: '⚖️'
    }
  ];

  let isHeaderVisible = true;
  let lastScrollY = 0;

  onMount(() => {
    const handleScroll = () => {
      const currentScrollY = window.scrollY;
      isHeaderVisible = currentScrollY < lastScrollY || currentScrollY < 50;
      lastScrollY = currentScrollY;
    };

    window.addEventListener('scroll', handleScroll, { passive: true });

    return () => {
      window.removeEventListener('scroll', handleScroll);
    };
  });
</script>

<main>
  <!-- Hero Section -->
  <section class="hero">
    <div class="hero-content">
      <h1>Welcome to Gordon College</h1>
      <p class="hero-subtitle">Empowering Minds, Transforming Lives</p>
      <p class="hero-description">
        Experience quality education with our modern facilities and dedicated faculty.
        Join our community of learners and shape your future with us.
      </p>
      <div class="hero-buttons">
        <a href="/auth/register" class="cta-button">Start Your Journey</a>
        <a href="/assistant" class="secondary-button">Ask GC Assistant</a>
      </div>
    </div>
    <div class="hero-image">
      <img src="/campus-hero.jpg" alt="Gordon College Campus" />
    </div>
  </section>

  <!-- Features Section -->
  <section id="features" class="features">
    <div class="section-container">
      <h2>Why Choose Gordon College?</h2>
      <div class="features-grid">
        {#each features as feature}
          <div class="feature-card">
            <div class="feature-icon">{feature.icon}</div>
            <h3>{feature.title}</h3>
            <p>{feature.description}</p>
          </div>
        {/each}
      </div>
    </div>
  </section>

  <!-- Programs Section -->
  <section id="programs" class="programs">
    <div class="section-container">
      <h2>Our Programs</h2>
      <div class="programs-grid">
        {#each programs as program}
          <div class="program-card">
            <div class="program-icon">{program.icon}</div>
            <h3>{program.title}</h3>
            <p>{program.description}</p>
            <a href="/auth/register" class="program-cta">Learn More →</a>
          </div>
        {/each}
      </div>
    </div>
  </section>

  <!-- About Section -->
  <section id="about" class="about">
    <div class="section-container">
      <div class="about-content">
        <div class="about-text">
          <h2>About Gordon College</h2>
          <p>
            Founded in 1962, Gordon College has been a beacon of academic excellence
            in Zambales. Our institution is committed to providing quality education
            that prepares students for the challenges of tomorrow.
          </p>
          <ul class="about-highlights">
            <li>✓ CHED Recognized Programs</li>
            <li>✓ Modern Learning Facilities</li>
            <li>✓ Expert Faculty Members</li>
            <li>✓ Strong Industry Partnerships</li>
          </ul>
          <a href="/auth/register" class="about-cta">Join Our Community</a>
        </div>
        <div class="about-image">
          <img src="/about-image.jpg" alt="Gordon College Campus Life" />
        </div>
      </div>
    </div>
  </section>

  <!-- Contact Section -->
  <section id="contact" class="contact">
    <div class="section-container">
      <h2>Get in Touch</h2>
      <div class="contact-content">
        <div class="contact-info">
          <div class="contact-item">
            <span class="contact-icon">📍</span>
            <div>
              <h3>Visit Us</h3>
              <p>Rizal St., East Tapinac<br>Olongapo City, Zambales</p>
            </div>
          </div>
          <div class="contact-item">
            <span class="contact-icon">📞</span>
            <div>
              <h3>Call Us</h3>
              <p>(047) 222-XXXX</p>
            </div>
          </div>
          <div class="contact-item">
            <span class="contact-icon">✉️</span>
            <div>
              <h3>Email Us</h3>
              <p>info@gordoncollege.edu.ph</p>
            </div>
          </div>
        </div>
        <div class="contact-map">
          <!-- Add your map embed code here -->
          <div class="map-placeholder">
            <p>Campus Map</p>
          </div>
        </div>
      </div>
    </div>
  </section>
</main>

<style>
  /* Hero Section */
  .hero {
    padding: 4rem var(--spacing-xl);
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 4rem;
    max-width: 1200px;
    margin: 0 auto;
  }

  .hero-content {
    display: flex;
    flex-direction: column;
    justify-content: center;
  }

  .hero h1 {
    font-size: 3.5rem;
    font-weight: 700;
    color: var(--text);
    margin-bottom: 1rem;
    line-height: 1.2;
  }

  .hero-subtitle {
    font-size: 1.5rem;
    color: var(--primary);
    margin-bottom: 1.5rem;
    font-weight: 500;
  }

  .hero-description {
    font-size: 1.125rem;
    color: var(--text-light);
    margin-bottom: 2rem;
    line-height: 1.6;
  }

  .hero-buttons {
    display: flex;
    gap: 1rem;
  }

  .cta-button {
    background: var(--primary);
    color: white;
    padding: 1rem 2rem;
    border-radius: var(--radius-md);
    text-decoration: none;
    font-weight: 500;
    transition: background-color 0.2s;
  }

  .cta-button:hover {
    background: var(--primary-light);
  }

  .secondary-button {
    background: transparent;
    color: var(--text);
    padding: 1rem 2rem;
    border-radius: var(--radius-md);
    text-decoration: none;
    font-weight: 500;
    border: 1px solid var(--border);
    transition: all 0.2s;
  }

  .secondary-button:hover {
    background: var(--surface);
    border-color: var(--text);
  }

  .hero-image {
    position: relative;
  }

  .hero-image img {
    width: 100%;
    height: 100%;
    object-fit: cover;
    border-radius: var(--radius-lg);
  }

  /* Features Section */
  .features {
    padding: 4rem 0;
    background: var(--surface);
  }

  .section-container {
    max-width: 1200px;
    margin: 0 auto;
    padding: 0 var(--spacing-xl);
  }

  .features h2 {
    text-align: center;
    font-size: 2.5rem;
    color: var(--text);
    margin-bottom: 3rem;
  }

  .features-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(250px, 1fr));
    gap: 2rem;
  }

  .feature-card {
    background: white;
    padding: 2rem;
    border-radius: var(--radius-lg);
    box-shadow: var(--shadow-sm);
    transition: transform 0.2s;
  }

  .feature-card:hover {
    transform: translateY(-4px);
  }

  .feature-icon {
    font-size: 2.5rem;
    margin-bottom: 1rem;
  }

  .feature-card h3 {
    color: var(--text);
    font-size: 1.25rem;
    margin-bottom: 0.5rem;
  }

  .feature-card p {
    color: var(--text-light);
  }

  /* Programs Section */
  .programs {
    padding: 4rem 0;
  }

  .programs h2 {
    text-align: center;
    font-size: 2.5rem;
    color: var(--text);
    margin-bottom: 3rem;
  }

  .programs-grid {
    display: grid;
    grid-template-columns: repeat(auto-fit, minmax(280px, 1fr));
    gap: 2rem;
  }

  .program-card {
    background: white;
    padding: 2rem;
    border-radius: var(--radius-lg);
    border: 1px solid var(--border);
    transition: all 0.2s;
  }

  .program-card:hover {
    border-color: var(--primary);
    box-shadow: var(--shadow-md);
  }

  .program-icon {
    font-size: 2.5rem;
    margin-bottom: 1rem;
  }

  .program-card h3 {
    color: var(--text);
    font-size: 1.25rem;
    margin-bottom: 0.5rem;
  }

  .program-card p {
    color: var(--text-light);
    margin-bottom: 1rem;
  }

  .program-cta {
    color: var(--primary);
    text-decoration: none;
    font-weight: 500;
    display: inline-flex;
    align-items: center;
    gap: 0.25rem;
  }

  .program-cta:hover {
    text-decoration: underline;
  }

  /* About Section */
  .about {
    padding: 4rem 0;
    background: var(--surface);
  }

  .about-content {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 4rem;
    align-items: center;
  }

  .about-text h2 {
    font-size: 2.5rem;
    color: var(--text);
    margin-bottom: 1.5rem;
  }

  .about-text p {
    color: var(--text-light);
    margin-bottom: 2rem;
    line-height: 1.6;
  }

  .about-highlights {
    list-style: none;
    margin-bottom: 2rem;
  }

  .about-highlights li {
    margin-bottom: 0.5rem;
    color: var(--text);
    display: flex;
    align-items: center;
    gap: 0.5rem;
  }

  .about-cta {
    display: inline-block;
    background: var(--primary);
    color: white;
    padding: 1rem 2rem;
    border-radius: var(--radius-md);
    text-decoration: none;
    font-weight: 500;
    transition: background-color 0.2s;
  }

  .about-cta:hover {
    background: var(--primary-light);
  }

  .about-image img {
    width: 100%;
    height: auto;
    border-radius: var(--radius-lg);
  }

  /* Contact Section */
  .contact {
    padding: 4rem 0;
  }

  .contact h2 {
    text-align: center;
    font-size: 2.5rem;
    color: var(--text);
    margin-bottom: 3rem;
  }

  .contact-content {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 4rem;
  }

  .contact-info {
    display: flex;
    flex-direction: column;
    gap: 2rem;
  }

  .contact-item {
    display: flex;
    gap: 1rem;
    align-items: flex-start;
  }

  .contact-icon {
    font-size: 1.5rem;
  }

  .contact-item h3 {
    color: var(--text);
    font-size: 1.25rem;
    margin-bottom: 0.25rem;
  }

  .contact-item p {
    color: var(--text-light);
  }

  .contact-map {
    border-radius: var(--radius-lg);
    overflow: hidden;
  }

  .map-placeholder {
    background: var(--surface);
    height: 100%;
    min-height: 300px;
    display: flex;
    align-items: center;
    justify-content: center;
    color: var(--text-light);
    border: 1px solid var(--border);
  }

  /* Responsive Design */
  @media (max-width: 768px) {
    .hero {
      grid-template-columns: 1fr;
      padding-top: 6rem;
      gap: 2rem;
    }

    .about-content {
      grid-template-columns: 1fr;
    }

    .contact-content {
      grid-template-columns: 1fr;
    }
  }
</style>
