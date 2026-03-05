<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>Awais Khan — WordPress & Frontend Developer</title>
<link href="https://fonts.googleapis.com/css2?family=Syne:wght@400;600;700;800&family=Space+Mono:wght@400;700&display=swap" rel="stylesheet"/>
<style>
  :root {
    --bg: #050810;
    --surface: #0d1117;
    --card: #111827;
    --border: #1f2937;
    --accent: #6ee7b7;
    --accent2: #818cf8;
    --accent3: #f472b6;
    --text: #f1f5f9;
    --muted: #94a3b8;
    --wp: #21759b;
  }

  *, *::before, *::after { margin: 0; padding: 0; box-sizing: border-box; }

  html { scroll-behavior: smooth; }

  body {
    background: var(--bg);
    color: var(--text);
    font-family: 'Space Mono', monospace;
    overflow-x: hidden;
    cursor: none;
  }

  /* Custom cursor */
  .cursor {
    width: 12px; height: 12px;
    background: var(--accent);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none;
    z-index: 9999;
    transform: translate(-50%, -50%);
    transition: transform 0.1s, width 0.2s, height 0.2s, background 0.2s;
    mix-blend-mode: screen;
  }
  .cursor-ring {
    width: 36px; height: 36px;
    border: 1px solid var(--accent2);
    border-radius: 50%;
    position: fixed; top: 0; left: 0;
    pointer-events: none;
    z-index: 9998;
    transform: translate(-50%, -50%);
    transition: transform 0.15s ease-out, border-color 0.2s;
    opacity: 0.6;
  }

  /* Noise overlay */
  body::before {
    content: '';
    position: fixed; inset: 0;
    background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 200 200' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='n'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23n)' opacity='0.04'/%3E%3C/svg%3E");
    pointer-events: none;
    z-index: 1000;
    opacity: 0.4;
  }

  /* Grid bg */
  body::after {
    content: '';
    position: fixed; inset: 0;
    background-image:
      linear-gradient(rgba(110,231,183,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(110,231,183,0.03) 1px, transparent 1px);
    background-size: 60px 60px;
    pointer-events: none;
    z-index: 0;
  }

  /* ===== HERO ===== */
  .hero {
    min-height: 100vh;
    display: grid;
    grid-template-columns: 1fr 1fr;
    position: relative;
    z-index: 1;
    overflow: hidden;
  }

  .hero-left {
    display: flex;
    flex-direction: column;
    justify-content: center;
    padding: 80px 60px 80px 80px;
    position: relative;
  }

  .hero-tag {
    display: inline-flex;
    align-items: center;
    gap: 8px;
    font-size: 11px;
    letter-spacing: 0.2em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 32px;
    opacity: 0;
    animation: fadeUp 0.6s 0.2s forwards;
  }
  .hero-tag::before {
    content: '';
    width: 24px; height: 1px;
    background: var(--accent);
  }

  .hero-name {
    font-family: 'Syne', sans-serif;
    font-size: clamp(52px, 6vw, 88px);
    font-weight: 800;
    line-height: 1;
    letter-spacing: -0.03em;
    opacity: 0;
    animation: fadeUp 0.7s 0.35s forwards;
  }

  .hero-name .line2 {
    display: block;
    background: linear-gradient(135deg, var(--accent) 0%, var(--accent2) 100%);
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
  }

  .hero-role {
    margin-top: 24px;
    font-size: 13px;
    color: var(--muted);
    line-height: 1.8;
    max-width: 400px;
    opacity: 0;
    animation: fadeUp 0.7s 0.5s forwards;
  }

  .hero-cta {
    display: flex;
    gap: 16px;
    margin-top: 48px;
    opacity: 0;
    animation: fadeUp 0.7s 0.65s forwards;
  }

  .btn {
    padding: 14px 28px;
    font-family: 'Space Mono', monospace;
    font-size: 11px;
    letter-spacing: 0.12em;
    text-transform: uppercase;
    text-decoration: none;
    border-radius: 4px;
    transition: all 0.25s;
    cursor: none;
  }
  .btn-primary {
    background: var(--accent);
    color: #050810;
    font-weight: 700;
    border: 1px solid var(--accent);
  }
  .btn-primary:hover { background: transparent; color: var(--accent); box-shadow: 0 0 20px rgba(110,231,183,0.3); }
  .btn-outline {
    border: 1px solid var(--border);
    color: var(--muted);
  }
  .btn-outline:hover { border-color: var(--accent2); color: var(--accent2); }

  .hero-right {
    display: flex;
    align-items: center;
    justify-content: center;
    position: relative;
    padding: 80px;
  }

  /* Animated orbit */
  .orbit-wrap {
    position: relative;
    width: 340px; height: 340px;
    opacity: 0;
    animation: fadeIn 1s 0.8s forwards;
  }

  .orbit-center {
    position: absolute;
    top: 50%; left: 50%;
    transform: translate(-50%, -50%);
    width: 120px; height: 120px;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    border-radius: 50%;
    display: flex; align-items: center; justify-content: center;
    font-family: 'Syne', sans-serif;
    font-size: 36px; font-weight: 800;
    color: #050810;
    box-shadow: 0 0 60px rgba(110,231,183,0.4);
    z-index: 2;
  }

  .orbit {
    position: absolute; inset: 0;
    border-radius: 50%;
    border: 1px dashed rgba(129,140,248,0.2);
  }
  .orbit-1 { animation: spin 12s linear infinite; }
  .orbit-2 { inset: -30px; border-color: rgba(110,231,183,0.15); animation: spin 20s linear infinite reverse; }
  .orbit-3 { inset: -65px; border-color: rgba(244,114,182,0.1); animation: spin 30s linear infinite; }

  .orbit-dot {
    position: absolute;
    width: 10px; height: 10px;
    border-radius: 50%;
    top: -5px; left: 50%;
    transform: translateX(-50%);
  }
  .dot-1 { background: var(--accent2); box-shadow: 0 0 10px var(--accent2); }
  .dot-2 { background: var(--accent); box-shadow: 0 0 10px var(--accent); top: calc(100% - 5px); }
  .dot-3 { background: var(--accent3); box-shadow: 0 0 10px var(--accent3); }

  .orbit-icons {
    position: absolute; inset: -30px;
  }
  .orbit-icon {
    position: absolute;
    font-size: 22px;
    background: var(--card);
    border: 1px solid var(--border);
    width: 44px; height: 44px;
    border-radius: 10px;
    display: flex; align-items: center; justify-content: center;
    box-shadow: 0 4px 20px rgba(0,0,0,0.4);
  }
  .oi-1 { top: -10px; left: 50%; transform: translateX(-50%); }
  .oi-2 { right: -10px; top: 50%; transform: translateY(-50%); }
  .oi-3 { bottom: -10px; left: 50%; transform: translateX(-50%); }
  .oi-4 { left: -10px; top: 50%; transform: translateY(-50%); }

  /* divider */
  .divider {
    height: 1px;
    background: linear-gradient(90deg, transparent, var(--border), transparent);
    margin: 0 80px;
    position: relative; z-index: 1;
  }

  /* ===== SECTION SHARED ===== */
  section {
    position: relative; z-index: 1;
    padding: 100px 80px;
  }

  .section-label {
    font-size: 10px;
    letter-spacing: 0.3em;
    text-transform: uppercase;
    color: var(--accent);
    display: flex; align-items: center; gap: 12px;
    margin-bottom: 20px;
  }
  .section-label::after {
    content: '';
    flex: 1;
    height: 1px;
    background: linear-gradient(90deg, var(--border), transparent);
  }

  .section-title {
    font-family: 'Syne', sans-serif;
    font-size: clamp(32px, 4vw, 52px);
    font-weight: 800;
    letter-spacing: -0.02em;
    line-height: 1.1;
    margin-bottom: 60px;
  }

  /* ===== ABOUT ===== */
  .about-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 60px;
    align-items: start;
  }

  .about-text p {
    color: var(--muted);
    font-size: 13px;
    line-height: 2;
    margin-bottom: 20px;
  }

  .about-stats {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 20px;
  }

  .stat-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 12px;
    padding: 28px;
    position: relative;
    overflow: hidden;
    transition: border-color 0.3s, transform 0.3s;
  }
  .stat-card:hover { border-color: var(--accent); transform: translateY(-3px); }
  .stat-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    opacity: 0;
    transition: opacity 0.3s;
  }
  .stat-card:hover::before { opacity: 1; }

  .stat-num {
    font-family: 'Syne', sans-serif;
    font-size: 42px;
    font-weight: 800;
    background: linear-gradient(135deg, var(--accent), var(--accent2));
    -webkit-background-clip: text;
    -webkit-text-fill-color: transparent;
    background-clip: text;
    line-height: 1;
  }
  .stat-label {
    font-size: 11px;
    color: var(--muted);
    margin-top: 8px;
    text-transform: uppercase;
    letter-spacing: 0.1em;
  }

  /* ===== SKILLS ===== */
  .skills-section { background: var(--surface); }

  .skills-grid {
    display: grid;
    grid-template-columns: repeat(4, 1fr);
    gap: 16px;
  }

  .skill-pill {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 8px;
    padding: 16px 20px;
    display: flex;
    align-items: center;
    gap: 12px;
    font-size: 12px;
    color: var(--text);
    transition: all 0.3s;
    cursor: none;
  }
  .skill-pill:hover {
    border-color: var(--accent2);
    transform: scale(1.03);
    box-shadow: 0 0 20px rgba(129,140,248,0.15);
  }
  .skill-icon {
    font-size: 20px;
    width: 36px; height: 36px;
    background: var(--surface);
    border-radius: 8px;
    display: flex; align-items: center; justify-content: center;
    flex-shrink: 0;
  }

  /* ===== PROJECTS ===== */
  .projects-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 24px;
  }

  .project-card {
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 36px;
    position: relative;
    overflow: hidden;
    transition: all 0.35s;
    cursor: none;
  }
  .project-card:hover {
    border-color: rgba(110,231,183,0.4);
    transform: translateY(-6px);
    box-shadow: 0 20px 60px rgba(0,0,0,0.5), 0 0 40px rgba(110,231,183,0.08);
  }
  .project-card::after {
    content: '';
    position: absolute;
    top: -60px; right: -60px;
    width: 160px; height: 160px;
    border-radius: 50%;
    background: radial-gradient(circle, rgba(110,231,183,0.07), transparent);
    transition: opacity 0.35s;
    opacity: 0;
  }
  .project-card:hover::after { opacity: 1; }

  .project-num {
    font-family: 'Syne', sans-serif;
    font-size: 64px;
    font-weight: 800;
    color: rgba(255,255,255,0.04);
    position: absolute;
    top: 16px; right: 24px;
    line-height: 1;
  }
  .project-emoji {
    font-size: 32px;
    margin-bottom: 20px;
    display: block;
  }
  .project-name {
    font-family: 'Syne', sans-serif;
    font-size: 20px;
    font-weight: 700;
    margin-bottom: 12px;
    color: var(--text);
  }
  .project-desc {
    font-size: 12px;
    color: var(--muted);
    line-height: 1.9;
    margin-bottom: 24px;
  }
  .project-tags {
    display: flex; flex-wrap: wrap; gap: 8px;
  }
  .tag {
    font-size: 10px;
    padding: 4px 10px;
    border-radius: 20px;
    letter-spacing: 0.08em;
    text-transform: uppercase;
  }
  .tag-green { background: rgba(110,231,183,0.1); color: var(--accent); border: 1px solid rgba(110,231,183,0.2); }
  .tag-purple { background: rgba(129,140,248,0.1); color: var(--accent2); border: 1px solid rgba(129,140,248,0.2); }
  .tag-pink { background: rgba(244,114,182,0.1); color: var(--accent3); border: 1px solid rgba(244,114,182,0.2); }

  /* ===== CONNECT ===== */
  .connect-section {
    text-align: center;
    background: var(--surface);
  }

  .connect-card {
    display: inline-block;
    background: var(--card);
    border: 1px solid var(--border);
    border-radius: 24px;
    padding: 60px 80px;
    max-width: 640px;
    position: relative;
    overflow: hidden;
  }
  .connect-card::before {
    content: '';
    position: absolute;
    inset: 0;
    background: radial-gradient(ellipse at 50% 0%, rgba(110,231,183,0.06), transparent 70%);
  }

  .connect-card h2 {
    font-family: 'Syne', sans-serif;
    font-size: 40px;
    font-weight: 800;
    margin-bottom: 16px;
  }
  .connect-card p {
    color: var(--muted);
    font-size: 12px;
    line-height: 2;
    margin-bottom: 40px;
  }

  .social-links {
    display: flex;
    justify-content: center;
    gap: 16px;
    flex-wrap: wrap;
  }

  .social-btn {
    display: flex;
    align-items: center;
    gap: 10px;
    padding: 12px 22px;
    border-radius: 8px;
    font-size: 11px;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    text-decoration: none;
    transition: all 0.25s;
    cursor: none;
  }
  .s-linkedin { background: rgba(10,102,194,0.15); color: #5c9eff; border: 1px solid rgba(10,102,194,0.3); }
  .s-linkedin:hover { background: rgba(10,102,194,0.3); box-shadow: 0 0 20px rgba(10,102,194,0.3); }
  .s-email { background: rgba(110,231,183,0.1); color: var(--accent); border: 1px solid rgba(110,231,183,0.2); }
  .s-email:hover { background: rgba(110,231,183,0.2); box-shadow: 0 0 20px rgba(110,231,183,0.2); }
  .s-portfolio { background: rgba(244,114,182,0.1); color: var(--accent3); border: 1px solid rgba(244,114,182,0.2); }
  .s-portfolio:hover { background: rgba(244,114,182,0.2); box-shadow: 0 0 20px rgba(244,114,182,0.2); }

  /* ===== FOOTER ===== */
  footer {
    position: relative; z-index: 1;
    padding: 40px 80px;
    border-top: 1px solid var(--border);
    display: flex;
    justify-content: space-between;
    align-items: center;
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 0.1em;
  }

  /* ===== ANIMATIONS ===== */
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(24px); }
    to   { opacity: 1; transform: translateY(0); }
  }
  @keyframes fadeIn {
    from { opacity: 0; }
    to   { opacity: 1; }
  }
  @keyframes spin {
    to { transform: rotate(360deg); }
  }
  @keyframes pulse {
    0%, 100% { box-shadow: 0 0 20px rgba(110,231,183,0.2); }
    50% { box-shadow: 0 0 50px rgba(110,231,183,0.5); }
  }

  .animate-on-scroll {
    opacity: 0;
    transform: translateY(30px);
    transition: opacity 0.6s ease, transform 0.6s ease;
  }
  .animate-on-scroll.visible {
    opacity: 1;
    transform: none;
  }

  /* Glowing line left side */
  .hero::before {
    content: '';
    position: absolute;
    left: 50%; top: 10%; bottom: 10%;
    width: 1px;
    background: linear-gradient(180deg, transparent, var(--accent2), transparent);
    opacity: 0.3;
  }
</style>
</head>
<body>

<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<!-- ===== HERO ===== -->
<section class="hero">
  <div class="hero-left">
    <div class="hero-tag">Available for Projects</div>
    <h1 class="hero-name">
      Awais<br>
      <span class="line2">Khan.</span>
    </h1>
    <p class="hero-role">
      WordPress & Frontend Developer from Pakistan 🇵🇰<br>
      Crafting fast, scalable, and beautiful web experiences<br>
      with clean code and pixel-perfect design.
    </p>
    <div class="hero-cta">
      <a href="mailto:awaiskhan.raees123@gmail.com" class="btn btn-primary">Get In Touch</a>
      <a href="https://www.linkedin.com/in/awais-khan-487203308/" class="btn btn-outline" target="_blank">LinkedIn →</a>
    </div>
  </div>

  <div class="hero-right">
    <div class="orbit-wrap">
      <div class="orbit orbit-1">
        <div class="orbit-dot dot-1"></div>
        <div class="orbit-dot dot-2"></div>
      </div>
      <div class="orbit orbit-2">
        <div class="orbit-dot dot-3"></div>
      </div>
      <div class="orbit orbit-3"></div>
      <div class="orbit-center">AK</div>
      <div class="orbit-icons">
        <div class="orbit-icon oi-1">🌐</div>
        <div class="orbit-icon oi-2">⚡</div>
        <div class="orbit-icon oi-3">🛒</div>
        <div class="orbit-icon oi-4">🎨</div>
      </div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ===== ABOUT ===== -->
<section>
  <div class="section-label">01 — About</div>
  <h2 class="section-title animate-on-scroll">Building the web,<br><span style="color:var(--accent)">one pixel</span> at a time.</h2>
  <div class="about-grid">
    <div class="about-text animate-on-scroll">
      <p>I'm a dedicated WordPress and Frontend Developer with a passion for creating websites that are not just visually appealing, but also optimized for performance and conversion.</p>
      <p>My workflow blends custom PHP development, ACF, Elementor, and modern JavaScript to deliver solutions that stand out. I obsess over details — from load times to layout precision.</p>
      <p>Currently expanding into <span style="color:var(--accent)">Headless WordPress</span>, <span style="color:var(--accent2)">React</span>, and <span style="color:var(--accent3)">Gutenberg Block Development</span>. My goal for 2025: build my own WordPress plugin and contribute to open-source.</p>
    </div>
    <div class="about-stats animate-on-scroll">
      <div class="stat-card">
        <div class="stat-num">50+</div>
        <div class="stat-label">Projects Delivered</div>
      </div>
      <div class="stat-card">
        <div class="stat-num">3+</div>
        <div class="stat-label">Years Experience</div>
      </div>
      <div class="stat-card">
        <div class="stat-num">100%</div>
        <div class="stat-label">Client Satisfaction</div>
      </div>
      <div class="stat-card">
        <div class="stat-num">∞</div>
        <div class="stat-label">Lines of Code</div>
      </div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ===== SKILLS ===== -->
<section class="skills-section">
  <div class="section-label">02 — Skills</div>
  <h2 class="section-title animate-on-scroll">My Tech <span style="color:var(--accent2)">Arsenal</span></h2>
  <div class="skills-grid animate-on-scroll">
    <div class="skill-pill"><span class="skill-icon">🌐</span> WordPress</div>
    <div class="skill-pill"><span class="skill-icon">🛒</span> WooCommerce</div>
    <div class="skill-pill"><span class="skill-icon">🐘</span> PHP</div>
    <div class="skill-pill"><span class="skill-icon">⚡</span> JavaScript</div>
    <div class="skill-pill"><span class="skill-icon">🏗️</span> HTML5</div>
    <div class="skill-pill"><span class="skill-icon">🎨</span> CSS3</div>
    <div class="skill-pill"><span class="skill-icon">💨</span> Tailwind CSS</div>
    <div class="skill-pill"><span class="skill-icon">🅱️</span> Bootstrap</div>
    <div class="skill-pill"><span class="skill-icon">🔧</span> ACF</div>
    <div class="skill-pill"><span class="skill-icon">⚙️</span> Elementor</div>
    <div class="skill-pill"><span class="skill-icon">🔀</span> Git & GitHub</div>
    <div class="skill-pill"><span class="skill-icon">🎭</span> Figma</div>
    <div class="skill-pill"><span class="skill-icon">🔍</span> SEO & Performance</div>
    <div class="skill-pill"><span class="skill-icon">🌍</span> REST API</div>
    <div class="skill-pill"><span class="skill-icon">🗄️</span> phpMyAdmin</div>
    <div class="skill-pill"><span class="skill-icon">⚛️</span> React (Learning)</div>
  </div>
</section>

<div class="divider"></div>

<!-- ===== PROJECTS ===== -->
<section>
  <div class="section-label">03 — Projects</div>
  <h2 class="section-title animate-on-scroll">Highlight <span style="color:var(--accent3)">Works</span></h2>
  <div class="projects-grid">
    <div class="project-card animate-on-scroll">
      <div class="project-num">01</div>
      <span class="project-emoji">🛒</span>
      <div class="project-name">WooCommerce Quote Builder</div>
      <p class="project-desc">Built a custom B2B quote request system for clients who need pricing negotiations before checkout. Used AJAX for smooth async requests and ACF for flexible data management.</p>
      <div class="project-tags">
        <span class="tag tag-green">WooCommerce</span>
        <span class="tag tag-purple">AJAX</span>
        <span class="tag tag-pink">ACF</span>
      </div>
    </div>
    <div class="project-card animate-on-scroll">
      <div class="project-num">02</div>
      <span class="project-emoji">🎨</span>
      <div class="project-name">Elementor Portfolio Theme</div>
      <p class="project-desc">A lightweight, blazing-fast portfolio theme built for creatives. Optimized for Core Web Vitals with minimal dependencies and maximum visual impact.</p>
      <div class="project-tags">
        <span class="tag tag-green">Elementor</span>
        <span class="tag tag-purple">Performance</span>
        <span class="tag tag-pink">CSS3</span>
      </div>
    </div>
    <div class="project-card animate-on-scroll">
      <div class="project-num">03</div>
      <span class="project-emoji">🔐</span>
      <div class="project-name">Membership Site with Paywall</div>
      <p class="project-desc">Full membership system with tiered access levels, automated email workflows, and payment gateway integration using WordPress and Restrict Content Pro.</p>
      <div class="project-tags">
        <span class="tag tag-green">WordPress</span>
        <span class="tag tag-purple">RCP</span>
        <span class="tag tag-pink">PHP</span>
      </div>
    </div>
    <div class="project-card animate-on-scroll">
      <div class="project-num">04</div>
      <span class="project-emoji">🔄</span>
      <div class="project-name">CRM Data Sync via REST API</div>
      <p class="project-desc">Seamlessly synced WordPress with an external CRM using custom REST API endpoints. Real-time data exchange and bi-directional sync with custom PHP logic.</p>
      <div class="project-tags">
        <span class="tag tag-green">REST API</span>
        <span class="tag tag-purple">PHP</span>
        <span class="tag tag-pink">CRM</span>
      </div>
    </div>
  </div>
</section>

<div class="divider"></div>

<!-- ===== CONNECT ===== -->
<section class="connect-section">
  <div class="connect-card animate-on-scroll">
    <div class="section-label" style="justify-content:center; margin-bottom:16px;">04 — Contact</div>
    <h2>Let's Build<br><span style="background:linear-gradient(135deg,var(--accent),var(--accent2));-webkit-background-clip:text;-webkit-text-fill-color:transparent;background-clip:text;">Something Great.</span></h2>
    <p>Have a project in mind? Looking for a WordPress developer<br>who cares about performance and design? Let's talk.</p>
    <div class="social-links">
      <a href="https://www.linkedin.com/in/awais-khan-487203308/" class="social-btn s-linkedin" target="_blank">
        💼 LinkedIn
      </a>
      <a href="mailto:awaiskhan.raees123@gmail.com" class="social-btn s-email">
        📧 Email Me
      </a>
      <a href="#" class="social-btn s-portfolio">
        🌐 Portfolio
      </a>
    </div>
  </div>
</section>

<footer>
  <span>© 2025 Awais Khan</span>
  <span style="color:var(--accent)">WordPress & Frontend Developer</span>
  <span>Pakistan 🇵🇰</span>
</footer>

<script>
  // Custom cursor
  const cursor = document.getElementById('cursor');
  const ring = document.getElementById('cursorRing');
  let mx = 0, my = 0, rx = 0, ry = 0;

  document.addEventListener('mousemove', e => {
    mx = e.clientX; my = e.clientY;
    cursor.style.left = mx + 'px';
    cursor.style.top = my + 'px';
  });

  function animateRing() {
    rx += (mx - rx) * 0.12;
    ry += (my - ry) * 0.12;
    ring.style.left = rx + 'px';
    ring.style.top = ry + 'px';
    requestAnimationFrame(animateRing);
  }
  animateRing();

  document.querySelectorAll('a, button, .skill-pill, .project-card, .stat-card').forEach(el => {
    el.addEventListener('mouseenter', () => {
      cursor.style.width = '20px';
      cursor.style.height = '20px';
      ring.style.borderColor = 'var(--accent)';
    });
    el.addEventListener('mouseleave', () => {
      cursor.style.width = '12px';
      cursor.style.height = '12px';
      ring.style.borderColor = 'var(--accent2)';
    });
  });

  // Scroll animations
  const observer = new IntersectionObserver((entries) => {
    entries.forEach((entry, i) => {
      if (entry.isIntersecting) {
        setTimeout(() => entry.target.classList.add('visible'), i * 80);
      }
    });
  }, { threshold: 0.1 });

  document.querySelectorAll('.animate-on-scroll').forEach(el => observer.observe(el));
</script>
</body>
</html>
