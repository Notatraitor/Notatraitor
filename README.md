<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8"/>
<meta name="viewport" content="width=device-width, initial-scale=1.0"/>
<title>GitHub Profile Preview</title>
<link href="https://fonts.googleapis.com/css2?family=JetBrains+Mono:wght@400;600;700&family=Sora:wght@300;400;600;700&display=swap" rel="stylesheet"/>
<style>
  :root {
    --bg: #0d1117;
    --surface: #161b22;
    --border: #21262d;
    --cyan: #00fff0;
    --purple: #7b2ff7;
    --text: #e6edf3;
    --muted: #8b949e;
  }

  * { box-sizing: border-box; margin: 0; padding: 0; }

  body {
    background: #010409;
    font-family: 'Sora', sans-serif;
    color: var(--text);
    min-height: 100vh;
    display: flex;
    flex-direction: column;
    align-items: center;
    padding: 24px 16px 0;
  }

  /* Top label */
  .top-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px;
    letter-spacing: 3px;
    text-transform: uppercase;
    color: var(--cyan);
    opacity: 0.6;
    margin-bottom: 16px;
    animation: fadeUp 0.6s ease both;
  }

  /* GitHub chrome */
  .github-frame {
    width: 100%;
    max-width: 860px;
    background: var(--bg);
    border: 1px solid var(--border);
    border-radius: 12px;
    overflow: hidden;
    box-shadow: 0 0 60px rgba(0,255,240,0.07), 0 0 120px rgba(123,47,247,0.05);
    animation: fadeUp 0.7s 0.1s ease both;
  }

  /* Browser chrome */
  .browser-bar {
    background: #1c2128;
    border-bottom: 1px solid var(--border);
    padding: 10px 16px;
    display: flex;
    align-items: center;
    gap: 10px;
  }
  .dot { width: 12px; height: 12px; border-radius: 50%; }
  .dot.r { background: #ff5f57; }
  .dot.y { background: #febc2e; }
  .dot.g { background: #28c840; }
  .url-bar {
    flex: 1;
    background: #0d1117;
    border: 1px solid var(--border);
    border-radius: 6px;
    padding: 4px 12px;
    font-size: 12px;
    font-family: 'JetBrains Mono', monospace;
    color: var(--muted);
    margin-left: 8px;
  }

  /* Profile content */
  .profile-content {
    padding: 0;
  }

  /* Header wave */
  .wave-header {
    width: 100%;
    height: 180px;
    background: linear-gradient(135deg, #0d1117 0%, #0a0f1a 40%, #0d1117 100%);
    position: relative;
    overflow: hidden;
    display: flex;
    flex-direction: column;
    align-items: center;
    justify-content: center;
    gap: 6px;
  }

  .wave-header::before {
    content: '';
    position: absolute;
    inset: 0;
    background:
      radial-gradient(ellipse 80% 60% at 50% 120%, rgba(0,255,240,0.15) 0%, transparent 70%),
      radial-gradient(ellipse 40% 40% at 80% 20%, rgba(123,47,247,0.2) 0%, transparent 60%);
  }

  .wave-top {
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 5px;
    background: linear-gradient(90deg, var(--cyan), var(--purple), var(--cyan));
    background-size: 200% 100%;
    animation: shimmer 3s linear infinite;
  }

  @keyframes shimmer {
    0% { background-position: 200% 0; }
    100% { background-position: -200% 0; }
  }

  .wave-bottom {
    position: absolute;
    bottom: 0; left: 0; right: 0;
    height: 5px;
    background: linear-gradient(90deg, var(--purple), var(--cyan), var(--purple));
    background-size: 200% 100%;
    animation: shimmer 3s linear infinite reverse;
  }

  .header-name {
    font-family: 'Sora', sans-serif;
    font-size: 42px;
    font-weight: 700;
    color: #fff;
    letter-spacing: -1px;
    position: relative;
    z-index: 1;
    text-shadow: 0 0 40px rgba(0,255,240,0.4);
    animation: fadeUp 0.8s 0.3s ease both;
  }

  .header-sub {
    font-family: 'JetBrains Mono', monospace;
    font-size: 13px;
    color: var(--cyan);
    opacity: 0.85;
    position: relative;
    z-index: 1;
    animation: fadeUp 0.8s 0.45s ease both;
    letter-spacing: 1px;
  }

  /* Typing line */
  .typing-section {
    padding: 20px;
    display: flex;
    justify-content: center;
    border-bottom: 1px solid var(--border);
  }

  .typing-bar {
    background: #0a0f1a;
    border: 1px solid rgba(0,255,240,0.2);
    border-radius: 8px;
    padding: 10px 20px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 14px;
    font-weight: 600;
    color: var(--cyan);
    display: flex;
    align-items: center;
    gap: 8px;
    box-shadow: 0 0 20px rgba(0,255,240,0.05);
  }

  .cursor {
    width: 2px;
    height: 16px;
    background: var(--cyan);
    animation: blink 1s step-end infinite;
  }

  @keyframes blink { 50% { opacity: 0; } }

  /* Sections */
  .section {
    padding: 24px 28px;
    border-bottom: 1px solid var(--border);
    animation: fadeUp 0.8s ease both;
  }

  .section-title {
    font-family: 'JetBrains Mono', monospace;
    font-size: 13px;
    font-weight: 600;
    color: var(--cyan);
    letter-spacing: 2px;
    text-transform: uppercase;
    margin-bottom: 16px;
    display: flex;
    align-items: center;
    gap: 8px;
  }

  .section-title::after {
    content: '';
    flex: 1;
    height: 1px;
    background: linear-gradient(90deg, rgba(0,255,240,0.3), transparent);
  }

  /* Code block */
  .code-block {
    background: #0a0f1a;
    border: 1px solid rgba(0,255,240,0.15);
    border-radius: 8px;
    padding: 18px 20px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 13px;
    line-height: 1.8;
  }

  .kw { color: #ff79c6; }
  .cls { color: #50fa7b; }
  .key { color: #8be9fd; }
  .val { color: #f1fa8c; }
  .str { color: #a8d8a8; }
  .comment { color: var(--muted); }

  /* Badges */
  .badge-group {
    display: flex;
    flex-wrap: wrap;
    gap: 8px;
    margin-bottom: 12px;
  }

  .badge-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 1px;
    text-transform: uppercase;
    margin-bottom: 8px;
    margin-top: 4px;
  }

  .badge {
    display: flex;
    align-items: center;
    gap: 6px;
    background: #0a0f1a;
    border: 1px solid rgba(0,255,240,0.2);
    border-radius: 6px;
    padding: 6px 12px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    font-weight: 600;
    color: var(--cyan);
    transition: all 0.2s;
    cursor: default;
  }

  .badge:hover {
    border-color: var(--cyan);
    box-shadow: 0 0 12px rgba(0,255,240,0.2);
    transform: translateY(-1px);
  }

  .badge-icon {
    width: 16px;
    height: 16px;
    opacity: 0.9;
  }

  /* Stats grid */
  .stats-grid {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 12px;
  }

  .stat-card {
    background: #0a0f1a;
    border: 1px solid rgba(0,255,240,0.15);
    border-radius: 8px;
    padding: 16px 18px;
    position: relative;
    overflow: hidden;
    transition: border-color 0.2s;
  }

  .stat-card:hover { border-color: rgba(0,255,240,0.4); }

  .stat-card::before {
    content: '';
    position: absolute;
    top: 0; left: 0; right: 0;
    height: 2px;
    background: linear-gradient(90deg, var(--cyan), var(--purple));
    opacity: 0.6;
  }

  .stat-label {
    font-family: 'JetBrains Mono', monospace;
    font-size: 10px;
    color: var(--muted);
    letter-spacing: 2px;
    text-transform: uppercase;
    margin-bottom: 6px;
  }

  .stat-value {
    font-family: 'Sora', sans-serif;
    font-size: 28px;
    font-weight: 700;
    color: var(--cyan);
    line-height: 1;
    text-shadow: 0 0 20px rgba(0,255,240,0.4);
  }

  .stat-sub {
    font-size: 11px;
    color: var(--muted);
    margin-top: 4px;
  }

  /* Streak */
  .streak-bar-wrap {
    margin-top: 12px;
    background: #0a0f1a;
    border: 1px solid rgba(0,255,240,0.15);
    border-radius: 8px;
    padding: 16px 18px;
  }

  .streak-row {
    display: flex;
    justify-content: space-between;
    align-items: center;
    margin-bottom: 10px;
  }

  .streak-title {
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px;
    color: var(--cyan);
    letter-spacing: 1px;
  }

  .streak-num {
    font-family: 'Sora', sans-serif;
    font-size: 22px;
    font-weight: 700;
    color: var(--purple);
    text-shadow: 0 0 15px rgba(123,47,247,0.5);
  }

  .progress-bg {
    height: 6px;
    background: #1c2128;
    border-radius: 3px;
    overflow: hidden;
  }

  .progress-fill {
    height: 100%;
    width: 0%;
    background: linear-gradient(90deg, var(--cyan), var(--purple));
    border-radius: 3px;
    animation: fillBar 1.5s 0.8s ease forwards;
  }

  @keyframes fillBar { to { width: 68%; } }

  /* Social links */
  .social-grid {
    display: flex;
    flex-wrap: wrap;
    gap: 10px;
    justify-content: center;
  }

  .social-btn {
    display: flex;
    align-items: center;
    gap: 8px;
    background: #0a0f1a;
    border: 1px solid rgba(0,255,240,0.2);
    border-radius: 8px;
    padding: 10px 18px;
    font-family: 'JetBrains Mono', monospace;
    font-size: 13px;
    font-weight: 600;
    color: var(--cyan);
    text-decoration: none;
    transition: all 0.2s;
    cursor: default;
  }

  .social-btn:hover {
    border-color: var(--cyan);
    box-shadow: 0 0 16px rgba(0,255,240,0.15);
    transform: translateY(-2px);
  }

  /* Footer wave */
  .wave-footer {
    width: 100%;
    height: 70px;
    background: linear-gradient(180deg, #0d1117 0%, #0a0814 100%);
    position: relative;
    overflow: hidden;
  }

  .wave-footer::before {
    content: '';
    position: absolute;
    bottom: 0; left: 0; right: 0;
    height: 4px;
    background: linear-gradient(90deg, var(--purple), var(--cyan), var(--purple));
    background-size: 200% 100%;
    animation: shimmer 3s linear infinite;
  }

  .views-badge {
    display: flex;
    justify-content: center;
    align-items: center;
    height: 100%;
    font-family: 'JetBrains Mono', monospace;
    font-size: 11px;
    color: var(--muted);
    letter-spacing: 2px;
  }

  .views-count {
    color: var(--cyan);
    font-weight: 600;
    margin-left: 6px;
  }

  /* Bottom instructions */
  .instructions {
    width: 100%;
    max-width: 860px;
    margin: 24px 0;
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 10px;
    padding: 20px 24px;
    animation: fadeUp 0.8s 0.6s ease both;
  }

  .inst-title {
    font-family: 'JetBrains Mono', monospace;
    font-size: 12px;
    color: var(--cyan);
    letter-spacing: 2px;
    text-transform: uppercase;
    margin-bottom: 12px;
  }

  .steps {
    list-style: none;
    display: flex;
    flex-direction: column;
    gap: 8px;
  }

  .steps li {
    display: flex;
    align-items: flex-start;
    gap: 10px;
    font-size: 13px;
    color: var(--muted);
    line-height: 1.5;
  }

  .step-num {
    min-width: 22px;
    height: 22px;
    border-radius: 50%;
    background: rgba(0,255,240,0.1);
    border: 1px solid rgba(0,255,240,0.3);
    display: flex;
    align-items: center;
    justify-content: center;
    font-family: 'JetBrains Mono', monospace;
    font-size: 10px;
    font-weight: 700;
    color: var(--cyan);
    flex-shrink: 0;
    margin-top: 1px;
  }

  .highlight { color: var(--text); font-weight: 600; }
  .cyan { color: var(--cyan); }

  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(16px); }
    to { opacity: 1; transform: translateY(0); }
  }
</style>
</head>
<body>

<div class="top-label">⚡ GitHub Profile Preview</div>

<div class="github-frame">
  <div class="browser-bar">
    <div class="dot r"></div>
    <div class="dot y"></div>
    <div class="dot g"></div>
    <div class="url-bar">github.com / NotaTraitor</div>
  </div>

  <div class="profile-content">

    <!-- Header -->
    <div class="wave-header">
      <div class="wave-top"></div>
      <div class="header-name">Magnus</div>
      <div class="header-sub">Full-Stack Developer &nbsp;|&nbsp; Python · TypeScript</div>
      <div class="wave-bottom"></div>
    </div>

    <!-- Typing line -->
    <div class="typing-section">
      <div class="typing-bar">
        Building things that matter.<div class="cursor"></div>
      </div>
    </div>

    <!-- About Me -->
    <div class="section">
      <div class="section-title">⚡ About Me</div>
      <div class="code-block">
        <div><span class="kw">class</span> <span class="cls">Developer</span>:</div>
        <div>&nbsp;&nbsp;&nbsp;&nbsp;<span class="key">name</span>       <span class="comment">=</span> <span class="str">"Magnus"</span></div>
        <div>&nbsp;&nbsp;&nbsp;&nbsp;<span class="key">role</span>       <span class="comment">=</span> <span class="str">"Full-Stack Developer"</span></div>
        <div>&nbsp;&nbsp;&nbsp;&nbsp;<span class="key">languages</span>  <span class="comment">=</span> <span class="val">["Python", "TypeScript", "JavaScript"]</span></div>
        <div>&nbsp;&nbsp;&nbsp;&nbsp;<span class="key">interests</span>  <span class="comment">=</span> <span class="val">["Open Source", "Dev Tools", "Clean Code"]</span></div>
        <div>&nbsp;&nbsp;&nbsp;&nbsp;<span class="key">currently</span>  <span class="comment">=</span> <span class="str">"Building something cool 🚀"</span></div>
      </div>
    </div>

    <!-- Tech Stack -->
    <div class="section">
      <div class="section-title">🛠 Tech Stack</div>

      <div class="badge-label">Languages</div>
      <div class="badge-group">
        <div class="badge">🐍 Python</div>
        <div class="badge">TS TypeScript</div>
        <div class="badge">JS JavaScript</div>
      </div>

      <div class="badge-label">Frontend</div>
      <div class="badge-group">
        <div class="badge">⚛ React</div>
        <div class="badge">▲ Next.js</div>
        <div class="badge">🌊 Tailwind</div>
        <div class="badge">📄 HTML5</div>
      </div>

      <div class="badge-label">Backend & Tools</div>
      <div class="badge-group">
        <div class="badge">🟢 Node.js</div>
        <div class="badge">⚡ FastAPI</div>
        <div class="badge">🐘 PostgreSQL</div>
        <div class="badge">🐳 Docker</div>
        <div class="badge">🔧 Git</div>
        <div class="badge">🐧 Linux</div>
      </div>
    </div>

    <!-- GitHub Stats -->
    <div class="section">
      <div class="section-title">📊 GitHub Stats</div>
      <div class="stats-grid">
        <div class="stat-card">
          <div class="stat-label">Total Commits</div>
          <div class="stat-value">1.2k+</div>
          <div class="stat-sub">across all repositories</div>
        </div>
        <div class="stat-card">
          <div class="stat-label">Top Language</div>
          <div class="stat-value">PY</div>
          <div class="stat-sub">Python · 45%</div>
        </div>
      </div>
      <div class="streak-bar-wrap">
        <div class="streak-row">
          <span class="streak-title">🔥 CURRENT STREAK</span>
          <span class="streak-num">12 days</span>
        </div>
        <div class="progress-bg">
          <div class="progress-fill"></div>
        </div>
      </div>
    </div>

    <!-- Connect -->
    <div class="section" style="border-bottom: none;">
      <div class="section-title">🌐 Connect With Me</div>
      <div class="social-grid">
        <div class="social-btn">💼 LinkedIn</div>
        <div class="social-btn">𝕏 Twitter</div>
        <div class="social-btn">🌍 Portfolio</div>
        <div class="social-btn">✉️ Email</div>
      </div>
    </div>

    <!-- Footer -->
    <div class="wave-footer">
      <div class="views-badge">PROFILE VIEWS <span class="views-count">—</span></div>
    </div>

  </div>
</div>

<!-- Instructions -->
<div class="instructions">
  <div class="inst-title">🚀 How to activate your profile</div>
  <ul class="steps">
    <li><span class="step-num">1</span><span>Create a new GitHub repo named exactly <span class="highlight">NotaTraitor</span> (same as your username). Make it public and check <span class="cyan">"Add a README file"</span>.</span></li>
    <li><span class="step-num">2</span><span>Download the <span class="highlight">README.md</span> file above and paste its contents into the repo's README editor.</span></li>
    <li><span class="step-num">3</span><span>Replace every <span class="cyan">NotaTraitor</span>, <span class="cyan">Magnus</span>, <span class="cyan">Magnussteenholmjensen@gmail.com</span>, etc. with your real info.</span></li>
    <li><span class="step-num">4</span><span>Commit the file — GitHub will instantly show your profile README on your main page. <span class="highlight">Done!</span> ⚡</span></li>
  </ul>
</div>

</body>
</html>
