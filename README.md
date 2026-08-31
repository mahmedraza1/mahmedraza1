<!DOCTYPE html>
<html lang="en" class="scroll-smooth">
<head>
  <meta charset="UTF-8" />
  <meta name="viewport" content="width=device-width, initial-scale=1.0" />
  <title>~/ mahmedraza1</title>
  <script src="https://cdn.tailwindcss.com"></script>
  <link rel="preconnect" href="https://fonts.googleapis.com" />
  <link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:ital,wght@0,300;0,400;0,500;0,700;1,400&family=Fira+Code:wght@300;400;500;600&display=swap" rel="stylesheet" />
  <script>
    tailwind.config = {
      theme: {
        extend: {
          fontFamily: {
            mono: ['JetBrains Mono', 'Fira Code', 'monospace'],
          },
          colors: {
            term: {
              bg:      '#0d0f0d',
              surface: '#111411',
              panel:   '#141814',
              border:  '#1e2a1e',
              green:   '#39d353',
              lime:    '#a8ff78',
              cyan:    '#00ffcc',
              yellow:  '#ffe066',
              red:     '#ff5555',
              blue:    '#6cb6ff',
              muted:   '#4a6349',
              text:    '#c8e6c9',
              dim:     '#1a221a',
            }
          },
          animation: {
            'blink':  'blink 1s step-end infinite',
            'scan':   'scan 8s linear infinite',
            'fadeup': 'fadeup 0.6s ease forwards',
            'glow':   'glow 3s ease-in-out infinite',
          },
          keyframes: {
            blink:  { '0%,100%': {opacity:'1'}, '50%': {opacity:'0'} },
            scan:   { '0%': {transform:'translateY(-100%)'}, '100%': {transform:'translateY(100vh)'} },
            fadeup: { 'from': {opacity:'0',transform:'translateY(20px)'}, 'to': {opacity:'1',transform:'translateY(0)'} },
            glow:   {
              '0%,100%': {textShadow:'0 0 8px #39d353, 0 0 20px #39d35366'},
              '50%':     {textShadow:'0 0 14px #39d353, 0 0 40px #39d35399'},
            },
          }
        }
      }
    }
  </script>
  <style>
    *, *::before, *::after { box-sizing: border-box; }
    html, body {
      background: #0d0f0d;
      color: #c8e6c9;
      font-family: 'JetBrains Mono', 'Fira Code', monospace;
    }
    /* CRT scanlines */
    body::after {
      content: '';
      position: fixed; inset: 0;
      background: repeating-linear-gradient(
        0deg, transparent, transparent 2px,
        rgba(0,0,0,0.07) 2px, rgba(0,0,0,0.07) 4px
      );
      pointer-events: none;
      z-index: 9999;
    }
    .scanline {
      position: fixed; top: 0; left: 0; right: 0; height: 3px;
      background: linear-gradient(transparent, rgba(57,211,83,0.1), transparent);
      animation: scan 8s linear infinite;
      pointer-events: none; z-index: 9998;
    }
    ::-webkit-scrollbar { width: 4px; }
    ::-webkit-scrollbar-track { background: #0d0f0d; }
    ::-webkit-scrollbar-thumb { background: #1e2a1e; }
    ::-webkit-scrollbar-thumb:hover { background: #39d353; }
    .glow       { animation: glow 3s ease-in-out infinite; }
    .glow-sm    { text-shadow: 0 0 6px #39d353aa; }
    .term-win   { border: 1px solid #1e2a1e; background: #111411; }
    .term-bar   { background: #141814; border-bottom: 1px solid #1e2a1e; padding: 8px 14px; display:flex; align-items:center; gap:8px; }
    .dot        { width:10px; height:10px; border-radius:50%; }
    .prompt::before      { content:'$ '; color:#39d353; }
    .prompt-root::before { content:'# '; color:#ff5555; }
    .comment::before     { content:'# '; color:#4a6349; }
    .reveal { opacity:0; transform:translateY(16px); transition:opacity .5s ease, transform .5s ease; }
    .reveal.in { opacity:1; transform:none; }
    .proj-card  { transition: border-color .2s, background .2s; }
    .proj-card:hover { border-color:#39d353!important; background:#0f1a0f!important; }
    .proj-card:hover .proj-title { color:#39d353; text-shadow:0 0 8px #39d35388; }
    .skill-pill { transition: all .15s; cursor:default; }
    .skill-pill:hover { background:#39d353; color:#0d0f0d; }
    .nav-link   { transition: color .15s; }
    .nav-link:hover { color:#39d353; text-shadow:0 0 8px #39d35366; }
    ::selection { background:#39d35333; color:#a8ff78; }
  </style>
</head>
<body class="min-h-screen">

  <div class="scanline"></div>

  <!-- NAV -->
  <nav class="fixed top-0 left-0 right-0 z-50 border-b border-term-border bg-term-bg/90 backdrop-blur-sm">
    <div class="max-w-6xl mx-auto px-6 py-3 flex items-center justify-between">
      <div class="flex items-center gap-1.5 text-sm font-mono">
        <span class="text-term-muted">root@mahmedraza1</span>
        <span class="text-term-muted">:</span>
        <span class="text-term-blue">~</span>
        <span class="text-term-muted">#</span>
        <span class="text-term-green ml-1">portfolio.sh</span>
        <span class="inline-block w-2 h-[17px] bg-term-green ml-1 animate-blink align-middle"></span>
      </div>
      <div class="hidden md:flex items-center gap-6 text-xs text-term-muted">
        <a href="#about"    class="nav-link">[1] about</a>
        <a href="#projects" class="nav-link">[2] projects</a>
        <a href="#skills"   class="nav-link">[3] skills</a>
        <a href="#contact"  class="nav-link">[4] contact</a>
        <a href="https://github.com/mahmedraza1" target="_blank" class="nav-link text-term-cyan">[gh] ↗</a>
      </div>
    </div>
  </nav>

  <!-- HERO -->
  <section class="min-h-screen flex items-center pt-20 pb-10 px-6" id="home">
    <div class="max-w-4xl mx-auto w-full">

      <div class="term-win w-full">
        <div class="term-bar">
          <div class="dot bg-term-red"></div>
          <div class="dot bg-term-yellow"></div>
          <div class="dot bg-term-green"></div>
          <span class="text-term-muted text-xs ml-3">bash — 130×38 — mahmedraza1@ubuntu</span>
        </div>

        <div class="p-6 md:p-10 text-sm leading-relaxed space-y-3">

          <!-- Boot lines -->
          <div class="text-xs space-y-0.5">
            <p class="text-term-muted opacity-0 animate-fadeup" style="animation-delay:.1s;animation-fill-mode:forwards">
              [ <span class="text-term-green">  OK  </span> ] Started System Boot
            </p>
            <p class="text-term-muted opacity-0 animate-fadeup" style="animation-delay:.35s;animation-fill-mode:forwards">
              [ <span class="text-term-green">  OK  </span> ] Mounted /dev/portfolio
            </p>
            <p class="text-term-muted opacity-0 animate-fadeup" style="animation-delay:.6s;animation-fill-mode:forwards">
              [ <span class="text-term-green">  OK  </span> ] Loaded developer.service
            </p>
            <p class="text-term-muted opacity-0 animate-fadeup" style="animation-delay:.85s;animation-fill-mode:forwards">
              [ <span class="text-term-cyan"> INFO </span> ] Starting identity resolver...
            </p>
          </div>

          <div class="border-y border-term-dim py-3 my-1 opacity-0 animate-fadeup" style="animation-delay:1.1s;animation-fill-mode:forwards">
            <p class="text-term-muted text-xs">Ubuntu 24.04.1 LTS — kernel 6.8.0-51-generic x86_64</p>
            <p class="text-term-muted text-xs">Last login: Sun May 10 2026 · Session: <span class="text-term-green">active</span></p>
          </div>

          <!-- whoami -->
          <div class="opacity-0 animate-fadeup space-y-3" style="animation-delay:1.4s;animation-fill-mode:forwards">
            <p class="text-term-muted text-xs prompt">whoami</p>
            <div class="pl-4 border-l-2 border-term-dim space-y-1">
              <p class="text-5xl md:text-7xl font-bold tracking-tight glow text-term-green leading-none">Muhammad</p>
              <p class="text-5xl md:text-7xl font-bold tracking-tight text-term-text leading-none">Ahmed <span class="text-term-cyan">Raza</span></p>
            </div>
          </div>

          <!-- cat role -->
          <div class="opacity-0 animate-fadeup space-y-1.5 pt-1" style="animation-delay:1.8s;animation-fill-mode:forwards">
            <p class="text-term-muted text-xs prompt">cat /etc/role</p>
            <div class="pl-4 border-l-2 border-term-dim text-xs md:text-sm text-term-text leading-relaxed">
              Full-stack developer · Linux enthusiast · Builder of things that
              <span class="text-term-green"> just work</span>.<br/>
              Stack: <span class="text-term-cyan">Next.js</span> · <span class="text-term-cyan">React</span> · <span class="text-term-cyan">Node.js</span> ·
              <span class="text-term-yellow">TypeScript</span> · <span class="text-term-yellow">Python</span> · <span class="text-term-blue">Expo</span>
            </div>
          </div>

          <!-- ls -->
          <div class="opacity-0 animate-fadeup space-y-1.5 pt-1" style="animation-delay:2.1s;animation-fill-mode:forwards">
            <p class="text-term-muted text-xs prompt">ls -la ~/ --color=always</p>
            <div class="pl-4 border-l-2 border-term-dim text-xs grid grid-cols-2 md:grid-cols-4 gap-x-6 gap-y-1">
              <span class="text-term-blue">drwx  projects/</span>
              <span class="text-term-blue">drwx  skills/</span>
              <span class="text-term-blue">drwx  contact/</span>
              <span class="text-term-green">-rwx  resume.pdf</span>
            </div>
          </div>

          <!-- CTA prompt -->
          <div class="opacity-0 animate-fadeup flex flex-wrap items-center gap-3 pt-3" style="animation-delay:2.5s;animation-fill-mode:forwards">
            <span class="text-term-green text-xs">root@mahmedraza1:~#</span>
            <a href="#projects" class="text-xs border border-term-green text-term-green px-4 py-1.5 hover:bg-term-green hover:text-term-bg transition-all">cd projects/</a>
            <a href="https://github.com/mahmedraza1" target="_blank" class="text-xs border border-term-cyan text-term-cyan px-4 py-1.5 hover:bg-term-cyan hover:text-term-bg transition-all">open github ↗</a>
            <span class="inline-block w-2.5 h-5 bg-term-green animate-blink"></span>
          </div>

        </div>
      </div>

      <!-- stat bar -->
      <div class="grid grid-cols-2 md:grid-cols-4 border border-term-border border-t-0 text-xs">
        <div class="px-5 py-4 border-r border-term-border">
          <p class="text-term-muted comment mb-1">repos</p>
          <p class="text-2xl font-bold text-term-green glow-sm">8+</p>
        </div>
        <div class="px-5 py-4 border-r border-term-border">
          <p class="text-term-muted comment mb-1">languages</p>
          <p class="text-2xl font-bold text-term-cyan">3</p>
        </div>
        <div class="px-5 py-4 border-r border-term-border">
          <p class="text-term-muted comment mb-1">projects pinned</p>
          <p class="text-2xl font-bold text-term-yellow">6</p>
        </div>
        <div class="px-5 py-4">
          <p class="text-term-muted comment mb-1">session uptime</p>
          <p class="text-xl font-bold text-term-green" id="uptime">00:00:00</p>
        </div>
      </div>

    </div>
  </section>

  <!-- PROJECTS -->
  <section id="projects" class="py-24 px-6">
    <div class="max-w-6xl mx-auto">

      <div class="mb-10 reveal">
        <p class="text-term-muted text-xs prompt mb-1">ls -la ~/projects/ --color=always</p>
        <p class="text-term-muted text-xs">total <span class="text-term-green">6</span> entries · sorted by: <span class="text-term-green">most_interesting</span></p>
      </div>

      <div class="grid md:grid-cols-2 lg:grid-cols-3 gap-px bg-term-border">

        <div class="proj-card border border-term-border bg-term-surface p-6 space-y-3 reveal">
          <div class="flex items-center justify-between text-xs text-term-muted">
            <span>-rwxr-xr-x</span><span class="text-term-yellow">JS · Next.js</span>
          </div>
          <div class="proj-title text-term-text font-bold text-base transition-all">📄 Articly</div>
          <p class="text-term-muted text-xs leading-relaxed">Convert Google Docs to clean HTML + downloadable images in one click. Productivity tool for content workflows.</p>
          <div class="text-xs text-term-muted border-t border-term-dim pt-3 flex items-center justify-between">
            <span class="text-term-green">● active</span>
            <a href="https://github.com/mahmedraza1/Articly" target="_blank" class="text-term-cyan hover:text-term-lime transition-colors">git clone ↗</a>
          </div>
        </div>

        <div class="proj-card border border-term-border bg-term-surface p-6 space-y-3 reveal">
          <div class="flex items-center justify-between text-xs text-term-muted">
            <span>-rwxr-xr-x</span><span class="text-term-yellow">JavaScript</span>
          </div>
          <div class="proj-title text-term-text font-bold text-base transition-all">🕷 FMCSA-Scraper</div>
          <p class="text-term-muted text-xs leading-relaxed">Scrapes FMCSA carrier data with MC number support. Bulk CSV export for downstream analysis.</p>
          <div class="text-xs text-term-muted border-t border-term-dim pt-3 flex items-center justify-between">
            <span class="text-term-green">● active</span>
            <a href="https://github.com/mahmedraza1/FMCSA-Scraper" target="_blank" class="text-term-cyan hover:text-term-lime transition-colors">git clone ↗</a>
          </div>
        </div>

        <div class="proj-card border border-term-border bg-term-surface p-6 space-y-3 reveal">
          <div class="flex items-center justify-between text-xs text-term-muted">
            <span>-rwxr-xr-x</span><span class="text-term-blue">TypeScript · Expo</span>
          </div>
          <div class="proj-title text-term-text font-bold text-base transition-all">📱 Learn.Pk App</div>
          <p class="text-term-muted text-xs leading-relaxed">Full Expo LMS mobile app for Learn.pk. Complete codebase for students and educators on mobile.</p>
          <div class="text-xs text-term-muted border-t border-term-dim pt-3 flex items-center justify-between">
            <span class="text-term-green">● active</span>
            <a href="https://github.com/mahmedraza1/Learn.Pk-Expo-App" target="_blank" class="text-term-cyan hover:text-term-lime transition-colors">git clone ↗</a>
          </div>
        </div>

        <div class="proj-card border border-term-border bg-term-surface p-6 space-y-3 reveal">
          <div class="flex items-center justify-between text-xs text-term-muted">
            <span>-rwxr-xr-x</span><span class="text-term-yellow">JS · Appwrite</span>
          </div>
          <div class="proj-title text-term-text font-bold text-base transition-all">✍ Blog Platform</div>
          <p class="text-term-muted text-xs leading-relaxed">Vite + React frontend with Appwrite backend. Handles auth, storage, and database out of the box.</p>
          <div class="text-xs text-term-muted border-t border-term-dim pt-3 flex items-center justify-between">
            <span class="text-term-green">● active</span>
            <a href="https://github.com/mahmedraza1/Blog" target="_blank" class="text-term-cyan hover:text-term-lime transition-colors">git clone ↗</a>
          </div>
        </div>

        <div class="proj-card border border-term-border bg-term-surface p-6 space-y-3 reveal">
          <div class="flex items-center justify-between text-xs text-term-muted">
            <span>-rwxr-xr-x</span><span class="text-term-yellow">JavaScript</span>
          </div>
          <div class="proj-title text-term-text font-bold text-base transition-all">🗂 MediaGrid</div>
          <p class="text-term-muted text-xs leading-relaxed">Google Drive-like file explorer UI for managing VPS uploads. Clean browser-based file management.</p>
          <div class="text-xs text-term-muted border-t border-term-dim pt-3 flex items-center justify-between">
            <span class="text-term-green">● active</span>
            <a href="https://github.com/mahmedraza1/MediaGrid" target="_blank" class="text-term-cyan hover:text-term-lime transition-colors">git clone ↗</a>
          </div>
        </div>

        <div class="proj-card border border-term-border bg-term-surface p-6 space-y-3 reveal">
          <div class="flex items-center justify-between text-xs text-term-muted">
            <span>-rwxr-xr-x</span><span class="text-term-blue">Python</span>
          </div>
          <div class="proj-title text-term-text font-bold text-base transition-all">🤖 AutoTyper</div>
          <p class="text-term-muted text-xs leading-relaxed">Open-source contribution. Python automation tool for simulating keyboard input programmatically.</p>
          <div class="text-xs text-term-muted border-t border-term-dim pt-3 flex items-center justify-between">
            <span class="text-term-cyan">● contrib</span>
            <a href="https://github.com/bilalmirzatrader/AutoTyper" target="_blank" class="text-term-cyan hover:text-term-lime transition-colors">git clone ↗</a>
          </div>
        </div>

      </div>
      <p class="mt-3 text-xs text-term-muted reveal"><span class="text-term-green">6</span> items · use <span class="text-term-yellow">git clone &lt;url&gt;</span> to grab any project</p>
    </div>
  </section>

  <!-- SKILLS -->
  <section id="skills" class="py-24 px-6 border-y border-term-border bg-term-surface">
    <div class="max-w-6xl mx-auto">

      <div class="mb-10 reveal">
        <p class="text-term-muted text-xs prompt mb-1">cat /etc/skills.conf</p>
      </div>

      <div class="term-win reveal">
        <div class="term-bar">
          <div class="dot bg-term-red"></div>
          <div class="dot bg-term-yellow"></div>
          <div class="dot bg-term-green"></div>
          <span class="text-term-muted text-xs ml-3">/etc/skills.conf — readonly</span>
        </div>
        <div class="p-6 md:p-8 text-xs leading-loose space-y-6">

          <div>
            <p class="text-term-muted mb-2 comment">Frontend</p>
            <div class="flex flex-wrap gap-2">
              <span class="skill-pill border border-term-border px-3 py-1 text-term-cyan">Next.js</span>
              <span class="skill-pill border border-term-border px-3 py-1 text-term-cyan">React</span>
              <span class="skill-pill border border-term-border px-3 py-1 text-term-cyan">Vite</span>
              <span class="skill-pill border border-term-border px-3 py-1 text-term-cyan">Tailwind CSS</span>
              <span class="skill-pill border border-term-border px-3 py-1 text-term-cyan">HTML / CSS</span>
            </div>
          </div>

          <div>
            <p class="text-term-muted mb-2 comment">Languages</p>
            <div class="flex flex-wrap gap-2">
              <span class="skill-pill border border-term-border px-3 py-1 text-term-yellow">TypeScript</span>
              <span class="skill-pill border border-term-border px-3 py-1 text-term-yellow">JavaScript</span>
              <span class="skill-pill border border-term-border px-3 py-1 text-term-yellow">Python</span>
              <span class="skill-pill border border-term-border px-3 py-1 text-term-yellow">Bash / Shell</span>
            </div>
          </div>

          <div>
            <p class="text-term-muted mb-2 comment">Backend & Infra</p>
            <div class="flex flex-wrap gap-2">
              <span class="skill-pill border border-term-border px-3 py-1 text-term-green">Node.js</span>
              <span class="skill-pill border border-term-border px-3 py-1 text-term-green">Appwrite</span>
              <span class="skill-pill border border-term-border px-3 py-1 text-term-green">REST APIs</span>
              <span class="skill-pill border border-term-border px-3 py-1 text-term-green">VPS / Linux</span>
              <span class="skill-pill border border-term-border px-3 py-1 text-term-green">Nginx</span>
            </div>
          </div>

          <div>
            <p class="text-term-muted mb-2 comment">Mobile & Tooling</p>
            <div class="flex flex-wrap gap-2">
              <span class="skill-pill border border-term-border px-3 py-1 text-term-blue">React Native</span>
              <span class="skill-pill border border-term-border px-3 py-1 text-term-blue">Expo</span>
              <span class="skill-pill border border-term-border px-3 py-1 text-term-blue">Web Scraping</span>
              <span class="skill-pill border border-term-border px-3 py-1 text-term-blue">Git / GitHub</span>
              <span class="skill-pill border border-term-border px-3 py-1 text-term-blue">Docker</span>
            </div>
          </div>

          <div class="border-t border-term-dim pt-4 text-term-muted">
            <span class="text-term-green">loaded</span>=true &nbsp; <span class="text-term-yellow">level</span>="hands-on" &nbsp; <span class="text-term-cyan">learning</span>=always
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- ABOUT -->
  <section id="about" class="py-24 px-6">
    <div class="max-w-6xl mx-auto">

      <div class="mb-10 reveal">
        <p class="text-term-muted text-xs prompt mb-1">man mahmedraza1</p>
      </div>

      <div class="grid md:grid-cols-2 gap-6">

        <!-- man page -->
        <div class="term-win reveal">
          <div class="term-bar">
            <div class="dot bg-term-red"></div>
            <div class="dot bg-term-yellow"></div>
            <div class="dot bg-term-green"></div>
            <span class="text-term-muted text-xs ml-3">MAHMEDRAZA1(1) — Manual</span>
          </div>
          <div class="p-6 text-xs leading-loose space-y-4">
            <div>
              <p class="text-term-yellow font-bold">NAME</p>
              <p class="pl-5 text-term-text">mahmedraza1 — Muhammad Ahmed Raza, full-stack developer</p>
            </div>
            <div>
              <p class="text-term-yellow font-bold">SYNOPSIS</p>
              <p class="pl-5 text-term-muted">developer [--stack next|node|python] &lt;project&gt;</p>
            </div>
            <div>
              <p class="text-term-yellow font-bold">DESCRIPTION</p>
              <p class="pl-5 text-term-muted leading-relaxed">Passionate full-stack developer who ships clean code on Linux. Builds web apps, mobile apps, automation tools, and things that don't crash in production. Exit code is always <span class="text-term-green">0</span>.</p>
            </div>
            <div>
              <p class="text-term-yellow font-bold">FLAGS</p>
              <div class="pl-5 space-y-1 text-term-muted">
                <p><span class="text-term-cyan">--collab</span>    &nbsp;open to freelance &amp; projects</p>
                <p><span class="text-term-cyan">--oss</span>       &nbsp;active open-source contributor</p>
                <p><span class="text-term-cyan">--linux</span>     &nbsp;daily driver: Ubuntu</p>
                <p><span class="text-term-cyan">--nocoffee</span>  &nbsp;runs on pure determination</p>
              </div>
            </div>
            <div>
              <p class="text-term-yellow font-bold">ACHIEVEMENTS</p>
              <div class="pl-5 space-y-1 text-term-muted">
                <p><span class="text-term-green">✔</span> Pull Shark ×2 — merges PRs consistently</p>
                <p><span class="text-term-green">✔</span> Quickdraw — fast issue resolution</p>
                <p><span class="text-term-green">✔</span> YOLO — ships with confidence</p>
              </div>
            </div>
            <div>
              <p class="text-term-yellow font-bold">SEE ALSO</p>
              <p class="pl-5">
                <a href="https://github.com/mahmedraza1" target="_blank" class="text-term-cyan hover:text-term-lime transition-colors">github.com/mahmedraza1(7)</a>
              </p>
            </div>
          </div>
        </div>

        <!-- htop -->
        <div class="term-win reveal">
          <div class="term-bar">
            <div class="dot bg-term-red"></div>
            <div class="dot bg-term-yellow"></div>
            <div class="dot bg-term-green"></div>
            <span class="text-term-muted text-xs ml-3">htop — mahmedraza1@ubuntu</span>
          </div>
          <div class="p-5 text-xs">
            <div class="flex justify-between text-term-muted mb-3 border-b border-term-dim pb-2">
              <span class="w-10">PID</span><span class="flex-1">PROCESS</span><span class="w-12 text-right">CPU%</span><span class="w-16 text-right">STATUS</span>
            </div>
            <div class="space-y-2">
              <div class="flex justify-between"><span class="w-10 text-term-muted">001</span><span class="flex-1 text-term-cyan">next.js-app</span><span class="w-12 text-right text-term-green">98%</span><span class="w-16 text-right text-term-green">running</span></div>
              <div class="flex justify-between"><span class="w-10 text-term-muted">002</span><span class="flex-1 text-term-cyan">react-ui</span><span class="w-12 text-right text-term-green">94%</span><span class="w-16 text-right text-term-green">running</span></div>
              <div class="flex justify-between"><span class="w-10 text-term-muted">003</span><span class="flex-1 text-term-yellow">typescript-lsp</span><span class="w-12 text-right text-term-yellow">88%</span><span class="w-16 text-right text-term-green">running</span></div>
              <div class="flex justify-between"><span class="w-10 text-term-muted">004</span><span class="flex-1 text-term-yellow">node-server</span><span class="w-12 text-right text-term-green">82%</span><span class="w-16 text-right text-term-green">running</span></div>
              <div class="flex justify-between"><span class="w-10 text-term-muted">005</span><span class="flex-1 text-term-blue">python-scraper</span><span class="w-12 text-right text-term-cyan">70%</span><span class="w-16 text-right text-term-muted">sleeping</span></div>
              <div class="flex justify-between"><span class="w-10 text-term-muted">006</span><span class="flex-1 text-term-blue">expo-bundler</span><span class="w-12 text-right text-term-cyan">65%</span><span class="w-16 text-right text-term-muted">sleeping</span></div>
              <div class="flex justify-between"><span class="w-10 text-term-muted">007</span><span class="flex-1 text-term-muted">vim</span><span class="w-12 text-right text-term-green">100%</span><span class="w-16 text-right text-term-yellow">zombie</span></div>
            </div>
            <div class="mt-5 pt-3 border-t border-term-dim space-y-1.5 text-term-muted">
              <div class="flex gap-3"><span>Uptime :</span><span class="text-term-green" id="uptime2">00:00:00</span></div>
              <div class="flex gap-3"><span>Load   :</span><span class="text-term-cyan">∞  ∞  ∞</span></div>
              <div class="flex gap-3"><span>MEM    :</span><span class="text-term-yellow">all of it</span></div>
              <div class="flex gap-3"><span>Swap   :</span><span class="text-term-red">also all of it</span></div>
            </div>
          </div>
        </div>

      </div>
    </div>
  </section>

  <!-- CONTACT -->
  <section id="contact" class="py-24 px-6 border-t border-term-border bg-term-surface">
    <div class="max-w-4xl mx-auto">

      <div class="mb-10 reveal">
        <p class="text-term-muted text-xs prompt mb-1">ping mahmedraza1 -c 4 --say "let's work together"</p>
      </div>

      <div class="term-win reveal">
        <div class="term-bar">
          <div class="dot bg-term-red"></div>
          <div class="dot bg-term-yellow"></div>
          <div class="dot bg-term-green"></div>
          <span class="text-term-muted text-xs ml-3">contact.sh — interactive session</span>
        </div>
        <div class="p-8 space-y-6 text-xs">
          <div class="space-y-1 text-term-muted">
            <p>PING mahmedraza1 (0.0.0.0) 56 bytes of passion</p>
            <p><span class="text-term-green">64 bytes</span> from dev: icmp_seq=1 ttl=64 time=<span class="text-term-cyan">0.420ms</span></p>
            <p><span class="text-term-green">64 bytes</span> from dev: icmp_seq=2 ttl=64 time=<span class="text-term-cyan">0.069ms</span></p>
            <p><span class="text-term-green">64 bytes</span> from dev: icmp_seq=3 ttl=64 time=<span class="text-term-cyan">0.137ms</span></p>
            <p class="pt-1">--- mahmedraza1 ping statistics ---</p>
            <p>3 packets transmitted, 3 received, <span class="text-term-green">0% packet loss</span></p>
            <p class="text-term-green pt-1">✔ Developer is online and available for work.</p>
          </div>

          <div class="border-t border-term-dim pt-6 space-y-3">
            <p class="text-term-text font-bold">Available channels:</p>
            <div class="grid md:grid-cols-2 gap-3">
              <a href="https://github.com/mahmedraza1" target="_blank"
                 class="flex items-center gap-3 border border-term-border p-4 hover:border-term-green hover:bg-term-panel transition-all group">
                <span class="text-xl">🐙</span>
                <div>
                  <div class="text-term-cyan group-hover:text-term-lime transition-colors font-bold">GitHub</div>
                  <div class="text-term-muted">github.com/mahmedraza1</div>
                </div>
              </a>
              <a href="mailto:contact@mahmedraza.dev"
                 class="flex items-center gap-3 border border-term-border p-4 hover:border-term-green hover:bg-term-panel transition-all group">
                <span class="text-xl">✉</span>
                <div>
                  <div class="text-term-cyan group-hover:text-term-lime transition-colors font-bold">Email</div>
                  <div class="text-term-muted">contact@mahmedraza.dev</div>
                </div>
              </a>
            </div>
          </div>

          <div class="border-t border-term-dim pt-5 flex items-center gap-2 text-term-muted">
            <span class="text-term-green">root@mahmedraza1:~#</span>
            <span id="typeEl" class="text-term-text"></span>
            <span class="inline-block w-2 h-4 bg-term-green animate-blink"></span>
          </div>
        </div>
      </div>
    </div>
  </section>

  <!-- FOOTER -->
  <footer class="border-t border-term-border px-6 py-5 text-xs text-term-muted flex flex-col md:flex-row justify-between items-center gap-2 bg-term-bg">
    <p>© 2026 Muhammad Ahmed Raza &nbsp;·&nbsp; <span class="text-term-green">exit 0</span></p>
    <p>crafted in <span class="text-term-yellow">vim</span> on <span class="text-term-cyan">Ubuntu</span> · <a href="https://github.com/mahmedraza1" target="_blank" class="text-term-green hover:text-term-lime transition-colors">github.com/mahmedraza1</a></p>
  </footer>

  <script>
    // Scroll reveal
    const revEls = document.querySelectorAll('.reveal');
    new IntersectionObserver((entries) => {
      entries.forEach((e, i) => {
        if (e.isIntersecting) {
          setTimeout(() => e.target.classList.add('in'), i * 90);
        }
      });
    }, { threshold: 0.08 }).observe ? (() => {
      const obs = new IntersectionObserver((entries) => {
        entries.forEach((e, i) => {
          if (e.isIntersecting) {
            setTimeout(() => e.target.classList.add('in'), i * 90);
          }
        });
      }, { threshold: 0.08 });
      revEls.forEach(el => obs.observe(el));
    })() : revEls.forEach(el => el.classList.add('in'));

    // Uptime
    const t0 = Date.now();
    function tick() {
      const s = Math.floor((Date.now() - t0) / 1000);
      const hh = String(Math.floor(s / 3600)).padStart(2,'0');
      const mm = String(Math.floor((s % 3600) / 60)).padStart(2,'0');
      const ss = String(s % 60).padStart(2,'0');
      const v = `${hh}:${mm}:${ss}`;
      document.getElementById('uptime').textContent  = v;
      document.getElementById('uptime2').textContent = v;
    }
    setInterval(tick, 1000); tick();

    // Typewriter at contact prompt
    const cmds = [
      'send_message --hire-me',
      'collaborate --on "next big thing"',
      'ping --say "hey, great work!"',
      'cat opportunities.txt',
    ];
    let ci = 0, char = 0, del = false;
    const tel = document.getElementById('typeEl');
    function tw() {
      const cmd = cmds[ci];
      if (!del) {
        tel.textContent = cmd.slice(0, ++char);
        if (char > cmd.length) { del = true; return setTimeout(tw, 1600); }
      } else {
        tel.textContent = cmd.slice(0, --char);
        if (char < 0) { del = false; ci = (ci + 1) % cmds.length; char = 0; }
      }
      setTimeout(tw, del ? 35 : 65);
    }
    setTimeout(tw, 3200);
  </script>
</body>
</html>
