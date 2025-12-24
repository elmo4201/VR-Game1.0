<!DOCTYPE html>
<html lang="en">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>Vibe – Short Video & Live App</title>
  <style>
    :root {
      --bg-dark: #0b0b0b;
      --bg-card: #111111;
      --bg-header: #000000;
      --text-main: #ffffff;
      --text-muted: #cccccc;
      --accent-pink: #ff0050;
      --accent-red: #ff0000;
      --border-subtle: #222222;
    }

    body.light {
      --bg-dark: #f5f5f5;
      --bg-card: #ffffff;
      --bg-header: #ffffff;
      --text-main: #000000;
      --text-muted: #555555;
      --border-subtle: #dddddd;
    }

    * {
      box-sizing: border-box;
    }

    body {
      margin: 0;
      font-family: Arial, sans-serif;
      background: var(--bg-dark);
      color: var(--text-main);
      scroll-behavior: smooth;
    }

    /* Sticky Header */
    header {
      padding: 16px 24px;
      display: flex;
      justify-content: space-between;
      align-items: center;
      background: var(--bg-header);
      position: sticky;
      top: 0;
      z-index: 1000;
      border-bottom: 1px solid var(--border-subtle);
    }

    .logo {
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .logo-icon {
      width: 28px;
      height: 28px;
      border-radius: 8px;
      background: linear-gradient(135deg, var(--accent-pink), var(--accent-red));
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 16px;
      font-weight: bold;
      color: #ffffff;
    }

    header h1 {
      margin: 0;
      color: var(--accent-pink);
      font-weight: 900;
      letter-spacing: 1px;
      font-size: 22px;
    }

    nav {
      display: flex;
      align-items: center;
      gap: 16px;
    }

    nav a {
      color: var(--text-main);
      text-decoration: none;
      font-weight: bold;
      font-size: 14px;
      transition: 0.3s;
    }

    nav a:hover {
      color: var(--accent-pink);
      text-shadow: 0 0 10px var(--accent-pink);
    }

    .header-actions {
      display: flex;
      align-items: center;
      gap: 10px;
    }

    .toggle-theme {
      padding: 8px 14px;
      font-size: 12px;
      border-radius: 999px;
      border: 1px solid var(--border-subtle);
      background: transparent;
      color: var(--text-main);
      cursor: pointer;
      display: flex;
      align-items: center;
      gap: 6px;
    }

    .toggle-theme span {
      font-size: 14px;
    }

    .primary-cta {
      padding: 8px 16px;
      font-size: 13px;
      border: none;
      border-radius: 999px;
      background: linear-gradient(90deg, var(--accent-pink), var(--accent-red));
      color: #ffffff;
      cursor: pointer;
      font-weight: bold;
      box-shadow: 0 0 12px var(--accent-pink);
      transition: 0.3s;
    }

    .primary-cta:hover {
      transform: scale(1.03);
      box-shadow: 0 0 20px var(--accent-pink);
    }

    /* Mobile Nav */
    .menu-toggle {
      display: none;
      background: none;
      border: none;
      color: var(--text-main);
      font-size: 22px;
      cursor: pointer;
    }

    @media (max-width: 768px) {
      nav {
        position: fixed;
        inset: 60px 0 auto 0;
        background: var(--bg-header);
        flex-direction: column;
        padding: 16px 24px 24px;
        gap: 12px;
        transform: translateY(-150%);
        opacity: 0;
        pointer-events: none;
        transition: 0.3s ease;
      }

      nav.open {
        transform: translateY(0);
        opacity: 1;
        pointer-events: auto;
      }

      .header-actions {
        display: none;
      }

      .menu-toggle {
        display: block;
      }
    }

    /* Hero with video background */
    .hero {
      position: relative;
      height: 90vh;
      display: flex;
      align-items: center;
      justify-content: center;
      text-align: center;
      padding: 20px;
      overflow: hidden;
      color: #ffffff;
    }

    .hero-video {
      position: absolute;
      inset: 0;
      width: 100%;
      height: 100%;
      object-fit: cover;
      filter: brightness(0.3);
      z-index: -2;
    }

    .hero-overlay {
      position: absolute;
      inset: 0;
      background: radial-gradient(circle at top left, rgba(255, 0, 80, 0.5), transparent),
                  radial-gradient(circle at bottom right, rgba(255, 0, 0, 0.6), transparent);
      z-index: -1;
    }

    .hero-content {
      max-width: 600px;
      animation: fadeIn 1.2s ease;
    }

    .hero-tagline {
      display: inline-flex;
      align-items: center;
      gap: 8px;
      padding: 4px 10px;
      border-radius: 999px;
      background: rgba(0, 0, 0, 0.6);
      border: 1px solid rgba(255, 0, 80, 0.7);
      font-size: 12px;
      margin-bottom: 12px;
    }

    .hero-tag-pill {
      width: 7px;
      height: 7px;
      border-radius: 50%;
      background: #00ff88;
      box-shadow: 0 0 8px #00ff88;
    }

    .hero h2 {
      font-size: 52px;
      margin-bottom: 10px;
      font-weight: 900;
    }

    .hero p {
      font-size: 18px;
      color: #e0e0e0;
      margin-bottom: 24px;
    }

    .hero-actions {
      display: flex;
      justify-content: center;
      gap: 12px;
      flex-wrap: wrap;
    }

    .hero button.hero-secondary {
      padding: 12px 24px;
      font-size: 14px;
      border-radius: 999px;
      border: 1px solid rgba(255, 255, 255, 0.3);
      background: rgba(0, 0, 0, 0.5);
      color: #ffffff;
      cursor: pointer;
      display: flex;
      align-items: center;
      gap: 8px;
    }

    .hero-stats {
      margin-top: 30px;
      display: flex;
      justify-content: center;
      gap: 24px;
      flex-wrap: wrap;
      font-size: 13px;
      color: #dddddd;
    }

    .hero-stats span strong {
      color: var(--accent-pink);
    }

    /* Sections shared */
    section {
      padding: 60px 20px;
    }

    .section-heading {
      text-align: center;
      margin-bottom: 30px;
    }

    .section-heading h2 {
      font-size: 32px;
      font-weight: 900;
      margin-bottom: 6px;
      color: var(--accent-pink);
    }

    .section-heading p {
      color: var(--text-muted);
      font-size: 16px;
    }

    /* Features */
    .features {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(230px, 1fr));
      gap: 20px;
    }

    .card {
      background: var(--bg-card);
      padding: 22px;
      border-radius: 14px;
      transition: 0.3s;
      border: 1px solid var(--border-subtle);
    }

    .card:hover {
      transform: translateY(-5px);
      box-shadow: 0 0 20px rgba(255, 0, 80, 0.4);
      border-color: var(--accent-pink);
    }

    .card h3 {
      color: var(--accent-pink);
      font-size: 20px;
      margin-bottom: 8px;
    }

    .card p {
      color: var(--text-muted);
      font-size: 14px;
    }

    /* Download */
    .download {
      background: var(--bg-dark);
      border-top: 1px solid var(--border-subtle);
    }

    .download .store-buttons {
      display: flex;
      justify-content: center;
      gap: 20px;
      flex-wrap: wrap;
      margin-top: 14px;
    }

    .store-btn {
      padding: 12px 24px;
      font-size: 16px;
      border: none;
      border-radius: 10px;
      cursor: pointer;
      font-weight: bold;
      display: flex;
      align-items: center;
      gap: 10px;
      transition: 0.3s;
      box-shadow: 0 0 15px rgba(255, 0, 80, 0.6);
    }

    .store-btn span {
      font-size: 20px;
    }

    .store-btn.ios {
      background: #ffffff;
      color: #000000;
    }

    .store-btn.android {
      background: var(--accent-red);
      color: #ffffff;
    }

    .store-btn:hover {
      transform: scale(1.05);
      box-shadow: 0 0 25px rgba(255, 0, 80, 0.9);
    }

    /* Creators section */
    .creators-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(260px, 1fr));
      gap: 20px;
      align-items: stretch;
    }

    .creator-card-highlight {
      border: 1px solid var(--accent-pink);
      box-shadow: 0 0 20px rgba(255, 0, 80, 0.4);
    }

    .creator-metrics {
      display: flex;
      gap: 16px;
      margin-top: 14px;
      flex-wrap: wrap;
      font-size: 13px;
      color: var(--text-muted);
    }

    .creator-metrics span strong {
      color: var(--accent-pink);
    }

    .badge {
      display: inline-block;
      padding: 3px 8px;
      border-radius: 999px;
      font-size: 11px;
      color: #ffffff;
      background: linear-gradient(90deg, var(--accent-pink), var(--accent-red));
      margin-top: 6px;
    }

    /* Messaging section */
    .messaging-layout {
      display: grid;
      grid-template-columns: minmax(0, 1.3fr) minmax(0, 1fr);
      gap: 24px;
      align-items: center;
    }

    @media (max-width: 850px) {
      .messaging-layout {
        grid-template-columns: 1fr;
      }
    }

    .chat-mock {
      background: var(--bg-card);
      border-radius: 18px;
      padding: 16px;
      border: 1px solid var(--border-subtle);
      max-width: 420px;
      margin: 0 auto;
    }

    .chat-header {
      display: flex;
      align-items: center;
      justify-content: space-between;
      margin-bottom: 12px;
    }

    .chat-user {
      display: flex;
      align-items: center;
      gap: 8px;
      font-size: 13px;
    }

    .chat-avatar {
      width: 28px;
      height: 28px;
      border-radius: 50%;
      background: linear-gradient(135deg, var(--accent-pink), var(--accent-red));
    }

    .chat-dot {
      width: 4px;
      height: 4px;
      border-radius: 50%;
      background: #00ff88;
      box-shadow: 0 0 8px #00ff88;
    }

    .chat-bubbles {
      display: flex;
      flex-direction: column;
      gap: 8px;
      font-size: 13px;
    }

    .bubble {
      padding: 8px 12px;
      border-radius: 14px;
      max-width: 80%;
    }

    .bubble.me {
      margin-left: auto;
      background: linear-gradient(90deg, var(--accent-pink), var(--accent-red));
      color: #ffffff;
    }

    .bubble.them {
      background: rgba(255, 255, 255, 0.04);
      border: 1px solid var(--border-subtle);
    }

    /* Screenshots section */
    .screenshots-grid {
      display: grid;
      grid-template-columns: repeat(auto-fit, minmax(220px, 1fr));
      gap: 20px;
    }

    .screenshot-card {
      background: var(--bg-card);
      border-radius: 16px;
      padding: 16px;
      border: 1px solid var(--border-subtle);
      text-align: center;
      font-size: 13px;
      color: var(--text-muted);
    }

    .screenshot-frame {
      width: 100%;
      aspect-ratio: 9 / 16;
      border-radius: 12px;
      background: radial-gradient(circle at top, rgba(255, 0, 80, 0.5), transparent),
                  radial-gradient(circle at bottom, rgba(255, 0, 0, 0.7), transparent),
                  #000000;
      margin-bottom: 10px;
      position: relative;
      overflow: hidden;
    }

    .screenshot-frame::after {
      content: "Vibe UI preview";
      position: absolute;
      bottom: 8px;
      left: 50%;
      transform: translateX(-50%);
      font-size: 11px;
      color: #ffffff;
      opacity: 0.8;
    }

    /* Contact section */
    .contact {
      background: var(--bg-card);
      border-top: 1px solid var(--border-subtle);
    }

    .contact-inner {
      max-width: 600px;
      margin: 0 auto;
    }

    .contact-form {
      display: flex;
      flex-direction: column;
      gap: 12px;
      margin-top: 16px;
    }

    .contact-form label {
      font-size: 13px;
      color: var(--text-muted);
    }

    .contact-form input,
    .contact-form textarea {
      width: 100%;
      padding: 10px;
      border-radius: 8px;
      border: 1px solid var(--border-subtle);
      background: var(--bg-dark);
      color: var(--text-main);
      font-size: 14px;
    }

    .contact-form textarea {
      resize: vertical;
      min-height: 100px;
    }

    .contact-form button {
      align-self: flex-start;
      padding: 10px 20px;
      font-size: 14px;
      border-radius: 999px;
      border: none;
      background: linear-gradient(90deg, var(--accent-pink), var(--accent-red));
      color: #ffffff;
      cursor: pointer;
      font-weight: bold;
      margin-top: 4px;
    }

    .contact-note {
      font-size: 12px;
      color: var(--text-muted);
      margin-top: 10px;
    }

    /* Footer */
    footer {
      text-align: center;
      padding: 18px 16px;
      background: var(--bg-header);
      color: #777777;
      font-size: 12px;
      border-top: 1px solid var(--border-subtle);
    }

    /* Animations */
    @keyframes fadeIn {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }
  </style>
</head>
<body>
  <header>
    <div class="logo">
      <div class="logo-icon">V</div>
      <h1>Vibe</h1>
    </div>

    <button class="menu-toggle" aria-label="Toggle menu">☰</button>

    <nav>
      <a href="#features">Features</a>
      <a href="#creators">Creators</a>
      <a href="#download">Download</a>
      <a href="#screenshots">Screenshots</a>
      <a href="#contact">Contact</a>
    </nav>

    <div class="header-actions">
      <button class="toggle-theme" id="themeToggle">
        <span>🌙</span> Theme
      </button>
      <button class="primary-cta" onclick="scrollToDownload()">Get the App</button>
    </div>
  </header>

  <!-- Hero with video background -->
  <section class="hero">
    <!-- You can replace this video src with your own MP4 link -->
    <video class="hero-video" autoplay muted loop playsinline>
      <source src="http:/www.youtube.com/killerelmo43" type="video/mp4" />
    </video>
    <div class="hero-overlay"></div>

    <div class="hero-content">
      <div class="hero-tagline">
        <span class="hero-tag-pill"></span>
        Live now: 4,329 creators streaming
      </div>
      <h2>Watch. Create. Go Live.</h2>
      <p>The next‑gen short video & live streaming platform built for creators who want to grow fast.</p>

      <div class="hero-actions">
        <button class="primary-cta" onclick="scrollToDownload()">Download Vibe</button>
        <button class="hero-secondary" onclick="alert('Creator studio coming soon!')">
          🎥 Open Creator Studio
        </button>
      </div>

      <div class="hero-stats">
        <span><strong>+1.2M</strong> daily swipes</span>
        <span><strong>+8K</strong> active creators</span>
        <span><strong>Zero</strong> boring feeds</span>
      </div>
    </div>
  </section>

  <!-- Features -->
  <section id="features">
    <div class="section-heading">
      <h2>Features</h2>
      <p>Everything you need to create, go live, and build a real audience.</p>
    </div>

    <div class="features">
      <div class="card">
        <h3>Short Videos</h3>
        <p>Swipe through an endless feed of vertical videos tuned to your interests in seconds.</p>
      </div>
      <div class="card">
        <h3>Live Streaming</h3>
        <p>Go live in one tap, hang out with your community, and keep the chat flowing in real time.</p>
      </div>
      <div class="card">
        <h3>Messaging</h3>
        <p>DM your favorite creators, start group chats, and keep the conversation going off‑stream.</p>
      </div>
      <div class="card">
        <h3>Creator Tools</h3>
        <p>Advanced analytics, scheduling, and editing tools that help you grow without burning out.</p>
      </div>
    </div>
  </section>

  <!-- Creator monetization / focus -->
  <section id="creators">
    <div class="section-heading">
      <h2>Built for creators</h2>
      <p>Vibe puts creators first with growth, engagement, and monetization at the core.</p>
    </div>

    <div class="creators-grid">
      <div class="card creator-card-highlight">
        <h3>Earn while you stream</h3>
        <p>Turn your audience into a real income stream with gifts, memberships, and brand drops.</p>
        <div class="creator-metrics">
          <span><strong>Up to 70%</strong> creator revenue share</span>
          <span><strong>Instant</strong> payout options</span>
        </div>
        <span class="badge">Creator‑friendly payouts</span>
      </div>

      <div class="card">
        <h3>Deep analytics</h3>
        <p>See what content hits, when your audience is active, and how your channel grows over time.</p>
        <div class="creator-metrics">
          <span><strong>Real‑time</strong> viewer insights</span>
          <span><strong>Content heatmaps</strong> by watch time</span>
        </div>
      </div>

      <div class="card">
        <h3>Grow on your terms</h3>
        <p>Smart recommendations surface your content to the right viewers instead of the same old crowd.</p>
        <div class="creator-metrics">
          <span><strong>Fair</strong> discovery engine</span>
          <span><strong>Zero</strong> pay‑to‑play boosts</span>
        </div>
      </div>
    </div>
  </section>

  <!-- Messaging / social -->
  <section>
    <div class="section-heading">
      <h2>Messaging that keeps up</h2>
      <p>DMs, replies, and live chat all in one place.</p>
    </div>

    <div class="messaging-layout">
      <div>
        <h3 style="margin-top:0;">Stay close to your people</h3>
        <p style="color:var(--text-muted); font-size:14px; margin-bottom:10px;">
          Vibe makes it easy to keep your community tight with fast, creator‑first messaging.
        </p>
        <ul style="padding-left:18px; color:var(--text-muted); font-size:14px;">
          <li><strong>Live chat:</strong> interact with fans in real time while you stream.</li>
          <li><strong>Creator inbox:</strong> separate brand deals, fan messages, and collab requests.</li>
          <li><strong>Reply with video:</strong> turn comments into content in a single tap.</li>
        </ul>
      </div>

      <div class="chat-mock">
        <div class="chat-header">
          <div class="chat-user">
            <div class="chat-avatar"></div>
            <div>
              <div style="font-weight:bold;">@nightshiftcreator</div>
              <div style="font-size:11px; color:var(--text-muted);">Live now • 3.2K watching</div>
            </div>
          </div>
          <div class="chat-dot"></div>
        </div>
        <div class="chat-bubbles">
          <div class="bubble them">Just hit 50K followers this week 👀</div>
          <div class="bubble me">Let’s pin your best clips and push a highlight reel.</div>
          <div class="bubble them">Bet. Vibe actually wants me to grow lol</div>
          <div class="bubble me">Always. You focus on creating, we handle the rest.</div>
        </div>
      </div>
    </div>
  </section>

  <!-- Download section -->
  <section id="download" class="download">
    <div class="section-heading">
      <h2>Get the Vibe app</h2>
      <p>Launching soon on iOS and Android. Be first in line.</p>
    </div>

    <div class="store-buttons">
      <button class="store-btn ios" onclick="alert('App Store listing coming soon!')">
        <span></span> App Store
      </button>
      <button class="store-btn android" onclick="alert('Google Play listing coming soon!')">
        <span>▶</span> Google Play
      </button>
    </div>
  </section>

  <!-- Screenshots / preview -->
  <section id="screenshots">
    <div class="section-heading">
      <h2>See the experience</h2>
      <p>A feed that never sleeps, a studio that actually helps you grow.</p>
    </div>

    <div class="screenshots-grid">
      <div class="screenshot-card">
        <div class="screenshot-frame"></div>
        Creator feed with shorts, live rooms, and pinned clips.
      </div>
      <div class="screenshot-card">
        <div class="screenshot-frame"></div>
        Live control room with chat, gifts, and analytics in one view.
      </div>
      <div class="screenshot-card">
        <div class="screenshot-frame"></div>
        Creator studio dashboard tracking views, watch time, and revenue.
      </div>
    </div>
  </section>

  <!-- Contact section -->
  <section id="contact" class="contact">
    <div class="section-heading">
      <h2>Contact</h2>
      <p>Brands, creators, partners — let’s talk.</p>
    </div>

    <div class="contact-inner">
      <form class="contact-form" onsubmit="handleContactSubmit(event)">
        <div>
          <label for="name">Name</label>
          <input id="name" type="text" required placeholder="Your name" />
        </div>
        <div>
          <label for="email">Email</label>
          <input id="email" type="email" required placeholder="you@example.com" />
        </div>
        <div>
          <label for="message">Message</label>
          <textarea id="message" required placeholder="Tell us how you want to use Vibe"></textarea>
        </div>
        <button type="submit">Send message</button>
        <div class="contact-note">
          This is a demo contact form — you can wire it up to your backend or email service.
        </div>
      </form>
    </div>
  </section>

  <footer>
    <p>© 2025 Vibe App. All rights reserved.</p>
  </footer>

  <script>
    // Mobile menu toggle
    const menuToggle = document.querySelector('.menu-toggle');
    const nav = document.querySelector('nav');

    menuToggle.addEventListener('click', () => {
      nav.classList.toggle('open');
    });

    // Close menu when clicking a link (mobile)
    nav.querySelectorAll('a').forEach(link => {
      link.addEventListener('click', () => {
        nav.classList.remove('open');
      });
    });

    // Theme toggle
    const themeToggle = document.getElementById('themeToggle');
    const body = document.body;

    function applyStoredTheme() {
      const stored = localStorage.getItem('vibe-theme');
      if (stored === 'light') {
        body.classList.add('light');
        themeToggle.innerHTML = '<span>🌞</span> Theme';
      } else {
        body.classList.remove('light');
        themeToggle.innerHTML = '<span>🌙</span> Theme';
      }
    }

    themeToggle.addEventListener('click', () => {
      body.classList.toggle('light');
      const isLight = body.classList.contains('light');
      localStorage.setItem('vibe-theme', isLight ? 'light' : 'dark');
      applyStoredTheme();
    });

    applyStoredTheme();

    // Scroll helper for "Get the App"
    function scrollToDownload() {
      const el = document.getElementById('download');
      if (el) {
        el.scrollIntoView({ behavior: 'smooth' });
      }
    }

    // Contact form handler
    function handleContactSubmit(event) {
      event.preventDefault();
      const name = document.getElementById('name').value.trim();
      alert('Thanks, ' + (name || 'creator') + '! We will reach out soon.');
      event.target.reset();
    }
  </script>
</body>
</html>
