<!DOCTYPE html>
<html lang="es">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0"/>
  <title>[Tu Nombre] — Developer Profile</title>
  <link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@300;400;600;700&family=Syne:wght@400;700;800&display=swap" rel="stylesheet"/>
  <style>
    *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }

    :root {
      --bg: #080b10;
      --surface: #0d1117;
      --surface2: #161b22;
      --border: #21262d;
      --accent: #00e5a0;
      --accent2: #3b82f6;
      --accent3: #f59e0b;
      --text: #e6edf3;
      --muted: #7d8590;
      --danger: #f85149;
      --font-mono: 'JetBrains Mono', monospace;
      --font-display: 'Syne', sans-serif;
    }

    html { scroll-behavior: smooth; }

    body {
      background: var(--bg);
      color: var(--text);
      font-family: var(--font-mono);
      min-height: 100vh;
      overflow-x: hidden;
      cursor: none;
    }

    /* Custom cursor */
    .cursor {
      width: 12px; height: 12px;
      background: var(--accent);
      border-radius: 50%;
      position: fixed;
      pointer-events: none;
      z-index: 9999;
      transition: transform 0.15s ease, opacity 0.15s ease;
      mix-blend-mode: screen;
    }
    .cursor-ring {
      width: 36px; height: 36px;
      border: 1px solid var(--accent);
      border-radius: 50%;
      position: fixed;
      pointer-events: none;
      z-index: 9998;
      transition: all 0.08s ease;
      opacity: 0.5;
      transform: translate(-50%, -50%);
    }

    /* Grid background */
    body::before {
      content: '';
      position: fixed;
      inset: 0;
      background-image:
        linear-gradient(rgba(0,229,160,0.03) 1px, transparent 1px),
        linear-gradient(90deg, rgba(0,229,160,0.03) 1px, transparent 1px);
      background-size: 40px 40px;
      pointer-events: none;
      z-index: 0;
    }

    /* Noise overlay */
    body::after {
      content: '';
      position: fixed;
      inset: 0;
      background-image: url("data:image/svg+xml,%3Csvg viewBox='0 0 256 256' xmlns='http://www.w3.org/2000/svg'%3E%3Cfilter id='noise'%3E%3CfeTurbulence type='fractalNoise' baseFrequency='0.9' numOctaves='4' stitchTiles='stitch'/%3E%3C/filter%3E%3Crect width='100%25' height='100%25' filter='url(%23noise)' opacity='0.03'/%3E%3C/svg%3E");
      pointer-events: none;
      z-index: 0;
      opacity: 0.4;
    }

    main { position: relative; z-index: 1; max-width: 1000px; margin: 0 auto; padding: 0 24px 80px; }

    /* ─── HERO ─── */
    .hero {
      padding: 100px 0 60px;
      display: grid;
      grid-template-columns: 1fr auto;
      gap: 40px;
      align-items: center;
      animation: fadeUp 0.8s ease both;
    }

    .hero-tag {
      font-size: 11px;
      letter-spacing: 3px;
      color: var(--accent);
      text-transform: uppercase;
      margin-bottom: 16px;
      display: flex;
      align-items: center;
      gap: 10px;
    }
    .hero-tag::before {
      content: '';
      display: inline-block;
      width: 24px; height: 1px;
      background: var(--accent);
    }

    .hero h1 {
      font-family: var(--font-display);
      font-size: clamp(2.4rem, 5vw, 4rem);
      font-weight: 800;
      line-height: 1.05;
      letter-spacing: -1px;
      margin-bottom: 16px;
    }

    .hero h1 span {
      color: transparent;
      -webkit-text-stroke: 1px var(--accent);
    }

    .hero-sub {
      color: var(--muted);
      font-size: 13px;
      line-height: 1.8;
      max-width: 480px;
      margin-bottom: 32px;
    }

    .hero-sub strong { color: var(--accent); font-weight: 600; }

    .hero-badges {
      display: flex;
      gap: 10px;
      flex-wrap: wrap;
    }

    .badge {
      padding: 6px 14px;
      border: 1px solid var(--border);
      border-radius: 4px;
      font-size: 11px;
      letter-spacing: 1px;
      color: var(--muted);
      background: var(--surface2);
      transition: all 0.2s;
    }
    .badge:hover { border-color: var(--accent); color: var(--accent); }

    .avatar-wrap {
      position: relative;
      width: 160px;
      height: 160px;
      flex-shrink: 0;
    }
    .avatar-wrap::before {
      content: '';
      position: absolute;
      inset: -8px;
      border: 1px dashed var(--accent);
      border-radius: 50%;
      animation: spin 20s linear infinite;
      opacity: 0.4;
    }
    .avatar-wrap::after {
      content: '';
      position: absolute;
      inset: -20px;
      border: 1px dashed var(--accent2);
      border-radius: 50%;
      animation: spin 30s linear infinite reverse;
      opacity: 0.2;
    }
    .avatar {
      width: 160px; height: 160px;
      border-radius: 50%;
      background: linear-gradient(135deg, var(--surface2), var(--surface));
      border: 2px solid var(--border);
      display: flex;
      align-items: center;
      justify-content: center;
      font-size: 64px;
      position: relative;
      z-index: 1;
      overflow: hidden;
    }

    /* STATUS BAR */
    .status-bar {
      display: flex;
      align-items: center;
      gap: 8px;
      font-size: 11px;
      color: var(--muted);
      padding: 10px 16px;
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 6px;
      margin-bottom: 60px;
      animation: fadeUp 0.8s 0.2s ease both;
    }
    .status-dot {
      width: 7px; height: 7px;
      background: var(--accent);
      border-radius: 50%;
      animation: pulse 2s ease infinite;
    }
    .status-bar span { color: var(--text); }
    .status-bar .sep { color: var(--border); margin: 0 4px; }

    /* ─── SECTION ─── */
    section {
      margin-bottom: 64px;
      animation: fadeUp 0.6s ease both;
    }

    .section-label {
      display: flex;
      align-items: center;
      gap: 12px;
      font-size: 10px;
      letter-spacing: 3px;
      text-transform: uppercase;
      color: var(--accent);
      margin-bottom: 24px;
    }
    .section-label::after {
      content: '';
      flex: 1;
      height: 1px;
      background: linear-gradient(to right, var(--border), transparent);
    }

    /* ─── ABOUT ─── */
    .about-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 16px;
    }

    .about-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 20px 24px;
      transition: border-color 0.2s, transform 0.2s;
    }
    .about-card:hover { border-color: var(--accent); transform: translateY(-2px); }

    .about-card.wide { grid-column: span 2; }

    .card-icon { font-size: 20px; margin-bottom: 10px; }
    .card-title { font-size: 11px; letter-spacing: 1px; color: var(--muted); text-transform: uppercase; margin-bottom: 6px; }
    .card-body { font-size: 13px; line-height: 1.7; color: var(--text); }
    .card-body strong { color: var(--accent); }

    blockquote.highlight {
      border-left: 3px solid var(--accent);
      padding: 16px 20px;
      background: rgba(0,229,160,0.04);
      border-radius: 0 6px 6px 0;
      font-size: 13px;
      line-height: 1.7;
      color: var(--muted);
      font-style: italic;
    }
    blockquote.highlight em { color: var(--accent); font-style: normal; }

    /* ─── SKILLS ─── */
    .skills-block { margin-bottom: 28px; }
    .skills-block-title {
      font-size: 10px;
      letter-spacing: 2px;
      text-transform: uppercase;
      color: var(--muted);
      margin-bottom: 14px;
      padding-left: 2px;
    }

    .skills-grid {
      display: grid;
      grid-template-columns: repeat(auto-fill, minmax(180px, 1fr));
      gap: 10px;
    }

    .skill-item {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 6px;
      padding: 12px 16px;
      display: flex;
      align-items: center;
      gap: 10px;
      font-size: 12px;
      transition: all 0.2s ease;
      position: relative;
      overflow: hidden;
    }
    .skill-item::after {
      content: '';
      position: absolute;
      bottom: 0; left: 0;
      height: 2px;
      width: var(--level, 0%);
      background: var(--accent);
      transition: width 1s ease;
    }
    .skill-item:hover { border-color: var(--accent); background: var(--surface2); }
    .skill-icon { font-size: 16px; }
    .skill-name { font-weight: 600; color: var(--text); }
    .skill-level { margin-left: auto; font-size: 10px; color: var(--muted); }

    /* ─── PROJECTS ─── */
    .projects-grid {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 14px;
    }

    .project-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 22px;
      transition: all 0.25s ease;
      position: relative;
      overflow: hidden;
      cursor: pointer;
    }
    .project-card::before {
      content: '';
      position: absolute;
      top: 0; left: 0; right: 0;
      height: 2px;
      background: linear-gradient(to right, var(--accent), var(--accent2));
      transform: scaleX(0);
      transform-origin: left;
      transition: transform 0.3s ease;
    }
    .project-card:hover { border-color: var(--accent); transform: translateY(-3px); box-shadow: 0 16px 40px rgba(0,0,0,0.4); }
    .project-card:hover::before { transform: scaleX(1); }

    .project-header { display: flex; align-items: flex-start; justify-content: space-between; margin-bottom: 10px; }
    .project-icon { font-size: 22px; }
    .project-link {
      font-size: 10px;
      color: var(--muted);
      text-decoration: none;
      letter-spacing: 1px;
      border: 1px solid var(--border);
      padding: 4px 8px;
      border-radius: 4px;
      transition: all 0.2s;
    }
    .project-link:hover { color: var(--accent); border-color: var(--accent); }
    .project-name { font-family: var(--font-display); font-size: 15px; font-weight: 700; margin-bottom: 6px; }
    .project-desc { font-size: 12px; color: var(--muted); line-height: 1.6; margin-bottom: 14px; }
    .project-tags { display: flex; gap: 6px; flex-wrap: wrap; }
    .tag {
      font-size: 10px;
      padding: 3px 8px;
      border-radius: 3px;
      background: rgba(0,229,160,0.08);
      color: var(--accent);
      border: 1px solid rgba(0,229,160,0.2);
    }
    .tag.blue { background: rgba(59,130,246,0.08); color: var(--accent2); border-color: rgba(59,130,246,0.2); }
    .tag.amber { background: rgba(245,158,11,0.08); color: var(--accent3); border-color: rgba(245,158,11,0.2); }

    /* ─── STATS ─── */
    .stats-grid {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 14px;
      margin-bottom: 24px;
    }

    .stat-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 20px;
      text-align: center;
      transition: all 0.2s;
    }
    .stat-card:hover { border-color: var(--accent2); }
    .stat-number {
      font-family: var(--font-display);
      font-size: 28px;
      font-weight: 800;
      color: var(--accent);
      display: block;
      line-height: 1;
      margin-bottom: 4px;
    }
    .stat-label { font-size: 10px; letter-spacing: 1px; color: var(--muted); text-transform: uppercase; }

    .github-img-row {
      display: grid;
      grid-template-columns: 1fr 1fr;
      gap: 14px;
    }
    .github-img-row img {
      width: 100%;
      border-radius: 8px;
      border: 1px solid var(--border);
    }

    /* ─── CONTACT ─── */
    .contact-grid {
      display: grid;
      grid-template-columns: repeat(4, 1fr);
      gap: 12px;
    }

    .contact-card {
      background: var(--surface);
      border: 1px solid var(--border);
      border-radius: 8px;
      padding: 18px;
      text-align: center;
      text-decoration: none;
      color: var(--text);
      transition: all 0.25s ease;
      display: flex;
      flex-direction: column;
      align-items: center;
      gap: 8px;
    }
    .contact-card:hover { border-color: var(--accent); transform: translateY(-3px); box-shadow: 0 12px 30px rgba(0,0,0,0.3); }
    .contact-card:hover .contact-icon { transform: scale(1.2); }
    .contact-icon { font-size: 22px; transition: transform 0.2s; }
    .contact-label { font-size: 11px; letter-spacing: 1px; text-transform: uppercase; color: var(--muted); }
    .contact-value { font-size: 12px; color: var(--accent); }

    /* ─── FOOTER ─── */
    footer {
      border-top: 1px solid var(--border);
      padding-top: 24px;
      display: flex;
      align-items: center;
      justify-content: space-between;
      font-size: 11px;
      color: var(--muted);
    }
    footer span { color: var(--danger); }

    /* ─── TERMINAL PROMPT ─── */
    .prompt {
      font-size: 12px;
      color: var(--muted);
      margin-bottom: 6px;
    }
    .prompt .p-user { color: var(--accent); }
    .prompt .p-dir { color: var(--accent2); }
    .prompt .p-sym { color: var(--accent3); }

    /* ─── ANIMATIONS ─── */
    @keyframes fadeUp {
      from { opacity: 0; transform: translateY(20px); }
      to { opacity: 1; transform: translateY(0); }
    }
    @keyframes spin { to { transform: rotate(360deg); } }
    @keyframes pulse {
      0%, 100% { opacity: 1; box-shadow: 0 0 0 0 rgba(0,229,160,0.4); }
      50% { opacity: 0.7; box-shadow: 0 0 0 5px rgba(0,229,160,0); }
    }
    @keyframes blink { 0%,100%{opacity:1} 50%{opacity:0} }

    .blink { animation: blink 1s step-end infinite; }

    /* Delay helpers */
    .d1 { animation-delay: 0.1s; }
    .d2 { animation-delay: 0.2s; }
    .d3 { animation-delay: 0.3s; }
    .d4 { animation-delay: 0.4s; }

    @media (max-width: 680px) {
      .hero { grid-template-columns: 1fr; }
      .avatar-wrap { display: none; }
      .about-grid, .projects-grid, .github-img-row { grid-template-columns: 1fr; }
      .about-card.wide { grid-column: span 1; }
      .stats-grid { grid-template-columns: repeat(2,1fr); }
      .contact-grid { grid-template-columns: repeat(2,1fr); }
    }
  </style>
</head>
<body>

<!-- Custom cursor -->
<div class="cursor" id="cursor"></div>
<div class="cursor-ring" id="cursorRing"></div>

<main>

  <!-- ── HERO ── -->
  <div class="hero">
    <div>
      <div class="hero-tag">Available for projects</div>
      <h1>
        Hola, soy<br>
        <span>[Tu Nombre]</span>
      </h1>
      <p class="hero-sub">
        Desarrollo aplicaciones donde <strong>la IA y la web moderna</strong> se encuentran.
        Full-Stack Developer especializado en experiencias inteligentes, rápidas y escalables.
      </p>
      <div class="hero-badges">
        <span class="badge">React</span>
        <span class="badge">Node.js</span>
        <span class="badge">Python</span>
        <span class="badge">LLMs</span>
        <span class="badge">Open Source</span>
      </div>
    </div>
    <div class="avatar-wrap">
      <div class="avatar">🧑‍💻</div>
    </div>
  </div>

  <!-- STATUS BAR -->
  <div class="status-bar">
    <div class="status-dot"></div>
    <span>Disponible</span>
    <span class="sep">·</span>
    <span style="color:var(--muted)">Basado en</span>
    <span>[Tu Ciudad, País]</span>
    <span class="sep">·</span>
    <span style="color:var(--muted)">Abierto a</span>
    <span>freelance &amp; colaboraciones</span>
    <span class="blink" style="margin-left:auto; color:var(--accent)">_</span>
  </div>

  <!-- ── ABOUT ── -->
  <section class="d1">
    <div class="section-label">// sobre mí</div>

    <blockquote class="highlight" style="margin-bottom:20px">
      "El código es poesía cuando resuelve problemas reales. Mi objetivo: construir herramientas que <em>piensen, escalen y deleiten</em>."
    </blockquote>

    <div class="about-grid">
      <div class="about-card">
        <div class="card-icon">🤖</div>
        <div class="card-title">IA & Web</div>
        <div class="card-body">Especializado en integrar <strong>LLMs, agentes y sistemas RAG</strong> directamente en productos web modernos.</div>
      </div>
      <div class="about-card">
        <div class="card-icon">🌱</div>
        <div class="card-title">En constante aprendizaje</div>
        <div class="card-body">Explorando <strong>arquitecturas multi-agente</strong>, fine-tuning y edge computing para IA en tiempo real.</div>
      </div>
      <div class="about-card">
        <div class="card-icon">🚀</div>
        <div class="card-title">Filosofía</div>
        <div class="card-body">Creo en el <strong>ship fast, iterate faster</strong>. La perfección es el enemigo de lo lanzado.</div>
      </div>
      <div class="about-card">
        <div class="card-icon">🤝</div>
        <div class="card-title">Colaboración</div>
        <div class="card-body">Activo en <strong>open source</strong> y siempre abierto a proyectos con impacto real y equipos que aprenden.</div>
      </div>
    </div>
  </section>

  <!-- ── SKILLS ── -->
  <section class="d2">
    <div class="section-label">// habilidades</div>

    <div class="skills-block">
      <div class="skills-block-title">— Frontend</div>
      <div class="skills-grid">
        <div class="skill-item" style="--level:90%"><span class="skill-icon">⚛️</span><span class="skill-name">React</span><span class="skill-level">90%</span></div>
        <div class="skill-item" style="--level:80%"><span class="skill-icon">▲</span><span class="skill-name">Next.js</span><span class="skill-level">80%</span></div>
        <div class="skill-item" style="--level:85%"><span class="skill-icon">🔷</span><span class="skill-name">TypeScript</span><span class="skill-level">85%</span></div>
        <div class="skill-item" style="--level:90%"><span class="skill-icon">🎨</span><span class="skill-name">Tailwind CSS</span><span class="skill-level">90%</span></div>
      </div>
    </div>

    <div class="skills-block">
      <div class="skills-block-title">— Backend & Cloud</div>
      <div class="skills-grid">
        <div class="skill-item" style="--level:85%"><span class="skill-icon">🟢</span><span class="skill-name">Node.js</span><span class="skill-level">85%</span></div>
        <div class="skill-item" style="--level:75%"><span class="skill-icon">🐍</span><span class="skill-name">Python</span><span class="skill-level">75%</span></div>
        <div class="skill-item" style="--level:70%"><span class="skill-icon">🐘</span><span class="skill-name">PostgreSQL</span><span class="skill-level">70%</span></div>
        <div class="skill-item" style="--level:65%"><span class="skill-icon">🐳</span><span class="skill-name">Docker</span><span class="skill-level">65%</span></div>
      </div>
    </div>

    <div class="skills-block">
      <div class="skills-block-title">— IA & Machine Learning</div>
      <div class="skills-grid">
        <div class="skill-item" style="--level:80%"><span class="skill-icon">🧠</span><span class="skill-name">OpenAI API</span><span class="skill-level">80%</span></div>
        <div class="skill-item" style="--level:70%"><span class="skill-icon">🦜</span><span class="skill-name">LangChain</span><span class="skill-level">70%</span></div>
        <div class="skill-item" style="--level:65%"><span class="skill-icon">🗂️</span><span class="skill-name">Vector DBs</span><span class="skill-level">65%</span></div>
        <div class="skill-item" style="--level:60%"><span class="skill-icon">🤗</span><span class="skill-name">HuggingFace</span><span class="skill-level">60%</span></div>
      </div>
    </div>
  </section>

  <!-- ── PROJECTS ── -->
  <section class="d3">
    <div class="section-label">// proyectos destacados</div>
    <div class="projects-grid">

      <div class="project-card">
        <div class="project-header">
          <span class="project-icon">🤖</span>
          <a href="#" class="project-link">↗ Ver repo</a>
        </div>
        <div class="project-name">[Nombre Proyecto 1]</div>
        <div class="project-desc">App inteligente potenciada con GPT-4 y sistema RAG para [describir caso de uso]. Reducción del 60% en tiempo de respuesta.</div>
        <div class="project-tags">
          <span class="tag">React</span>
          <span class="tag blue">FastAPI</span>
          <span class="tag amber">OpenAI</span>
          <span class="tag">Pinecone</span>
        </div>
      </div>

      <div class="project-card">
        <div class="project-header">
          <span class="project-icon">📊</span>
          <a href="#" class="project-link">↗ Ver repo</a>
        </div>
        <div class="project-name">[Nombre Proyecto 2]</div>
        <div class="project-desc">Dashboard en tiempo real para análisis de [datos]. WebSockets + visualizaciones interactivas para +10k usuarios simultáneos.</div>
        <div class="project-tags">
          <span class="tag">Next.js</span>
          <span class="tag blue">WebSockets</span>
          <span class="tag amber">PostgreSQL</span>
        </div>
      </div>

      <div class="project-card">
        <div class="project-header">
          <span class="project-icon">🧬</span>
          <a href="#" class="project-link">↗ Ver repo</a>
        </div>
        <div class="project-name">[Nombre Proyecto 3]</div>
        <div class="project-desc">Agente autónomo con memoria persistente capaz de [tarea]. Arquitectura multi-herramienta con LangChain y Redis.</div>
        <div class="project-tags">
          <span class="tag">Python</span>
          <span class="tag blue">LangChain</span>
          <span class="tag amber">Redis</span>
        </div>
      </div>

      <div class="project-card" style="border-style:dashed; display:flex; align-items:center; justify-content:center; flex-direction:column; gap:8px; min-height:160px">
        <span style="font-size:28px">+</span>
        <span style="font-size:12px; color:var(--muted)">Más proyectos en GitHub</span>
        <a href="https://github.com/tu-usuario" style="font-size:11px; color:var(--accent); text-decoration:none; letter-spacing:1px">↗ github.com/tu-usuario</a>
      </div>

    </div>
  </section>

  <!-- ── STATS ── -->
  <section class="d4">
    <div class="section-label">// estadísticas</div>

    <div class="stats-grid">
      <div class="stat-card">
        <span class="stat-number" data-target="42">0</span>
        <span class="stat-label">Repositorios</span>
      </div>
      <div class="stat-card">
        <span class="stat-number" data-target="1200">0</span>
        <span class="stat-label">Commits / año</span>
      </div>
      <div class="stat-card">
        <span class="stat-number" data-target="15">0</span>
        <span class="stat-label">PRs merged</span>
      </div>
      <div class="stat-card">
        <span class="stat-number" data-target="8">0</span>
        <span class="stat-label">Proyectos IA</span>
      </div>
    </div>

    <!-- Reemplaza 'tu-usuario' con tu GitHub username -->
    <div class="github-img-row">
      <img src="https://github-readme-stats.vercel.app/api?username=tu-usuario&show_icons=true&theme=chartreuse-dark&hide_border=true&bg_color=0d1117&title_color=00e5a0&text_color=7d8590&icon_color=00e5a0" alt="GitHub Stats" />
      <img src="https://github-readme-stats.vercel.app/api/top-langs/?username=tu-usuario&layout=compact&theme=chartreuse-dark&hide_border=true&bg_color=0d1117&title_color=00e5a0&text_color=7d8590" alt="Top Languages" />
    </div>
  </section>

  <!-- ── CONTACT ── -->
  <section>
    <div class="section-label">// conecta conmigo</div>
    <div class="contact-grid">
      <a href="https://linkedin.com/in/tu-usuario" class="contact-card" target="_blank">
        <span class="contact-icon">💼</span>
        <span class="contact-label">LinkedIn</span>
        <span class="contact-value">tu-usuario</span>
      </a>
      <a href="https://github.com/tu-usuario" class="contact-card" target="_blank">
        <span class="contact-icon">🐙</span>
        <span class="contact-label">GitHub</span>
        <span class="contact-value">tu-usuario</span>
      </a>
      <a href="https://x.com/tu-usuario" class="contact-card" target="_blank">
        <span class="contact-icon">𝕏</span>
        <span class="contact-label">Twitter / X</span>
        <span class="contact-value">@tu-usuario</span>
      </a>
      <a href="mailto:tu@email.com" class="contact-card">
        <span class="contact-icon">📬</span>
        <span class="contact-label">Email</span>
        <span class="contact-value">tu@email.com</span>
      </a>
    </div>
  </section>

  <!-- ── FOOTER ── -->
  <footer>
    <div class="prompt">
      <span class="p-user">tu-usuario</span><span style="color:var(--muted)">@</span><span class="p-dir">github</span><span class="p-sym"> ~$</span>
      <span style="color:var(--text)"> git commit -m <span style="color:var(--accent3)">"keep building"</span></span>
    </div>
    <div>Made with <span>♥</span> &amp; mucho café · <span style="color:var(--muted)">2025</span></div>
  </footer>

</main>

<script>
  // Custom cursor
  const cursor = document.getElementById('cursor');
  const ring = document.getElementById('cursorRing');
  let mx = 0, my = 0, rx = 0, ry = 0;

  document.addEventListener('mousemove', e => {
    mx = e.clientX; my = e.clientY;
    cursor.style.left = mx - 6 + 'px';
    cursor.style.top = my - 6 + 'px';
  });

  (function animRing() {
    rx += (mx - rx) * 0.12;
    ry += (my - ry) * 0.12;
    ring.style.left = rx + 'px';
    ring.style.top = ry + 'px';
    requestAnimationFrame(animRing);
  })();

  document.querySelectorAll('a, button, .project-card, .skill-item').forEach(el => {
    el.addEventListener('mouseenter', () => { cursor.style.transform = 'scale(2)'; ring.style.opacity = '0.9'; });
    el.addEventListener('mouseleave', () => { cursor.style.transform = 'scale(1)'; ring.style.opacity = '0.5'; });
  });

  // Animated counters
  function animateCounter(el) {
    const target = +el.dataset.target;
    const duration = 1600;
    const start = performance.now();
    (function update(now) {
      const p = Math.min((now - start) / duration, 1);
      const ease = 1 - Math.pow(1 - p, 3);
      el.textContent = Math.floor(ease * target);
      if (p < 1) requestAnimationFrame(update);
      else el.textContent = target;
    })(start);
  }

  const obs = new IntersectionObserver(entries => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.querySelectorAll('[data-target]').forEach(animateCounter);
        obs.unobserve(e.target);
      }
    });
  }, { threshold: 0.3 });

  document.querySelectorAll('.stats-grid').forEach(el => obs.observe(el));

  // Skill bars animate on scroll
  const skillObs = new IntersectionObserver(entries => {
    entries.forEach(e => {
      if (e.isIntersecting) {
        e.target.style.setProperty('--level', e.target.getAttribute('style').match(/--level:([\d%]+)/)?.[1] || '0%');
      }
    });
  }, { threshold: 0.2 });

  document.querySelectorAll('.skill-item').forEach(el => skillObs.observe(el));
</script>
</body>
</html>
