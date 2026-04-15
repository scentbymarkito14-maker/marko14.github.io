# marko14.github.io
PGW Quiz
<!DOCTYPE html>
<html lang="de">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<title>PGW Quiz – Soziale Ungleichheit</title>
<link rel="preconnect" href="https://fonts.googleapis.com">
<link href="https://fonts.googleapis.com/css2?family=DM+Serif+Display:ital@0;1&family=DM+Sans:wght@300;400;500;600&display=swap" rel="stylesheet">
<style>
  :root {
    --bg: #0f0e17;
    --surface: #1a1928;
    --surface2: #231f3a;
    --accent: #a78bfa;
    --accent2: #f472b6;
    --accent3: #34d399;
    --text: #e8e6f0;
    --muted: #8b87a8;
    --border: rgba(167,139,250,0.15);
    --correct: #34d399;
    --wrong: #f87171;
    --reveal: #a78bfa;
  }
  *, *::before, *::after { box-sizing: border-box; margin: 0; padding: 0; }
  html { font-size: 16px; }
  body {
    font-family: 'DM Sans', sans-serif;
    background: var(--bg);
    color: var(--text);
    min-height: 100vh;
    overflow-x: hidden;
  }

  /* Animated background */
  body::before {
    content: '';
    position: fixed;
    top: -50%;
    left: -50%;
    width: 200%;
    height: 200%;
    background:
      radial-gradient(ellipse at 20% 20%, rgba(167,139,250,0.07) 0%, transparent 50%),
      radial-gradient(ellipse at 80% 80%, rgba(244,114,182,0.05) 0%, transparent 50%),
      radial-gradient(ellipse at 50% 50%, rgba(52,211,153,0.03) 0%, transparent 60%);
    animation: bgshift 20s ease-in-out infinite alternate;
    pointer-events: none;
    z-index: 0;
  }
  @keyframes bgshift {
    0% { transform: translate(0,0) rotate(0deg); }
    100% { transform: translate(2%, 2%) rotate(1deg); }
  }

  /* Grid pattern overlay */
  body::after {
    content: '';
    position: fixed;
    inset: 0;
    background-image:
      linear-gradient(rgba(167,139,250,0.03) 1px, transparent 1px),
      linear-gradient(90deg, rgba(167,139,250,0.03) 1px, transparent 1px);
    background-size: 40px 40px;
    pointer-events: none;
    z-index: 0;
  }

  .wrapper {
    position: relative;
    z-index: 1;
    max-width: 720px;
    margin: 0 auto;
    padding: 0 20px;
  }

  /* ── HEADER ── */
  header {
    padding: 2rem 0 1.5rem;
    display: flex;
    align-items: center;
    justify-content: space-between;
  }
  .logo {
    font-family: 'DM Serif Display', serif;
    font-size: 1.3rem;
    color: var(--accent);
    letter-spacing: -0.01em;
  }
  .logo span { color: var(--text); }
  .header-badge {
    font-size: 11px;
    font-weight: 500;
    letter-spacing: 0.08em;
    text-transform: uppercase;
    color: var(--muted);
    border: 1px solid var(--border);
    padding: 5px 12px;
    border-radius: 20px;
  }

  /* ── SCREENS ── */
  .screen { display: none; }
  .screen.active { display: block; }

  /* ── START SCREEN ── */
  .hero {
    padding: 3rem 0 2.5rem;
    text-align: center;
  }
  .hero-eyebrow {
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 0.15em;
    text-transform: uppercase;
    color: var(--accent);
    margin-bottom: 1rem;
  }
  .hero h1 {
    font-family: 'DM Serif Display', serif;
    font-size: clamp(2.2rem, 6vw, 3.5rem);
    line-height: 1.1;
    color: var(--text);
    margin-bottom: 0.75rem;
  }
  .hero h1 em {
    font-style: italic;
    color: var(--accent);
  }
  .hero-sub {
    font-size: 15px;
    color: var(--muted);
    line-height: 1.6;
    max-width: 480px;
    margin: 0 auto 2.5rem;
  }

  .stats-row {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 12px;
    margin-bottom: 2.5rem;
  }
  .stat-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 16px;
    padding: 1.25rem 1rem;
    text-align: center;
  }
  .stat-card .num {
    font-family: 'DM Serif Display', serif;
    font-size: 2rem;
    color: var(--accent);
    display: block;
    line-height: 1;
    margin-bottom: 6px;
  }
  .stat-card .lbl {
    font-size: 12px;
    color: var(--muted);
    font-weight: 500;
  }

  .section-title {
    font-size: 12px;
    font-weight: 600;
    letter-spacing: 0.1em;
    text-transform: uppercase;
    color: var(--muted);
    margin-bottom: 12px;
  }

  /* Category filter */
  .cat-grid {
    display: grid;
    grid-template-columns: repeat(2, 1fr);
    gap: 10px;
    margin-bottom: 2rem;
  }
  .cat-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 14px;
    padding: 14px 16px;
    cursor: pointer;
    transition: all 0.2s;
    text-align: left;
    display: flex;
    align-items: center;
    gap: 12px;
  }
  .cat-card:hover { border-color: rgba(167,139,250,0.4); background: var(--surface2); }
  .cat-card.active {
    border-color: var(--accent);
    background: rgba(167,139,250,0.08);
  }
  .cat-card.active .cat-name { color: var(--accent); }
  .cat-dot { width: 10px; height: 10px; border-radius: 50%; flex-shrink: 0; }
  .cat-name { font-size: 13px; font-weight: 500; color: var(--text); }
  .cat-count { font-size: 11px; color: var(--muted); margin-top: 2px; }

  .cat-card-all {
    grid-column: 1 / -1;
  }

  /* Difficulty filter */
  .diff-row {
    display: flex;
    gap: 8px;
    margin-bottom: 2rem;
    flex-wrap: wrap;
  }
  .diff-btn {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 20px;
    padding: 7px 16px;
    font-size: 13px;
    font-family: 'DM Sans', sans-serif;
    color: var(--muted);
    cursor: pointer;
    transition: all 0.2s;
  }
  .diff-btn:hover { color: var(--text); border-color: rgba(167,139,250,0.3); }
  .diff-btn.active { color: var(--bg); font-weight: 600; }
  .diff-btn[data-diff="all"].active { background: var(--accent); border-color: var(--accent); }
  .diff-btn[data-diff="leicht"].active { background: var(--correct); border-color: var(--correct); }
  .diff-btn[data-diff="mittel"].active { background: #fbbf24; border-color: #fbbf24; }
  .diff-btn[data-diff="schwer"].active { background: var(--wrong); border-color: var(--wrong); }

  .start-btn {
    width: 100%;
    background: var(--accent);
    color: var(--bg);
    border: none;
    border-radius: 14px;
    padding: 16px;
    font-size: 16px;
    font-family: 'DM Sans', sans-serif;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.2s;
    letter-spacing: 0.01em;
    margin-bottom: 2.5rem;
  }
  .start-btn:hover { opacity: 0.9; transform: translateY(-1px); }
  .start-btn:active { transform: translateY(0); }

  /* ── QUIZ SCREEN ── */
  .quiz-top {
    display: flex;
    justify-content: space-between;
    align-items: center;
    padding: 1.5rem 0 1rem;
  }
  .q-counter { font-size: 13px; color: var(--muted); }
  .score-pill {
    font-size: 13px;
    font-weight: 600;
    color: var(--accent);
    background: rgba(167,139,250,0.1);
    border: 1px solid rgba(167,139,250,0.2);
    padding: 5px 14px;
    border-radius: 20px;
  }

  .progress-track {
    height: 3px;
    background: rgba(255,255,255,0.06);
    border-radius: 2px;
    overflow: hidden;
    margin-bottom: 1.75rem;
  }
  .progress-fill {
    height: 100%;
    background: linear-gradient(90deg, var(--accent), var(--accent2));
    border-radius: 2px;
    transition: width 0.4s cubic-bezier(0.4,0,0.2,1);
  }

  .q-card {
    background: var(--surface);
    border: 1px solid var(--border);
    border-radius: 20px;
    padding: 1.75rem;
    margin-bottom: 1.25rem;
    animation: cardIn 0.3s ease;
  }
  @keyframes cardIn {
    from { opacity: 0; transform: translateY(8px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .q-meta {
    display: flex;
    align-items: center;
    gap: 8px;
    margin-bottom: 1rem;
  }
  .cat-pill {
    font-size: 11px;
    font-weight: 600;
    letter-spacing: 0.06em;
    text-transform: uppercase;
    padding: 4px 12px;
    border-radius: 20px;
  }
  .diff-pill {
    font-size: 11px;
    font-weight: 600;
    padding: 4px 10px;
    border-radius: 20px;
    letter-spacing: 0.04em;
  }
  .diff-leicht { background: rgba(52,211,153,0.12); color: var(--correct); }
  .diff-mittel { background: rgba(251,191,36,0.12); color: #fbbf24; }
  .diff-schwer { background: rgba(248,113,113,0.12); color: var(--wrong); }

  .q-text {
    font-size: 17px;
    line-height: 1.55;
    color: var(--text);
    font-weight: 400;
  }

  .answers { display: flex; flex-direction: column; gap: 10px; margin-bottom: 1rem; }
  .ans-btn {
    background: var(--surface);
    border: 1px solid rgba(255,255,255,0.08);
    border-radius: 14px;
    padding: 14px 18px;
    font-size: 14px;
    font-family: 'DM Sans', sans-serif;
    color: var(--text);
    cursor: pointer;
    text-align: left;
    transition: all 0.18s;
    line-height: 1.45;
  }
  .ans-btn:hover:not(.disabled) {
    border-color: rgba(167,139,250,0.4);
    background: var(--surface2);
    transform: translateX(3px);
  }
  .ans-btn.correct {
    background: rgba(52,211,153,0.1);
    border-color: var(--correct);
    color: var(--correct);
  }
  .ans-btn.wrong {
    background: rgba(248,113,113,0.1);
    border-color: var(--wrong);
    color: var(--wrong);
  }
  .ans-btn.reveal {
    background: rgba(167,139,250,0.1);
    border-color: var(--accent);
    color: var(--accent);
  }
  .ans-btn.disabled { pointer-events: none; opacity: 0.45; }
  .ans-btn.correct.disabled, .ans-btn.wrong.disabled, .ans-btn.reveal.disabled { opacity: 1; }

  .explanation {
    background: var(--surface2);
    border: 1px solid rgba(167,139,250,0.12);
    border-left: 3px solid var(--accent);
    border-radius: 0 12px 12px 0;
    padding: 14px 16px;
    font-size: 13px;
    color: var(--muted);
    line-height: 1.65;
    animation: fadeUp 0.25s ease;
  }
  @keyframes fadeUp {
    from { opacity: 0; transform: translateY(4px); }
    to { opacity: 1; transform: translateY(0); }
  }

  .next-btn {
    width: 100%;
    background: transparent;
    border: 1px solid rgba(167,139,250,0.3);
    border-radius: 14px;
    padding: 14px;
    font-size: 14px;
    font-family: 'DM Sans', sans-serif;
    font-weight: 500;
    color: var(--accent);
    cursor: pointer;
    transition: all 0.2s;
    margin-top: 12px;
    display: none;
  }
  .next-btn:hover { background: rgba(167,139,250,0.08); border-color: var(--accent); }

  /* ── RESULT SCREEN ── */
  .result-hero {
    text-align: center;
    padding: 3rem 0 2rem;
  }
  .result-grade {
    font-family: 'DM Serif Display', serif;
    font-size: 5rem;
    line-height: 1;
    margin-bottom: 0.5rem;
  }
  .result-msg {
    font-size: 15px;
    color: var(--muted);
    margin-bottom: 2rem;
  }

  .result-stats {
    display: grid;
    grid-template-columns: repeat(3, 1fr);
    gap: 12px;
    margin-bottom: 2rem;
  }

  .cat-results { margin-bottom: 2rem; }
  .cat-result-row {
    display: flex;
    align-items: center;
    gap: 12px;
    margin-bottom: 10px;
  }
  .cat-result-name {
    font-size: 12px;
    color: var(--muted);
    width: 150px;
    flex-shrink: 0;
  }
  .cat-bar-track {
    flex: 1;
    height: 6px;
    background: rgba(255,255,255,0.06);
    border-radius: 3px;
    overflow: hidden;
  }
  .cat-bar-fill {
    height: 100%;
    border-radius: 3px;
    transition: width 0.8s cubic-bezier(0.4,0,0.2,1);
  }
  .cat-result-pct {
    font-size: 12px;
    font-weight: 600;
    color: var(--text);
    width: 34px;
    text-align: right;
  }

  .result-btns {
    display: grid;
    grid-template-columns: 1fr 1fr;
    gap: 10px;
    padding-bottom: 3rem;
  }
  .result-btn {
    padding: 14px;
    border-radius: 14px;
    font-size: 14px;
    font-family: 'DM Sans', sans-serif;
    font-weight: 500;
    cursor: pointer;
    transition: all 0.2s;
    border: 1px solid var(--border);
    background: transparent;
    color: var(--text);
  }
  .result-btn.primary {
    background: var(--accent);
    color: var(--bg);
    border-color: var(--accent);
    font-weight: 600;
  }
  .result-btn:hover { opacity: 0.85; }

  /* ── FOOTER ── */
  footer {
    text-align: center;
    padding: 1.5rem 0 2rem;
    font-size: 12px;
    color: rgba(139,135,168,0.5);
    border-top: 1px solid var(--border);
  }

  @media (max-width: 480px) {
    .cat-grid { grid-template-columns: 1fr; }
    .cat-card-all { grid-column: 1; }
    .result-btns { grid-template-columns: 1fr; }
    .hero h1 { font-size: 2rem; }
    .stats-row { grid-template-columns: repeat(3,1fr); }
  }
</style>
</head>
<body>
<div class="wrapper">

  <header>
    <div class="logo">PGW<span>Quiz</span></div>
    <div class="header-badge">Abitur 2026</div>
  </header>

  <!-- ══ START SCREEN ══ -->
  <div id="start-screen" class="screen active">
    <div class="hero">
      <div class="hero-eyebrow">Politik · Gesellschaft · Wirtschaft</div>
      <h1>Soziale<br><em>Ungleichheit</em></h1>
      <p class="hero-sub">50 Fragen, 5 Kategorien, 3 Schwierigkeitsstufen – speziell für das Berliner Abitur 2026 auf erhöhtem Niveau.</p>
    </div>

    <div class="stats-row">
      <div class="stat-card"><span class="num" id="total-count">50</span><div class="lbl">Fragen</div></div>
      <div class="stat-card"><span class="num">5</span><div class="lbl">Kategorien</div></div>
      <div class="stat-card"><span class="num">3</span><div class="lbl">Levels</div></div>
    </div>

    <div class="section-title">Thema wählen</div>
    <div class="cat-grid" id="cat-grid">
      <div class="cat-card cat-card-all active" data-cat="all">
        <div class="cat-dot" style="background:var(--accent)"></div>
        <div>
          <div class="cat-name">Alle Themen</div>
          <div class="cat-count" id="count-all">50 Fragen</div>
        </div>
      </div>
      <div class="cat-card" data-cat="modelle">
        <div class="cat-dot" style="background:#a78bfa"></div>
        <div>
          <div class="cat-name">Sozialstrukturmodelle</div>
          <div class="cat-count" id="count-modelle"></div>
        </div>
      </div>
      <div class="cat-card" data-cat="begriffe">
        <div class="cat-dot" style="background:#34d399"></div>
        <div>
          <div class="cat-name">Fachbegriffe</div>
          <div class="cat-count" id="count-begriffe"></div>
        </div>
      </div>
      <div class="cat-card" data-cat="gerechtigkeit">
        <div class="cat-dot" style="background:#fbbf24"></div>
        <div>
          <div class="cat-name">Gerechtigkeitstheorien</div>
          <div class="cat-count" id="count-gerechtigkeit"></div>
        </div>
      </div>
      <div class="cat-card" data-cat="sozialstaat">
        <div class="cat-dot" style="background:#f472b6"></div>
        <div>
          <div class="cat-name">Sozialstaat</div>
          <div class="cat-count" id="count-sozialstaat"></div>
        </div>
      </div>
      <div class="cat-card" data-cat="analyse">
        <div class="cat-dot" style="background:#60a5fa"></div>
        <div>
          <div class="cat-name">Analyse &amp; Prüfung</div>
          <div class="cat-count" id="count-analyse"></div>
        </div>
      </div>
    </div>

    <div class="section-title">Schwierigkeitsgrad</div>
    <div class="diff-row">
      <button class="diff-btn active" data-diff="all">Alle</button>
      <button class="diff-btn" data-diff="leicht">Leicht</button>
      <button class="diff-btn" data-diff="mittel">Mittel</button>
      <button class="diff-btn" data-diff="schwer">Schwer</button>
    </div>

    <button class="start-btn" onclick="startGame()">Quiz starten →</button>
  </div>

  <!-- ══ QUIZ SCREEN ══ -->
  <div id="quiz-screen" class="screen">
    <div class="quiz-top">
      <span class="q-counter" id="q-counter">Frage 1 / 50</span>
      <span class="score-pill" id="score-pill">0 richtig</span>
    </div>
    <div class="progress-track"><div class="progress-fill" id="progress-fill" style="width:0%"></div></div>

    <div class="q-card" id="q-card">
      <div class="q-meta">
        <span class="cat-pill" id="cat-pill"></span>
        <span class="diff-pill" id="diff-pill"></span>
      </div>
      <p class="q-text" id="q-text"></p>
    </div>

    <div class="answers" id="answers"></div>
    <div id="explanation"></div>
    <button class="next-btn" id="next-btn" onclick="nextQuestion()">Nächste Frage →</button>
  </div>

  <!-- ══ RESULT SCREEN ══ -->
  <div id="result-screen" class="screen">
    <div class="result-hero">
      <div class="result-grade" id="result-grade"></div>
      <div class="result-msg" id="result-msg"></div>
    </div>

    <div class="result-stats">
      <div class="stat-card"><span class="num" id="res-correct" style="color:var(--correct)">0</span><div class="lbl">Richtig</div></div>
      <div class="stat-card"><span class="num" id="res-wrong" style="color:var(--wrong)">0</span><div class="lbl">Falsch</div></div>
      <div class="stat-card"><span class="num" id="res-pct">0%</span><div class="lbl">Score</div></div>
    </div>

    <div class="section-title">Nach Kategorie</div>
    <div class="cat-results" id="cat-results"></div>

    <div class="result-btns">
      <button class="result-btn primary" onclick="startGame()">Nochmal spielen</button>
      <button class="result-btn" onclick="showStart()">Kategorie wählen</button>
    </div>
  </div>

  <footer>PGW Quiz · Soziale Ungleichheit · Berlin Abitur 2026</footer>
</div>

<script>
const QUESTIONS = [
  // ── SOZIALSTRUKTURMODELLE (12 Fragen) ──
  {cat:"modelle",diff:"leicht",q:"Wer entwickelte die Klassentheorie, die Gesellschaft in Bourgeoisie und Proletariat unterteilt?",a:["Karl Marx","Max Weber","Émile Durkheim","Niklas Luhmann"],c:0,e:"Marx unterschied zwischen Besitzern der Produktionsmittel (Bourgeoisie) und der Arbeiterklasse (Proletariat). Ungleichheit entsteht laut Marx durch Ausbeutung der Lohnarbeit."},
  {cat:"modelle",diff:"leicht",q:"Was beschreibt das Sinus-Milieu-Modell?",a:["Nur Einkommensunterschiede","Kombination aus sozialer Lage und Wertorientierung","Rein berufliche Statusgruppen","Staatliche Versicherungssysteme"],c:1,e:"Sinus-Milieus kombinieren objektive Merkmale (Einkommen, Bildung) mit subjektiven Werten und Lebensstilen. Es gibt etwa 10 Milieus in Deutschland, die sich regelmäßig verschieben."},
  {cat:"modelle",diff:"leicht",q:"Was ist ein Schichtmodell?",a:["Ein Modell nur für Arbeitende","Hierarchische Einteilung der Gesellschaft nach Einkommen, Prestige und Bildung","Ein Modell, das nur Reichtum misst","Eine politische Parteistruktur"],c:1,e:"Schichtmodelle ordnen Menschen in vertikale Lagen (Ober-, Mittel-, Unterschicht) nach mehreren Kriterien. Dahrendorf und Geißler entwickelten bekannte deutsche Schichtmodelle."},
  {cat:"modelle",diff:"mittel",q:"Was ist der zentrale Gedanke von Ulrich Becks 'Risikogesellschaft'?",a:["Klassen werden immer wichtiger","Klassenstrukturen lösen sich durch Individualisierung auf","Schichten sind stabiler als je zuvor","Das Milieu bestimmt alles"],c:1,e:"Beck argumentiert, dass traditionelle Klassen und Schichten an Bedeutung verlieren. Individuen müssen ihre Biografie selbst gestalten – Chancen und Risiken sind individualisiert."},
  {cat:"modelle",diff:"mittel",q:"Was meint Bourdieu mit 'sozialem Kapital'?",a:["Geld auf dem Bankkonto","Schulabschlüsse und Zertifikate","Soziale Netzwerke und Beziehungen","Kulturelles Wissen und Geschmack"],c:2,e:"Soziales Kapital = Ressourcen aus Netzwerken und Beziehungen. Wer die richtigen Kontakte hat, hat Vorteile. Neben ökonomischem und kulturellem Kapital die dritte Kapitalform bei Bourdieu."},
  {cat:"modelle",diff:"mittel",q:"Was beschreibt Bourdieus Begriff 'Habitus'?",a:["Das staatliche Fördersystem","Unbewusste Denk- und Handlungsmuster, die durch Herkunft geprägt sind","Die rechtliche Stellung einer Person","Das Bildungsniveau einer Person"],c:1,e:"Der Habitus ist das 'Körper gewordene Soziale': durch Sozialisation verinnerlichte Dispositionen, die Geschmack, Urteile und Handlungen unbewusst steuern – und soziale Ungleichheit reproduzieren."},
  {cat:"modelle",diff:"mittel",q:"Was unterscheidet Marx' Klassenmodell von Webers Schichtungstheorie?",a:["Weber betont nur Einkommen; Marx betont alles","Marx betont Produktionsmittelbesitz; Weber ergänzt Status und Macht als eigenständige Dimensionen","Beide sind identisch","Weber lehnte Klassen komplett ab"],c:1,e:"Weber erweitert Marx: Er sieht drei unabhängige Dimensionen – Klasse (ökonomisch), Stand (Prestige/Status) und Partei (politische Macht). Ungleichheit ist mehrdimensional."},
  {cat:"modelle",diff:"schwer",q:"Was ist Bourdieus 'kulturelles Kapital' in der inkorporierten Form?",a:["Bücher und Kunstwerke zu Hause","Bildungsabschlüsse und Zertifikate","Verinnerlichte Fähigkeiten, Wissen und Geschmack","Geld und Immobilien"],c:2,e:"Inkorporiertes kulturelles Kapital = im Körper eingeschriebene Fähigkeiten, Sprachstile, ästhetische Urteile. Es entsteht durch Sozialisation und ist nicht übertragbar – nur durch Lernzeit erwerbbar."},
  {cat:"modelle",diff:"schwer",q:"Was kritisiert man an Schichtmodellen im Vergleich zu Milieumodellen?",a:["Sie sind zu komplex","Sie ignorieren subjektive Lebensstile und Wertvorstellungen, die Klassenlagen überlagern","Sie sind politisch gefärbt","Sie berücksichtigen zu viele Dimensionen"],c:1,e:"Schichtmodelle messen nur vertikale Merkmale (Einkommen, Bildung). Milieumodelle zeigen, dass Menschen gleicher sozialer Lage sehr unterschiedliche Werte und Lebensstile haben können."},
  {cat:"modelle",diff:"schwer",q:"Was meint Singularisierung als soziologischer Begriff (Andreas Reckwitz)?",a:["Wachsende Klassengesellschaft","Zunehmende Aufwertung des Einzigartigen und Besonderen in Konsum, Arbeit und Biografie","Rückgang von Individualismus","Homogenisierung der Gesellschaft"],c:1,e:"Reckwitz beschreibt eine 'Gesellschaft der Singularitäten': Das Besondere, Einzigartige wird zum gesellschaftlichen Leitwert – in Berufen, Produkten, Orten. Das verschärft neue Formen sozialer Ungleichheit."},
  {cat:"modelle",diff:"leicht",q:"Was misst der Gini-Koeffizient?",a:["Das Durchschnittseinkommen","Das Ausmaß der Einkommensungleichheit in einer Gesellschaft","Die Arbeitslosenquote","Die Staatsschulden"],c:1,e:"Der Gini-Koeffizient reicht von 0 (vollständige Gleichheit) bis 1 (maximale Ungleichheit). Deutschland liegt bei ca. 0,31 beim Einkommen – nach Umverteilung. Vor Umverteilung ist er deutlich höher."},
  {cat:"modelle",diff:"mittel",q:"Welches Modell betont, dass soziale Ungleichheit durch unterschiedliche 'Felder' (z.B. Wissenschaft, Kunst, Wirtschaft) geprägt wird?",a:["Marxismus","Dahrendorfs Schichtmodell","Bourdieus Feldtheorie","Becks Risikogesellschaft"],c:2,e:"Bourdieu: Gesellschaft ist in verschiedene Felder unterteilt, in denen unterschiedliche Kapitalarten zählen. Im wissenschaftlichen Feld zählt kulturelles Kapital, im wirtschaftlichen Feld ökonomisches Kapital."},

  // ── FACHBEGRIFFE (10 Fragen) ──
  {cat:"begriffe",diff:"leicht",q:"Was ist 'soziale Mobilität'?",a:["Die Fähigkeit, umzuziehen","Bewegung zwischen sozialen Positionen im Laufe des Lebens","Das Einkommen einer Person","Die Bildung der Eltern"],c:1,e:"Soziale Mobilität beschreibt Auf- oder Abstiege in der Sozialstruktur. Intergenerational = zwischen Generationen. Intragenerational = im eigenen Lebenslauf."},
  {cat:"begriffe",diff:"leicht",q:"Was versteht man unter 'horizontaler sozialer Ungleichheit'?",a:["Unterschiede im Einkommen","Ungleichheiten quer zur Hierarchie, z.B. nach Geschlecht oder Ethnizität","Unterschiede zwischen Oben und Unten","Geografische Unterschiede"],c:1,e:"Horizontale Ungleichheiten verlaufen quer zur vertikalen Hierarchie: Frauen und Männer auf gleichem Einkommensniveau können trotzdem ungleich behandelt werden – Gender Pay Gap."},
  {cat:"begriffe",diff:"mittel",q:"Was ist das 'Leistungsprinzip'?",a:["Jeder bekommt gleich viel","Wer mehr leistet, soll mehr erhalten","Der Staat verteilt nach Bedarf","Herkunft bestimmt den Status"],c:1,e:"Das Leistungsprinzip rechtfertigt Ungleichheit durch individuelle Leistung. Es ist Grundlage liberaler Gerechtigkeitsvorstellungen. Kritiker fragen: Ist Leistung wirklich frei von sozialer Herkunft?"},
  {cat:"begriffe",diff:"mittel",q:"Was bezeichnet der Begriff 'Prekarität'?",a:["Hohes Einkommen ohne Jobgarantie","Unsichere, instabile Lebensverhältnisse und Beschäftigung","Staatliche Rente","Kulturelles Kapital"],c:1,e:"Prekarität beschreibt unsichere Beschäftigung (Zeitverträge, Minijobs) und instabile Lebensverhältnisse. Betroffen sind oft Geringqualifizierte, Migranten und Frauen."},
  {cat:"begriffe",diff:"mittel",q:"Was meint 'Chancengleichheit' im Gegensatz zu 'Ergebnisgleichheit'?",a:["Beide bedeuten dasselbe","Chancengleichheit = gleiche Startbedingungen; Ergebnisgleichheit = gleiche Endresultate","Chancengleichheit = Ergebnis ist gleich","Nur ökonomische Begriffe"],c:1,e:"Chancengleichheit (liberal): Gleiche Ausgangsbedingungen genügen – danach entscheidet Leistung. Ergebnisgleichheit (egalitär): Auch die Verteilung der Outcomes muss gerechter werden."},
  {cat:"begriffe",diff:"schwer",q:"Was ist 'strukturelle Diskriminierung'?",a:["Absichtliche Benachteiligung durch Einzelpersonen","Benachteiligung durch Strukturen und Normen, nicht notwendig absichtlich","Biologisch bedingte Unterschiede","Gesetzlich vorgeschriebene Ungleichheit"],c:1,e:"Strukturelle Diskriminierung entsteht durch Regeln, Normen und Institutionen, die bestimmte Gruppen benachteiligen – auch ohne böse Absicht. Bsp.: Schulnoten, die Migrantenkinder systematisch benachteiligen."},
  {cat:"begriffe",diff:"leicht",q:"Was bedeutet 'vertikale soziale Ungleichheit'?",a:["Unterschiede nach Region","Hierarchische Unterschiede in Einkommen, Prestige oder Macht – oben/unten","Unterschiede nach Alter","Gleiche Chancen für alle"],c:1,e:"Vertikale Ungleichheit meint die klassische Oben-Unten-Dimension: Wer hat mehr Geld, mehr Prestige, mehr Macht? Das ist die traditionelle Perspektive der Sozialstrukturanalyse."},
  {cat:"begriffe",diff:"mittel",q:"Was ist der 'Gender Pay Gap'?",a:["Unterschied in der Rentenversicherung","Lohnunterschied zwischen Männern und Frauen","Unterschied in der Bildungszeit","Unterschied in der Arbeitszeit"],c:1,e:"Der Gender Pay Gap beschreibt, dass Frauen im Durchschnitt weniger verdienen als Männer. In Deutschland liegt der unbereinigte GPG bei ca. 18%. Ursachen: Berufsstruktur, Teilzeit, Diskriminierung."},
  {cat:"begriffe",diff:"schwer",q:"Was ist 'Reproduktion sozialer Ungleichheit'?",a:["Biologische Vererbung","Mechanismen, durch die Ungleichheiten von Generation zu Generation weitergegeben werden","Staatliche Umverteilung","Aufstieg durch Bildung"],c:1,e:"Reproduktion meint, dass Ungleichheiten sich selbst erhalten: Kinder aus armen Familien bleiben oft arm. Bourdieu erklärt dies durch Kapitalübertragung (ökonomisch, kulturell, sozial)."},
  {cat:"begriffe",diff:"schwer",q:"Was versteht die Soziologie unter 'sozialer Exklusion'?",a:["Nur Armut","Ausschluss von gesellschaftlicher Teilhabe in mehreren Lebensbereichen","Freiwilliger Rückzug","Politische Apathie"],c:1,e:"Soziale Exklusion = multidimensionaler Ausschluss: nicht nur arm sein, sondern auch keinen Job, keinen Zugang zu Bildung, Gesundheit, sozialen Netzwerken haben. Konzept wichtig für EU-Sozialpolitik."},

  // ── GERECHTIGKEITSTHEORIEN (10 Fragen) ──
  {cat:"gerechtigkeit",diff:"leicht",q:"Welche Position vertritt der Liberalismus zur sozialen Ungleichheit?",a:["Völlige Gleichheit ist das Ziel","Ungleichheit ist legitim, wenn Chancengleichheit herrscht","Der Staat soll stark umverteilen","Herkunft darf keine Rolle spielen – alles muss gleich sein"],c:1,e:"Liberalismus (z.B. Nozick): Solange alle die gleichen Chancen haben und niemand betrogen wird, sind Ungleichheiten im Ergebnis gerecht und Ausdruck von Freiheit."},
  {cat:"gerechtigkeit",diff:"leicht",q:"Was fordert der Egalitarismus?",a:["Nur Chancengleichheit","Gerechtere Verteilung von Gütern durch Umverteilung","Keine staatliche Einmischung","Leistung soll alles bestimmen"],c:1,e:"Egalitarismus will nicht nur gleiche Startchancen, sondern auch gerechtere Verteilung von Gütern und Ressourcen – z.B. durch progressive Besteuerung und Sozialtransfers."},
  {cat:"gerechtigkeit",diff:"mittel",q:"Was ist John Rawls' 'Schleier des Nichtwissens'?",a:["Ein Zensurgesetz","Gedankenexperiment: Gerechte Regeln wählen, ohne die eigene Position zu kennen","Eine Metapher für Armut","Ein Modell sozialer Schichten"],c:1,e:"Rawls fragt: Welche Regeln würde ich wählen, wenn ich nicht wüsste, wo ich in der Gesellschaft lande? Daraus folgt: Ungleichheiten sind nur gerecht, wenn sie den Schwächsten nützen (Differenzprinzip)."},
  {cat:"gerechtigkeit",diff:"mittel",q:"Was sagt der Funktionalismus (Davis & Moore) zur Ungleichheit?",a:["Ungleichheit ist immer ungerecht","Ungleichheit ist funktional notwendig, um wichtige Positionen zu besetzen","Alle Positionen sind gleich wichtig","Ungleichheit ist ein Systemfehler"],c:1,e:"Davis & Moore: Gesellschaft braucht Anreize, damit wichtige Positionen (Ärzte, Richter) attraktiv sind. Höheres Prestige und Einkommen sind funktionale Notwendigkeit."},
  {cat:"gerechtigkeit",diff:"mittel",q:"Was kritisiert die Konflikttheorie am Funktionalismus?",a:["Dass er zu wenig über Schulen sagt","Ungleichheit diene Machtinteressen, nicht der gesamten Gesellschaft","Dass er Klassen zu stark betont","Dass er soziale Mobilität überschätzt"],c:1,e:"Konflikttheoretiker (z.B. Marx, Dahrendorf): Ungleichheit dient nicht der Gesellschaft als Ganzes, sondern den Interessen privilegierter Gruppen, die Macht einsetzen, um Status zu erhalten."},
  {cat:"gerechtigkeit",diff:"schwer",q:"Wie rechtfertigt Rawls' Differenzprinzip bestimmte Ungleichheiten?",a:["Jede Ungleichheit ist gerecht","Ungleichheiten sind gerecht, wenn sie die am schlechtesten Gestellten besser stellen","Alle müssen gleich viel verdienen","Nur Herkunftsungleichheiten sind ungerecht"],c:1,e:"Rawls' Differenzprinzip: Soziale Ungleichheiten (z.B. höhere Löhne für Ärzte) sind akzeptabel, wenn sie dazu führen, dass auch die ärmsten Gesellschaftsmitglieder davon profitieren."},
  {cat:"gerechtigkeit",diff:"schwer",q:"Was versteht Amartya Sen unter dem 'Befähigungsansatz' (Capability Approach)?",a:["Staatliche Berufsausbildung","Gerechtigkeit bedeutet, Menschen reale Fähigkeiten und Handlungsmöglichkeiten zu ermöglichen","Gleiche Geldverteilung für alle","Leistungsprinzip im Bildungssystem"],c:1,e:"Sen: Nicht Ressourcen allein zählen, sondern was Menschen damit tun können (Capabilities). Eine behinderte Person braucht mehr Ressourcen, um die gleiche Freiheit zu haben. Beeinflusst UN-Entwicklungsziele."},
  {cat:"gerechtigkeit",diff:"leicht",q:"Was ist das Prinzip der Bedarfsgerechtigkeit?",a:["Jeder bekommt dasselbe","Wer mehr braucht, bekommt mehr","Wer mehr leistet, bekommt mehr","Alle Ausgangsbedingungen sind gleich"],c:1,e:"Bedarfsgerechtigkeit: Ressourcen werden nach Bedarf verteilt – Kranke bekommen mehr Gesundheitsleistungen, Arme mehr Unterstützung. Grundlage des deutschen Sozialstaats."},
  {cat:"gerechtigkeit",diff:"mittel",q:"Warum kritisieren Egalitaristen das Leistungsprinzip?",a:["Leistung sei nicht messbar","Leistung sei selbst durch soziale Herkunft geprägt – also kein fairer Maßstab","Leistung sei zu objektiv","Leistung und Herkunft sind völlig getrennt"],c:1,e:"Kritik: Wer in einer reichen Familie aufwächst, hat bessere Bildung, Netzwerke und Gesundheit. Leistung ist daher nicht unabhängig von Herkunft. Das Leistungsprinzip verschleiert soziale Startungleichheiten."},
  {cat:"gerechtigkeit",diff:"schwer",q:"Was unterscheidet formale von substantieller Chancengleichheit?",a:["Beide sind identisch","Formale = rechtliche Gleichstellung; substantielle = reale Gleichheit der Ausgangsbedingungen","Formale = mehr Rechte für Arme","Substantielle = nur gleiche Gesetze"],c:1,e:"Formale Chancengleichheit: Alle haben dieselben Rechte (z.B. Schulpflicht). Substantielle: Auch die realen Bedingungen müssen angeglichen werden (z.B. Nachhilfe, Kita-Qualität). Nur dann ist Chancengleichheit real."},

  // ── SOZIALSTAAT (10 Fragen) ──
  {cat:"sozialstaat",diff:"leicht",q:"Welche gehört NICHT zu den 5 Säulen der deutschen Sozialversicherung?",a:["Krankenversicherung","Rentenversicherung","Bildungsversicherung","Pflegeversicherung"],c:2,e:"Die 5 Säulen sind: Kranken-, Renten-, Pflege-, Unfall- und Arbeitslosenversicherung. Eine Bildungsversicherung gibt es im deutschen Sozialversicherungssystem nicht."},
  {cat:"sozialstaat",diff:"leicht",q:"In welchem Artikel des Grundgesetzes ist das Sozialstaatsprinzip verankert?",a:["Art. 1 GG","Art. 14 GG","Art. 20 GG","Art. 3 GG"],c:2,e:"Art. 20 GG: Deutschland ist ein demokratischer und sozialer Bundesstaat. Das Sozialstaatsprinzip verpflichtet den Staat zur Daseinsvorsorge und zum Ausgleich sozialer Ungleichheiten."},
  {cat:"sozialstaat",diff:"mittel",q:"Was ist ein typisches Argument gegen einen zu starken Sozialstaat?",a:["Er verhindert Armut","Er kann Fehlanreize schaffen und Eigenverantwortung hemmen","Er fördert die Wirtschaft","Er stärkt die Demokratie"],c:1,e:"Kritiker (liberal): Zu hohe Sozialleistungen können Anreize zur Arbeit reduzieren. Zudem sei die Finanzierbarkeit langfristig fraglich (demografischer Wandel). Befürworter betonen soziale Stabilität."},
  {cat:"sozialstaat",diff:"mittel",q:"Was beschreibt 'Umverteilung' im Sozialstaat?",a:["Alle zahlen gleich viel Steuern","Reiche zahlen mehr, um Ärmere zu unterstützen","Jeder behält sein Einkommen","Nur Arbeitgeber finanzieren den Sozialstaat"],c:1,e:"Umverteilung = progressives Steuersystem + Sozialtransfers. Höhere Einkommen werden stärker besteuert; die Einnahmen fließen als Kindergeld, Wohngeld oder Bürgergeld an ärmere Gruppen."},
  {cat:"sozialstaat",diff:"mittel",q:"Wie unterscheidet sich Deutschland vom US-amerikanischen Sozialmodell?",a:["In den USA gibt es mehr staatliche Fürsorge","Deutschland setzt auf Pflichtversicherungen; USA stärker auf Eigenverantwortung","Beide Systeme sind identisch","Die USA haben kein Rentensystem"],c:1,e:"Deutschland: Bismarcksches Sozialversicherungsmodell mit Pflichtbeiträgen. USA: Marktwirtschaftlich geprägt – private Krankenversicherungen, geringere Sozialleistungen, höhere Ungleichheit (höherer Gini-Koeffizient)."},
  {cat:"sozialstaat",diff:"schwer",q:"Was versteht man unter 'sozialer Durchlässigkeit'?",a:["Das Prinzip gleicher Steuern","Die Möglichkeit, durch eigene Leistung in höhere Schichten aufzusteigen","Staatliche Wirtschaftskontrolle","Gleiches Wahlrecht für alle"],c:1,e:"Soziale Durchlässigkeit = soziale Mobilität nach oben. Hohe Durchlässigkeit: Herkunft entscheidet weniger über Zukunft. Deutschland hat im OECD-Vergleich eine relativ geringe Durchlässigkeit."},
  {cat:"sozialstaat",diff:"leicht",q:"Was ist das Bürgergeld (früher Hartz IV)?",a:["Eine freiwillige Zusatzversicherung","Staatliche Grundsicherung für Erwerbslose und Bedürftige","Ein Kindergeldprogramm","Eine betriebliche Altersvorsorge"],c:1,e:"Das Bürgergeld (2023 eingeführt) ist die staatliche Grundsicherung für Arbeitsuchende. Es soll das Existenzminimum sichern und Vermittlung in Arbeit unterstützen. Kritiker sehen Fehlanreize, Befürworter sehen Würdeschutz."},
  {cat:"sozialstaat",diff:"mittel",q:"Was ist das Äquivalenzprinzip in der Sozialversicherung?",a:["Jeder bekommt gleich viel","Leistungen richten sich nach vorherigen Beiträgen","Der Staat zahlt alle Kosten","Nur Bedürftige erhalten Leistungen"],c:1,e:"Äquivalenzprinzip: Wer mehr eingezahlt hat, erhält mehr Leistung (z.B. höhere Rente bei höheren Beitragsjahren). Steht im Spannungsverhältnis zum Solidarprinzip (alle teilen Risiken)."},
  {cat:"sozialstaat",diff:"schwer",q:"Vor welcher sozialpolitischen Herausforderung steht Deutschland durch den demografischen Wandel?",a:["Zu viele junge Beitragszahler","Immer mehr Rentner bei sinkender Zahl von Beitragszahlern – Finanzierungslücke","Sinkende Lebenserwartung","Zu niedrige Geburtenrate führt zu weniger Rentnern"],c:1,e:"Demografischer Wandel: Babyboomer gehen in Rente, weniger Junge zahlen Beiträge. Folge: Rentensystem, Pflegeversicherung und Krankenversicherung kommen unter Druck. Lösungen: Einwanderung, längere Arbeitszeiten, Kapitaldeckung."},
  {cat:"sozialstaat",diff:"schwer",q:"Was ist sozialpolitisch mit 'aktivierendem Sozialstaat' gemeint?",a:["Mehr passive Transferleistungen","Fördern und Fordern: Unterstützung verbunden mit Eigenverantwortung und Aktivierung","Abschaffung des Sozialstaats","Vollbeschäftigung durch staatliche Jobs"],c:1,e:"Aktivierender Sozialstaat (seit Schröder/Hartz): Leistungen werden mit Gegenleistungen verknüpft (Bewerbungspflicht, Weiterbildung). Ziel: Eigeninitiative fördern. Kritik: Zumutbarkeit, Würde, strukturelle Arbeitslosigkeit."},

  // ── ANALYSE & PRÜFUNG (8 Fragen) ──
  {cat:"analyse",diff:"leicht",q:"Was bedeutet der Operator 'analysieren' in einer Abituraufgabe?",a:["Zusammenfassen ohne Wertung","Systematisch untersuchen, Merkmale herausarbeiten, Zusammenhänge erklären","Eine eigene Meinung äußern","Einen Begriff nur definieren"],c:1,e:"'Analysieren' = mehr als beschreiben. Du musst Merkmale benennen, Zusammenhänge herstellen und mit Fachbegriffen/Modellen arbeiten. Im erhöhten Niveau: auch Ursachen und Wirkungen einbeziehen."},
  {cat:"analyse",diff:"leicht",q:"Was ist der Unterschied zwischen 'erörtern' und 'bewerten'?",a:["Kein Unterschied","Erörtern = Pro/Contra abwägen; Bewerten = eigenes Urteil fällen","Bewerten = nur beschreiben","Erörtern = eigene Meinung, Bewerten = neutral"],c:1,e:"Erörtern: Argumente für und gegen eine These gegenüberstellen und abwägen. Bewerten: ein fundiertes eigenes Urteil mit Kriterien begründen. Beides erfordert Fachbegriffe und Belege."},
  {cat:"analyse",diff:"mittel",q:"Wie wendet man ein Sozialstrukturmodell auf ein Fallbeispiel an?",a:["Man nennt nur den Namen des Modells","Modell erklären, Merkmale des Falls benennen, zuordnen, Aussagekraft bewerten","Nur das Modell kritisieren","Alle Modelle aufzählen"],c:1,e:"Ablauf: 1) Modell kurz erklären, 2) Merkmale des Falls benennen, 3) Merkmale dem Modell zuordnen, 4) Aussagekraft und Grenzen des Modells für diesen Fall bewerten."},
  {cat:"analyse",diff:"mittel",q:"Was gehört in ein gelungenes Fazit einer Erörterung?",a:["Nur eine Zusammenfassung","Eigenes begründetes Urteil, Abwägung der Argumente, ggf. Ausblick","Neue Argumente","Nur eine Definition"],c:1,e:"Das Fazit zeigt analytische Kompetenz: Du wägst ab, welche Seite überzeugender ist und warum – mit Bezug auf deine Argumente. Kein neues Material, aber ein klares, begründetes Urteil."},
  {cat:"analyse",diff:"schwer",q:"Was ist bei einer Gestaltungsaufgabe (z.B. Rede, Kommentar) besonders wichtig?",a:["Nur Fachbegriffe","Adressatengerechte Sprache, klare Position, Genre einhalten, Fachinhalt einbetten","Neutral bleiben","Möglichst viele Modelle nennen"],c:1,e:"Gestaltungsaufgaben: Genre beachten (Rede = direkte Ansprache, Kommentar = argumentativ). Fachliches Wissen korrekt einbetten. Klar Position beziehen – das ist der Unterschied zur Erörterung."},
  {cat:"analyse",diff:"schwer",q:"Warum sind konkrete Beispiele und Statistiken in der Abiturprüfung wichtig?",a:["Sie sind nicht nötig","Sie belegen Argumente, machen Aussagen nachprüfbar, zeigen Anwendungskompetenz","Sie ersetzen Fachbegriffe","Nur bei Gestaltungsaufgaben"],c:1,e:"Ohne Belege bleiben Argumente abstrakt. Im erhöhten Niveau wird erwartet, dass du gesellschaftliche Probleme mit empirischen Daten (Gini-Koeffizient, PISA-Ergebnisse, GPG) untermauern kannst."},
  {cat:"analyse",diff:"mittel",q:"Was bedeutet 'Perspektivwechsel' in einer Abituraufgabe PGW?",a:["Eine andere Sprache wählen","Einen Sachverhalt aus der Sicht verschiedener Akteure oder Theorien beleuchten","Die eigene Meinung wechseln","Nur die Gegenseite darstellen"],c:1,e:"Perspektivwechsel = Sachverhalt durch verschiedene Brillen betrachten: Wie sieht ein Liberaler soziale Ungleichheit? Wie ein Egalitarist? Wie Bourdieu? Das zeigt Multiperspektivität und Analysekompetenz."},
  {cat:"analyse",diff:"schwer",q:"Was ist der Unterschied zwischen Ursachen und Folgen sozialer Ungleichheit in einer Analyse?",a:["Es gibt keinen Unterschied","Ursachen = was Ungleichheit erzeugt (Herkunft, Kapital); Folgen = was daraus resultiert (Armut, Gesundheit, Bildung)","Folgen sind immer positiv, Ursachen negativ","Ursachen kommen nach den Folgen"],c:1,e:"Gute Analysen trennen klar: Ursachen (z.B. Bildungsungleichheit durch Herkunft) von Folgen (z.B. geringeres Einkommen, schlechtere Gesundheit, geringere politische Teilhabe). Beides mit Modellen und Belegen stützen."},
];

const CAT_META = {
  modelle:      { name: "Sozialstrukturmodelle", dot: "#a78bfa", bg: "rgba(167,139,250,0.12)", c: "#c4b5fd" },
  begriffe:     { name: "Fachbegriffe",          dot: "#34d399", bg: "rgba(52,211,153,0.12)",  c: "#6ee7b7" },
  gerechtigkeit:{ name: "Gerechtigkeitstheorien",dot: "#fbbf24", bg: "rgba(251,191,36,0.12)",  c: "#fde68a" },
  sozialstaat:  { name: "Sozialstaat",            dot: "#f472b6", bg: "rgba(244,114,182,0.12)", c: "#f9a8d4" },
  analyse:      { name: "Analyse & Prüfung",      dot: "#60a5fa", bg: "rgba(96,165,250,0.12)",  c: "#93c5fd" },
};
const DIFF_LABELS = { leicht: "Leicht", mittel: "Mittel", schwer: "Schwer" };

let questions = [], idx = 0, correct = 0, wrong = 0;
let catScores = {}, selectedCat = "all", selectedDiff = "all";

function shuffle(a) {
  for (let i = a.length - 1; i > 0; i--) {
    const j = Math.floor(Math.random() * (i + 1));
    [a[i], a[j]] = [a[j], a[i]];
  }
  return a;
}

function getFiltered() {
  return QUESTIONS.filter(q =>
    (selectedCat === "all" || q.cat === selectedCat) &&
    (selectedDiff === "all" || q.diff === selectedDiff)
  );
}

function updateCounts() {
  document.getElementById("count-all").textContent = QUESTIONS.length + " Fragen";
  Object.keys(CAT_META).forEach(cat => {
    const count = QUESTIONS.filter(q => q.cat === cat).length;
    document.getElementById("count-" + cat).textContent = count + " Fragen";
  });
  document.getElementById("total-count").textContent = getFiltered().length;
}

document.querySelectorAll(".cat-card").forEach(c => {
  c.onclick = () => {
    document.querySelectorAll(".cat-card").forEach(x => x.classList.remove("active"));
    c.classList.add("active");
    selectedCat = c.dataset.cat;
    document.getElementById("total-count").textContent = getFiltered().length;
  };
});

document.querySelectorAll(".diff-btn").forEach(b => {
  b.onclick = () => {
    document.querySelectorAll(".diff-btn").forEach(x => x.classList.remove("active"));
    b.classList.add("active");
    selectedDiff = b.dataset.diff;
    document.getElementById("total-count").textContent = getFiltered().length;
  };
});

function showScreen(id) {
  document.querySelectorAll(".screen").forEach(s => s.classList.remove("active"));
  document.getElementById(id).classList.add("active");
}

function startGame() {
  const pool = getFiltered();
  if (pool.length === 0) { alert("Keine Fragen für diese Auswahl."); return; }
  questions = shuffle([...pool]);
  idx = 0; correct = 0; wrong = 0; catScores = {};
  showScreen("quiz-screen");
  renderQuestion();
}

function showStart() { showScreen("start-screen"); }

function renderQuestion() {
  if (idx >= questions.length) { showResult(); return; }
  const q = questions[idx];
  const pct = Math.round((idx / questions.length) * 100);
  document.getElementById("progress-fill").style.width = pct + "%";
  document.getElementById("q-counter").textContent = "Frage " + (idx + 1) + " / " + questions.length;
  document.getElementById("score-pill").textContent = correct + " richtig";

  const meta = CAT_META[q.cat];
  const catPill = document.getElementById("cat-pill");
  catPill.textContent = meta.name;
  catPill.style.background = meta.bg;
  catPill.style.color = meta.c;

  const diffPill = document.getElementById("diff-pill");
  diffPill.textContent = DIFF_LABELS[q.diff];
  diffPill.className = "diff-pill diff-" + q.diff;

  document.getElementById("q-text").textContent = q.q;
  document.getElementById("explanation").innerHTML = "";
  document.getElementById("next-btn").style.display = "none";

  const shuffled = q.a.map((text, i) => ({ text, origIdx: i }));
  shuffle(shuffled);

  const container = document.getElementById("answers");
  container.innerHTML = "";
  shuffled.forEach(({ text, origIdx }) => {
    const btn = document.createElement("button");
    btn.className = "ans-btn";
    btn.textContent = text;
    btn.onclick = () => answer(origIdx === q.c, q, container, btn);
    container.appendChild(btn);
  });
}

function answer(isCorrect, q, container, clicked) {
  if (!catScores[q.cat]) catScores[q.cat] = { c: 0, t: 0 };
  catScores[q.cat].t++;
  container.querySelectorAll(".ans-btn").forEach(b => b.classList.add("disabled"));

  if (isCorrect) {
    correct++;
    catScores[q.cat].c++;
    clicked.classList.add("correct");
  } else {
    wrong++;
    clicked.classList.add("wrong");
    container.querySelectorAll(".ans-btn").forEach(b => {
      if (b.textContent === q.a[q.c]) b.classList.add("reveal");
    });
  }
  document.getElementById("explanation").innerHTML =
    '<div class="explanation">' + q.e + '</div>';
  document.getElementById("next-btn").style.display = "block";
}

function nextQuestion() { idx++; renderQuestion(); }

function showResult() {
  showScreen("result-screen");
  const total = correct + wrong;
  const pct = total > 0 ? Math.round((correct / total) * 100) : 0;
  document.getElementById("res-correct").textContent = correct;
  document.getElementById("res-wrong").textContent = wrong;
  document.getElementById("res-pct").textContent = pct + "%";

  let grade, msg, gradeColor;
  if (pct >= 90) { grade = "A+"; msg = "Hervorragend – du bist gut vorbereitet!"; gradeColor = "#34d399"; }
  else if (pct >= 75) { grade = "B"; msg = "Solide – noch ein paar Lücken schließen."; gradeColor = "#a78bfa"; }
  else if (pct >= 55) { grade = "C"; msg = "Weiter üben – du bist auf dem richtigen Weg!"; gradeColor = "#fbbf24"; }
  else { grade = "D"; msg = "Nochmal von vorne – du schaffst das!"; gradeColor = "#f87171"; }

  document.getElementById("result-grade").textContent = grade;
  document.getElementById("result-grade").style.color = gradeColor;
  document.getElementById("result-msg").textContent = msg;

  const catDiv = document.getElementById("cat-results");
  catDiv.innerHTML = "";
  Object.entries(catScores).forEach(([cat, { c, t }]) => {
    const p = Math.round((c / t) * 100);
    const meta = CAT_META[cat];
    catDiv.innerHTML += `
      <div class="cat-result-row">
        <div class="cat-result-name">${meta.name}</div>
        <div class="cat-bar-track"><div class="cat-bar-fill" style="width:${p}%;background:${meta.dot}"></div></div>
        <div class="cat-result-pct">${p}%</div>
      </div>`;
  });
}

updateCounts();
</script>
</body>
</html>
