<html lang="en" data-theme="blue">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Designing Meaningful Teaching Materials — KAPP Workshop</title>
<style>
/* ===========================================================================
   1. TOKENS
   Accent hues live in variables so the pink theme is a single swap.
   Everything else (slate neutrals, radii, shadows) matches the original app.
   ========================================================================= */
:root {
  --accent-50:  #eff6ff;
  --accent-100: #dbeafe;
  --accent-500: #3b82f6;
  --accent-600: #2563eb;
  --accent-700: #1d4ed8;
  --accent-900: #1e3a8a;
  --grad-from:  #312e81;   /* speaker card / dark panels */
  --grad-to:    #0f172a;

  /* Fixed neutrals */
  --page:   #f8fafc;
  --card:   #ffffff;
  --line:   #e2e8f0;
  --line-2: #cbd5e1;
  --ink:    #000000;       /* body copy is black, by request */
  --head:   #0f172a;
  --muted:  #1a1a1a;
  --on-dark:#d3d9e6;

  --ok-bg: #ecfdf5; --ok-line: #6ee7b7; --ok-ink: #065f46;
  --no-bg: #fef2f2; --no-line: #fca5a5; --no-ink: #991b1b;
  --warn-bg:#fffbeb; --warn-line:#fcd34d; --warn-ink:#92400e;
  --navy:  #16305c;

  --r-lg: 16px; --r-md: 12px; --r-sm: 8px;
  --shadow: 0 1px 2px rgba(15,23,42,.06), 0 1px 3px rgba(15,23,42,.04);
  --sans: system-ui, -apple-system, "Segoe UI", Roboto, Helvetica, Arial, sans-serif;
}

html[data-theme="pink"] {
  --accent-50:  #fdf2f8;
  --accent-100: #fce7f3;
  --accent-500: #ec4899;
  --accent-600: #db2777;
  --accent-700: #be185d;
  --accent-900: #831843;
  --grad-from:  #831843;
  --grad-to:    #3f0d25;
}

* { box-sizing: border-box; }
body {
  margin: 0; background: var(--page); color: var(--ink);
  font: 400 17px/1.65 var(--sans); -webkit-text-size-adjust: 100%;
}
h1,h2,h3,h4 { color: var(--head); margin: 0; line-height: 1.25; font-weight: 700; }
p { margin: 0 0 1em; } p:last-child { margin-bottom: 0; }
strong { font-weight: 700; color: var(--head); }
button { font-family: inherit; }

/* ===========================================================================
   2. FRAME — header, sidebar, main, footer
   ========================================================================= */
.app { display: flex; flex-direction: column; min-height: 100vh; }

.topbar {
  display: flex; align-items: center; gap: 14px;
  background: var(--card); border-bottom: 1px solid var(--line);
  padding: 14px 28px; position: sticky; top: 0; z-index: 30;
}
.topbar__mark {
  width: 42px; height: 42px; border-radius: var(--r-md); flex: none;
  background: var(--accent-600); color: #fff;
  display: grid; place-items: center; font-size: 20px;
}
.topbar__title { font-size: 18px; }
.topbar__sub {
  font-size: 13px; font-weight: 700; letter-spacing: .06em;
  text-transform: uppercase; color: var(--muted); margin-top: 3px;
}
.topbar__right { margin-left: auto; display: flex; align-items: center; gap: 20px; }
.stat { text-align: right; }
.stat span { display: block; font-size: 13px; font-weight: 600; text-transform: uppercase; color: var(--muted); }
.stat b { font-size: 20px; color: var(--head); }
.stat b.mono { font-family: ui-monospace, Menlo, monospace; color: var(--accent-600); }
.themeBtn {
  display: flex; align-items: center; gap: 8px; cursor: pointer;
  background: var(--card); border: 1px solid var(--line);
  border-radius: var(--r-sm); padding: 8px 12px; font-size: 14px; font-weight: 600; color: var(--ink);
}
.themeBtn:hover { background: var(--page); }
.themeBtn i { width: 16px; height: 16px; border-radius: 50%; background: var(--accent-600); display: block; }

.body { display: flex; flex: 1; min-height: 0; }

.side {
  width: 280px; flex: none; background: var(--card);
  border-right: 1px solid var(--line);
  padding: 26px 0 26px 20px; display: flex; flex-direction: column;
  position: sticky; top: 71px; height: calc(100vh - 71px);
}
.side h2 {
  font-size: 14px; font-weight: 700; letter-spacing: .12em;
  text-transform: uppercase; color: var(--muted); margin-bottom: 18px;
}
.side nav { flex: 1; overflow-y: auto; padding-right: 16px; }
.side ol { list-style: none; margin: 0; padding: 0; }
.tab {
  display: flex; align-items: center; gap: 12px; width: 100%;
  text-align: left; cursor: pointer; background: none; border: 0;
  border-radius: var(--r-md); padding: 11px 12px; margin-bottom: 4px;
  font-size: 16px; line-height: 1.3; color: var(--ink);
}
.tab:hover { background: var(--page); }
.tab .n {
  width: 26px; height: 26px; border-radius: 50%; flex: none;
  display: grid; place-items: center; font-size: 12px; font-weight: 700;
  background: var(--page); color: var(--muted);
}
.tab[aria-current="true"] {
  background: var(--accent-50); color: var(--accent-700); font-weight: 700;
  box-shadow: inset 3px 0 0 var(--accent-600);
}
.tab[aria-current="true"] .n { background: var(--accent-600); color: #fff; }

.note {
  margin: 18px 16px 0 0; padding: 16px; border-radius: var(--r-md);
  background: var(--accent-900); color: #fff;
}
.note__head { display: flex; align-items: center; gap: 10px; margin-bottom: 10px; }
.note__head img { width: 36px; height: 36px; border-radius: 50%; object-fit: cover; border: 2px solid rgba(255,255,255,.3); }
.note__head span { font-size: 12px; font-weight: 700; letter-spacing: .08em; text-transform: uppercase; opacity: .7; }
.note p { font-size: 14px; font-style: italic; margin: 0; color: #fff; }

main { flex: 1; min-width: 0; padding: 34px 32px 70px; }
.view { max-width: 1000px; }
.view > section { margin-bottom: 48px; }
.view > section:last-child { margin-bottom: 0; }

.foot {
  background: var(--card); border-top: 1px solid var(--line);
  padding: 12px 28px; font-size: 13px; color: var(--muted);
  display: flex; justify-content: space-between; gap: 16px; flex-wrap: wrap;
}

/* ===========================================================================
   3. TYPE + PRIMITIVES
   ========================================================================= */
h2.h { font-size: 27px; margin-bottom: 12px; }
h3.h { font-size: 22px; margin-bottom: 12px; }
h4.h { font-size: 18px; margin-bottom: 8px; }
.lede { font-size: 17px; color: var(--ink); max-width: 74ch; }
.small { font-size: 15px; color: var(--ink); }
.eyebrow {
  display: inline-block; font-size: 13px; font-weight: 700;
  letter-spacing: .08em; text-transform: uppercase; color: var(--accent-600);
  margin-bottom: 10px;
}

.card {
  background: var(--card); border: 1px solid var(--line);
  border-radius: var(--r-lg); padding: 24px; box-shadow: var(--shadow);
}
.card--tint { background: var(--accent-50); border-color: var(--accent-100); }
.card--flat { box-shadow: none; }
.grid { display: grid; gap: 20px; }
.g2 { grid-template-columns: repeat(2, minmax(0,1fr)); }
.g3 { grid-template-columns: repeat(3, minmax(0,1fr)); }
.topline { border-top: 4px solid var(--accent-500); }

.dark {
  background: linear-gradient(135deg, var(--grad-from), var(--grad-to));
  color: #fff; border-radius: var(--r-lg); padding: 28px;
}
.dark h3, .dark h4 { color: #fff; }
.dark p { color: var(--on-dark); }
.navy { background: linear-gradient(135deg,#0b2050,#16336e); color: #fff; border-radius: var(--r-lg); padding: 28px; }
.navy p.stmt { font-size: 21px; font-weight: 700; color: #fff; line-height: 1.4; }
.navy p.sub  { font-size: 16px; color: #b9c6de; margin: 12px 0 0; }

.pill {
  display: inline-block; background: var(--head); color: #fff;
  border-radius: var(--r-sm); padding: 5px 11px;
  font-size: 13px; font-weight: 700;
}
.pill--accent { background: var(--accent-600); }
.dot {
  width: 30px; height: 30px; border-radius: 50%; flex: none;
  display: grid; place-items: center; font-size: 14px; font-weight: 700;
  background: var(--accent-100); color: var(--accent-700);
}
.dot--solid { background: var(--accent-600); color: #fff; }

.row {
  display: flex; gap: 20px; flex-wrap: wrap; align-items: flex-start;
  background: var(--card); border: 1px solid var(--line);
  border-radius: var(--r-md); padding: 16px 20px; margin-bottom: 10px;
}
.row__k { min-width: 220px; font-weight: 700; color: var(--head); }
.row__k small { display: block; font-size: 13px; font-weight: 600; letter-spacing: .06em; text-transform: uppercase; color: var(--muted); margin-top: 4px; }
.row__v { flex: 1; min-width: 260px; font-size: 16px; }
.hint { margin-top: 10px; padding: 10px 12px; border-radius: var(--r-sm); background: var(--ok-bg); color: var(--ok-ink); font-size: 15px; }

ul.ticks { list-style: none; margin: 0; padding: 0; }
ul.ticks li { position: relative; padding-left: 28px; margin-bottom: 10px; }
ul.ticks li::before {
  content: "✓"; position: absolute; left: 0; top: 0;
  color: var(--accent-600); font-weight: 700;
}

.switch { display: inline-flex; background: var(--page); border: 1px solid var(--line); border-radius: var(--r-md); padding: 4px; gap: 4px; }
.switch button {
  border: 0; background: none; cursor: pointer; border-radius: var(--r-sm);
  padding: 10px 18px; font-size: 15px; font-weight: 700; color: var(--muted);
}
.switch button[aria-pressed="true"] { background: var(--card); color: var(--head); box-shadow: var(--shadow); }

.btn {
  display: inline-flex; align-items: center; gap: 8px; cursor: pointer;
  background: var(--accent-600); color: #fff; border: 1px solid var(--accent-600);
  border-radius: var(--r-sm); padding: 12px 20px; font-size: 16px; font-weight: 700;
}
.btn:hover { background: var(--accent-700); border-color: var(--accent-700); }
.btn:disabled { opacity: .45; cursor: not-allowed; }
.btn--dark { background: var(--head); border-color: var(--head); }
.btn--dark:hover { background: #000; border-color: #000; }
.btn--ghost { background: var(--card); color: var(--head); border-color: var(--line-2); }
.btn--ghost:hover { background: var(--page); }

label.f { display: block; margin-bottom: 20px; }
label.f > span { display: block; font-weight: 700; color: var(--head); margin-bottom: 8px; }
textarea, input[type=text] {
  width: 100%; font: 400 16px/1.6 var(--sans); color: var(--ink);
  background: var(--card); border: 1px solid var(--line-2);
  border-radius: var(--r-sm); padding: 12px 14px; resize: vertical;
}
textarea::placeholder, input::placeholder { color: #4b5563; }
:focus-visible { outline: 2px solid var(--accent-600); outline-offset: 2px; }

/* Layers diagram (kept from the app: activity layer is the highlighted one) */
.layer {
  display: flex; gap: 22px; flex-wrap: wrap; align-items: baseline;
  background: var(--card); border: 1px solid var(--line);
  border-radius: var(--r-md); padding: 16px 20px; margin-bottom: 10px;
}
.layer--on { background: var(--accent-50); border-color: var(--accent-500); }
.layer b { min-width: 200px; font-size: 17px; color: var(--head); }
.layer b small { display: block; font-size: 14px; font-weight: 400; color: var(--muted); margin-top: 3px; }
.layer span { flex: 1; min-width: 250px; font-size: 16px; }

/* Steps */
.steps { display: flex; gap: 24px; flex-wrap: wrap; align-items: flex-start; }
.steps__list { flex: 1 1 280px; }
.steps__list button {
  display: block; width: 100%; text-align: left; cursor: pointer;
  background: var(--card); border: 1px solid var(--line); border-radius: var(--r-md);
  padding: 14px 16px; margin-bottom: 8px; font-size: 16px; color: var(--ink);
}
.steps__list button b { display: block; font-size: 12px; font-weight: 700; letter-spacing: .1em; text-transform: uppercase; color: var(--muted); margin-bottom: 4px; }
.steps__list button[aria-pressed="true"] { background: var(--accent-600); border-color: var(--accent-600); color: #fff; }
.steps__list button[aria-pressed="true"] b { color: rgba(255,255,255,.75); }
.steps__panel { flex: 2 1 360px; }

/* Quiz */
.quiz { background: var(--card); border: 1px solid var(--line); border-radius: var(--r-lg); padding: 26px; box-shadow: var(--shadow); }
.quiz__top { display: flex; justify-content: space-between; align-items: center; gap: 14px; flex-wrap: wrap; margin-bottom: 14px; }
.quiz__count { font-size: 14px; font-weight: 600; color: var(--muted); }
.meter { height: 6px; background: var(--page); border-radius: 3px; overflow: hidden; margin-bottom: 22px; }
.meter i { display: block; height: 100%; background: var(--accent-600); transition: width .3s ease; }
.scenario {
  background: var(--page); border-left: 4px solid var(--accent-500);
  border-radius: 0 var(--r-sm) var(--r-sm) 0; padding: 14px 18px;
  font-size: 17px; margin-bottom: 18px;
}
.qtext { font-weight: 700; color: var(--head); margin-bottom: 16px; }
.opt {
  display: flex; align-items: center; gap: 14px; width: 100%; text-align: left;
  cursor: pointer; background: var(--card); border: 1px solid var(--line);
  border-radius: var(--r-md); padding: 16px 18px; margin-bottom: 10px;
  font-size: 16px; color: var(--ink);
}
.opt:hover:not(:disabled) { background: var(--page); }
.opt .mark { width: 22px; height: 22px; border-radius: 50%; border: 2px solid var(--line-2); flex: none; display: grid; place-items: center; font-size: 13px; color: #fff; }
.opt[aria-pressed="true"] { background: var(--accent-50); border-color: var(--accent-600); }
.opt[aria-pressed="true"] .mark { border-color: var(--accent-600); border-width: 6px; }
.opt[data-s="right"] { background: var(--ok-bg); border-color: var(--ok-line); }
.opt[data-s="right"] .mark { background: #10b981; border-color: #10b981; }
.opt[data-s="wrong"] { background: var(--no-bg); border-color: var(--no-line); }
.opt[data-s="wrong"] .mark { background: #ef4444; border-color: #ef4444; }
.opt[data-s="mute"] { opacity: .55; }
.opt:disabled { cursor: default; }
.verdict { margin-top: 18px; padding: 16px 18px; border-radius: var(--r-md); border: 1px solid; }
.verdict--ok { background: var(--ok-bg); border-color: var(--ok-line); color: var(--ok-ink); }
.verdict--no { background: var(--no-bg); border-color: var(--no-line); color: var(--no-ink); }
.verdict b { display: block; margin-bottom: 6px; color: inherit; }
.result { text-align: center; padding: 26px 10px; }
.result .ring {
  width: 96px; height: 96px; border-radius: 50%; margin: 0 auto 18px;
  display: grid; place-items: center; background: var(--accent-50);
  color: var(--accent-700); font-size: 26px; font-weight: 700;
}

/* Case study tabs */
.chips { display: flex; gap: 8px; flex-wrap: wrap; margin-bottom: 22px; }
.chips button {
  cursor: pointer; background: var(--card); border: 1px solid var(--line);
  border-radius: var(--r-sm); padding: 9px 14px; font-size: 15px; font-weight: 600; color: var(--ink);
}
.chips button[aria-pressed="true"] { background: var(--accent-600); border-color: var(--accent-600); color: #fff; }

.speaker { display: flex; gap: 28px; flex-wrap: wrap; align-items: flex-start; }
.speaker > img { width: 128px; height: 128px; border-radius: 50%; object-fit: cover; border: 4px solid var(--accent-500); flex: none; }
.awards { display: grid; grid-template-columns: repeat(2, minmax(0,1fr)); gap: 12px; margin-top: 16px; }
.awards div { background: rgba(255,255,255,.1); border: 1px solid rgba(255,255,255,.14); border-radius: var(--r-sm); padding: 12px 14px; }
.awards b { display: block; font-size: 15px; color: #fff; }
.awards small { font-size: 13.5px; color: var(--on-dark); }

.fade { animation: fade .25s ease both; }
@keyframes fade { from { opacity: 0; transform: translateY(8px); } to { opacity: 1; transform: none; } }
@media (prefers-reduced-motion: reduce) { * { animation-duration: .001ms !important; transition-duration: .001ms !important; } }

@media (max-width: 940px) {
  .g2, .g3, .awards { grid-template-columns: 1fr; }
  .body { display: block; }

  /* Header stacks: title row, then the meta row underneath. */
  .topbar { flex-wrap: wrap; padding: 12px 16px; }
  .topbar__right { width: 100%; margin-left: 0; justify-content: space-between; gap: 12px; }

  /* Sidebar becomes a contained horizontal scroller. The clip on .side is what
     stops the wide tab list pushing the page sideways. */
  .side {
    width: auto; height: auto; position: static; overflow: hidden; min-width: 0;
    border-right: 0; border-bottom: 1px solid var(--line);
    padding: 12px 0 12px 16px;
  }
  .side h2, .note { display: none; }
  /* min-width:0 is required: without it the flex item refuses to shrink below
     its content width and the wide tab list pushes the whole page sideways. */
  .side nav { min-width: 0; overflow-x: auto; -webkit-overflow-scrolling: touch; padding: 0 16px 0 0; }
  .side ol { display: flex; gap: 8px; width: max-content; }
  .tab { white-space: nowrap; border: 1px solid var(--line); margin-bottom: 0; }

  main { padding: 24px 16px 60px; }
  .row__k, .row__v, .layer b, .layer span { min-width: 0; }
  .card, .row, .layer { overflow-wrap: anywhere; }
}
</style>
</head>
<body>
<div class="app">

  <header class="topbar">
    <div class="topbar__mark" aria-hidden="true">&#9782;</div>
    <div>
      <h1 class="topbar__title">Designing Meaningful Teaching Materials</h1>
      <div class="topbar__sub">Prof. Ts. Dr. Zurina Zainal Abidin</div>
    </div>
    <div class="topbar__right">
      <div class="stat"><span>Duration</span><b class="mono">120 Min</b></div>
      <button class="themeBtn" id="theme" aria-label="Switch colour theme"><i></i><span id="themeName">Blue</span></button>
      <div class="stat"><span>Modules</span><b>8</b></div>
    </div>
  </header>

  <div class="body">
    <aside class="side">
      <h2>Workshop Structure</h2>
      <nav aria-label="Workshop sections"><ol id="tabs"></ol></nav>
      <div class="note">
        <div class="note__head">
          <img src="data:image/jpeg;base64,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" alt="Prof. Ts. Dr. Zurina Zainal Abidin">
          <span>Speaker Note</span>
        </div>
        <p>“Innovation is simply solving a learning problem in a new or more effective way.”</p>
      </div>
    </aside>

    <main><div class="view" id="view" role="region" aria-live="polite"></div></main>
  </div>

  <footer class="foot">
    <span>Speaker: Prof. Ts. Dr. Zurina Zainal Abidin &bull; KAPP Workshop</span>
    <span>&copy; 2026 University Innovation Lab</span>
  </footer>
</div>

<script>
"use strict";

/* ===========================================================================
   DATA — all workshop content in one place
   ========================================================================= */
const PORTRAIT = "data:image/jpeg;base64,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";

const PHILOSOPHIES = [
  ["Connectivity, Compassion, and Empathy", "Teaching without knowing your students is like teaching without a soul. Build rapport, memorize names, and create memorable moments."],
  ["Do-Sense-Feel (Multisensory)", "Make use of human senses (visual, auditory, kinesthetic, tactile) to create the 'feel' or emotions that stimulate greater cognitive development."],
  ["Togetherness and Empowerment", "Adopt a growth mindset and build authentic mentorships to help students prioritize learning. Your authentic relationship empowers them."]
];

const TESTS = [
  ["It is intentional", "It answers a problem you actually identified in your own course — not a trend, and not a call for proposals.", "Chasing a tool because everyone is talking about it."],
  ["It changes what students do", "Their cognitive process differs. What happens inside the student's head is not the same as before.", "Same task, new device. The thinking is unchanged."],
  ["It is evidenced", "You can show that something improved — marks, attainment, competency, or transfer to a new context.", "Students said they enjoyed it, and nothing else was measured."]
];

const LAYERS = [
  ["Theory", "The account of how people learn", "Constructivism, active learning, multisensory learning", false],
  ["Pedagogical approach", "The named model you are drawing on", "PBL, flipped classroom, experiential, collaborative, challenge-based", false],
  ["Learning activity", "The specific thing students actually do", "Build the tower, dry the sample, trace the line on the real plant", true],
  ["Tool", "What you deliver it with", "Kahoot, video, Visio, a rubric, an AI model", false]
];

const DRIVERS = [
  "Students disengaged, or passing without understanding",
  "One Course Outcome consistently under-attained, year after year",
  "Resource shortage — no demonstrators, no equipment, no time",
  "Class size has defeated the method that used to work",
  "A gap between what you teach and what industry now does",
  "Assessment integrity — plagiarism, and now generative AI",
  "Accreditation shift — new EAC definitions, new WK / WP / EA"
];

const TYPES = [
  ["Curriculum &amp; content", "What is taught, the sequence, and its currency with industry practice."],
  ["Pedagogy &amp; delivery", "How it is taught — flipped, PBL, collaborative, immersive."],
  ["Assessment", "What is graded and how. The highest-leverage type, and the one lecturers assume they may not touch."],
  ["Learning environment", "Lab, pilot plant, site visit, outdoor, virtual, or the industry floor."],
  ["Technology-enabled", "Only counts as innovation when the tool changes the activity, not just the delivery."],
  ["Learning support", "Peer teaching, mentoring, self-access material, video demos."]
];

const PEDAGOGIES = [
  ["Constructivism &amp; Active Learning", "Students construct understanding rather than receive it.", "An open-ended problem with no obvious solution; the lecturer facilitates instead of answering.", "Students derive the design approach themselves before you show the standard method."],
  ["Flipped Classroom (Kelas Berbalik)", "Direct instruction moves out; class time becomes the hard part.", "Material consumed at home, contact hours spent on challenge and collaboration.", "P&amp;ID symbols compiled as pre-work, then a three-hour tracing challenge in class."],
  ["Experiential / Hands-On", "Learning through concrete experience, then reflection (Kolb's cycle).", "Students do the real thing under professional constraints, then analyse what happened.", "Drying apple samples, collecting data, and defending the rate curve."],
  ["Multisensory Pedagogy", "Multiple senses at once build richer cognitive connections.", "Something to see, touch, hear or smell — not a description of it.", "A real rose lets one smell its sweetness and feel the petals; an image cannot."],
  ["Collaborative &amp; Problem-Based Learning", "Genuine interdependence, where the task cannot be done alone.", "Small teams, a shared deliverable, and individual accountability within it.", "Groups of four building a free-standing Power Tower against a specification."],
  ["Challenge-Based Immersive Learning", "A real, bounded challenge in an authentic setting drives the learning.", "Time pressure, real equipment, and a problem with a right answer they must find.", "Tracing the flow on actual Boiler Drum Control Equipment in the pilot plant."],
  ["Assessment-as-Learning", "The assessment produces learning while it measures it.", "A test students would still benefit from even if it were ungraded.", "An experiment-based continuous assessment replacing the paper test."]
];

const MACRO = [
  ["Curriculum &amp; course syllabus", "Faculty / Senate", "Approved at faculty level and locked for the accreditation cycle.", "You cannot remove a topic — but the depth, sequence and framing within it are yours."],
  ["CO–PO mapping", "Programme committee", "Each Course Outcome is formally mapped to Programme Outcomes and taxonomy levels.", "The mapping is fixed; how you evidence attainment against it is not."],
  ["EAC requirements (WK / WP / EA)", "Engineering Accreditation Council", "Knowledge Profiles, Complex Problem attributes and Engineering Activities are externally defined.", "You choose which activities demonstrate them — and most courses under-use EA."],
  ["Credit hours &amp; SLT", "University", "Student Learning Time is fixed by the credit structure.", "The split between lecture, tutorial and independent learning within it is negotiable."],
  ["Timetable &amp; room allocation", "Faculty administration", "Slots and venues are centrally scheduled across programmes.", "Book a lab, plant or outdoor space early and the venue stops being a constraint."],
  ["Student list &amp; cohort size", "Registrar", "You teach whoever enrols, in whatever number.", "Grouping, pairing and roles within the cohort are entirely your design."]
];

const MICRO = [
  ["Lecture notes &amp; teaching materials", "Everything students read, watch or handle is authored by you.", "Replace a static diagram with a video demo, or a real object they can handle."],
  ["Delivery mode &amp; platform", "How the content reaches them — and whether they are passive while it does.", "Flip the lecture, run a space lecture, or bring in an industry speaker."],
  ["Learning activities", "The single highest-value thing you control: what students actually DO.", "Build a tower, dry a sample, trace a live line on the pilot plant."],
  ["Assessment design &amp; format", "Within the approved weighting, the FORM of the assessment is yours.", "An experiment-based test instead of a paper test, at the same 15%."],
  ["Sequencing within a topic", "What comes first changes what students are ready to understand.", "Let them fail at the problem first, then teach the method they needed."],
  ["Feedback &amp; classroom climate", "How safe it feels to be wrong determines how much thinking happens out loud.", "Live polling that redirects your teaching instead of just scoring them."]
];

const CYCLE = [
  ["Identify the Problem", "What is actually going wrong in your course?"],
  ["Diagnose the Cause", "Why is it happening — beyond the symptom?"],
  ["Choose a Pedagogical Construct", "Name the model: flipped classroom, PBL, experiential learning."],
  ["Design the Activity", "What will the students actually do?"],
  ["Build the Evidence Plan", "Decide what data you collect BEFORE you run it."]
];

const CASES = [
  { tab: "Video demos", title: "Biochemical Engineering laboratory aided by video demo",
    context: "Biochemical Engineering, 2015 &bull; Funded by GIPP UPM",
    rows: [
      ["Problem", "A shortage of funding to hire lab demonstrators disrupted the smooth running of the laboratory — several rigs run at once and all need supervision."],
      ["Objective", "Reduce dependency on demonstrators and technicians, and maintain the sustainability of the lab courses."],
      ["Innovation", "Produce laboratory video demos of the procedures to assist student learning."],
      ["Method", "Students conducted experiments with and without the assistance of video demonstrations."],
      ["Assessment", "Lab reports and student total assignment marks."],
      ["Impact", "Over 80% agreed the videos enhanced understanding (cognitive), helped them visualise the steps (psychomotor), and improved motivation (affective)."]
    ], output: "GIPP grant &bull; 2 copyrights &bull; 1 conference paper &bull; 1 silver medal" },
  { tab: "Power Tower", title: "Teamwork and real-life application in CAD",
    context: "Computer Aided Drawing",
    rows: [
      ["Problem", "Assignments were purely drawings. The routine creates boredom and has little relation to real-life application."],
      ["Objective", "Enhance the learning experience through experiential, collaborative STEM activity tied to real applications."],
      ["Innovation", "STEM-based hands-on activity added, giving a genuine basis for teamwork assessment."],
      ["Method", "Groups of four, three-hour session, building a free-standing Power Tower from a golf ball, 15 pipe cleaners and 3 straws."],
      ["Assessment", "Prototype, teamwork and reflection analysis, graded against specified Programme Outcomes."],
      ["Impact", "100% found it fun, 98% improved critical thinking, 96% analytical skills, 98% teamwork."]
    ], output: "1 bronze medal in PICTL" },
  { tab: "Comprehensive assessment", title: "Comprehensive CAD assessment",
    context: "Computer Aided Drawing &bull; Tackling plagiarism",
    rows: [
      ["Problem", "Similarities in submitted drawings raised plagiarism concerns, and grading the drawing alone could not verify actual hands-on competency."],
      ["Objective", "Tackle plagiarism and introduce a standard that evaluates competency, not just the artefact."],
      ["Innovation", "A comprehensive assessment combining cognitive (drawing) and psychomotor (live demonstration) components."],
      ["Method", "Drawing assignment 90%, plus a hands-on demonstration worth 10%, evaluated by the lecturer against a rubric."],
      ["Assessment", "100% total: 90% drawing, 10% psychomotor hands-on."],
      ["Impact", "Eradicated the plagiarism loophole. Students agreed the combination better reflected their real skills."]
    ], output: "1 gold medal in PICTL" },
  { tab: "Experiment as test", title: "Experiment-based assessment replacing the classroom test",
    context: "Physical Separation",
    rows: [
      ["Problem", "Typical assessment was classroom-based, paper-based, individual and cognitive — providing no meaningful learning experience."],
      ["Objective", "Enhance the learning experience through assessment itself, using an experiential and collaborative approach."],
      ["Innovation", "The test became the experiment."],
      ["Method", "Pairs over a three-hour session, drying apple samples and calculating moisture loss."],
      ["Assessment", "Experiment data collected, analysed, and engineering calculations graded."],
      ["Impact", "Over 75% strongly agreed that working in pairs let them work and learn more effectively, with better visualisation and critical thinking."]
    ], output: "A test that teaches while it measures" },
  { tab: "P&amp;ID tracing", title: "Industrial application — tracing line activities",
    context: "Computer Aided Drawing &bull; Industrial application",
    rows: [
      ["Problem", "P&amp;ID diagrams are widely used in industry, complicated to read, and must be related back to the actual plant."],
      ["Objective", "Expose students to reading a P&amp;ID against a real plant, as it is used in industry."],
      ["Innovation", "Challenge-based tracing line activities using actual Boiler Drum Control Equipment."],
      ["Method", "A 3-in-1 PID Maze: symbol compilation as flipped pre-work, a three-hour tracing challenge, then a mystery-unravel presentation of the flow logic."],
      ["Assessment", "Drawing portfolio (cognitive), quiz, and tracing line activities (psychomotor)."],
      ["Impact", "Highly interactive, work-related knowledge replicating a real plant, with commercialisation potential for TVET training."]
    ], output: "1 gold medal in PICTL 2020" }
];

const QUICKWINS = [
  ["2-hour Monologue Lecture", "Microlearning &amp; Polling: break lectures into 15-minute chunks separated by a quick interactive quiz.", "Passive listening → active recall and engagement."],
  ["Paper-based Quiz", "Experiment-Based Assessment: students dry an apple and calculate moisture loss instead of answering a test paper.", "Rote memorisation → experiential learning and application."],
  ["Standard Written Essay", "Video Pitch: students record a 60-second explanation of a complex concept.", "Information regurgitation → synthesis and communication."],
  ["100% Final Product Grade", "Process-Oriented Grading: assess the drafts, teamwork and physical prototype alongside the final drawing.", "Outcome-focused → process and critical thinking focused."]
];

const INNOVATION_QUIZ = [
  { s: "You move your weekly paper quiz into Kahoot. Same questions, same timing, same follow-up.", q: "Innovation, or not?",
    o: ["Innovation — it uses modern technology", "Substitution — the tool changed, the thinking did not", "Innovation — students enjoy it more", "Not innovation — because it is free to run"], a: 1,
    e: "The quiz is identical; only the delivery device changed. Enjoyment is not evidence of learning. This is substitution at the tool layer." },
  { s: "You use the same Kahoot — but when you see 60% choose the wrong option, you stop and reteach that concept for the next twenty minutes.", q: "Innovation, or not?",
    o: ["Substitution — it is still just Kahoot", "Innovation — the live data now redirects the teaching", "Not innovation — the tool is unchanged from before", "Innovation — because it saves marking time"], a: 1,
    e: "Same tool as the previous question, different answer. The feedback loop changed what happens in the room and what students then do. Innovation reached the activity layer." },
  { s: "You record all your lectures so students can rewatch them before the final exam. Class time continues exactly as before.", q: "Innovation, or not?",
    o: ["Innovation — it is a flipped classroom", "Substitution — access improved, the learning process did not", "Innovation — it supports different learning styles", "Not innovation — recordings reduce attendance"], a: 1,
    e: "This is augmentation, and it is genuinely useful. But flipping requires class time to be repurposed for challenge and collaboration. Nothing about the students' cognitive work changed." },
  { s: "You replace the written classroom test with an experiment that pairs of students design, run, and defend with their own calculations.", q: "Innovation, or not?",
    o: ["Substitution — it is still just a test", "Innovation — the assessment now produces the learning", "Not innovation — because no technology is involved", "Innovation — because it is harder to mark"], a: 1,
    e: "Assessment-as-learning. Students now analyse, decide and defend rather than recall. Note that no technology appears anywhere — innovation does not require it." },
  { s: "You redesign an activity, students tell you they loved it, and you write it up for a conference. You collected no marks data and had no comparison cohort.", q: "Does it qualify as an evidenced innovation?",
    o: ["Yes — student feedback is valid evidence", "Not yet — it passes tests one and two but fails the evidence test", "Yes — conference acceptance proves the impact", "No — the activity itself was not innovative"], a: 1,
    e: "The design may be excellent. But satisfaction is the weakest level of evidence, and students often rate the lecture they enjoyed above the activity that taught them more. Plan the data before you run it." },
  { s: "You ask AI to generate three times as many practice questions and upload them all to the course page.", q: "Innovation, or not?",
    o: ["Innovation — AI is involved", "Substitution — more of the same task, produced faster", "Not innovation — because AI made it, not you", "Innovation — variety prevents cheating"], a: 1,
    e: "Volume is not pedagogy. This would become innovation if the extra questions enabled something new — mastery-based retries until competence, for example — because then what students do would change." },
  { s: "Students build a physical prototype, then compare it against the CAD drawing they produced earlier and explain every difference.", q: "Innovation, or not?",
    o: ["Substitution — drawing was already part of the course", "Innovation — comparison and reflection are new cognitive work", "Not innovation — building models is a very old method", "Innovation — because students find it fun"], a: 1,
    e: "The prototype alone would be an activity swap. The comparison step forces students to confront the gap between plan and reality — that reflection is what makes it Kolb's experiential cycle." }
];

const PEDAGOGY_QUIZ = [
  { s: "Students compile P&amp;ID symbols as pre-work at home. The entire three-hour contact session is then spent solving a tracing maze in teams.", q: "Which pedagogy is this?",
    o: ["Multisensory Pedagogy", "Flipped Classroom", "Constructivism", "Assessment-as-Learning"], a: 1,
    e: "Direct instruction moved out of the classroom, and contact time was repurposed for the difficult, collaborative work. That is the defining structure of a flipped classroom." },
  { s: "Pairs of students dry apple samples in an oven, weigh them at intervals, plot the drying curve, and calculate the critical moisture content.", q: "Which pedagogy is this?",
    o: ["Flipped Classroom", "Experiential / Hands-On", "Direct Instruction", "Peer Instruction"], a: 1,
    e: "Concrete experience followed by analysis and reflection — Kolb's experiential cycle. Students learn the concept by generating the data themselves rather than being shown it." },
  { s: "You bring real roses into class so students can smell the sweetness and feel the petals, rather than showing a photograph on a slide.", q: "Which pedagogy is this?",
    o: ["Multisensory Pedagogy", "Experiential Learning", "Constructivism", "Challenge-Based Learning"], a: 0,
    e: "Multisensory pedagogy engages several senses at once to build richer cognitive connections. The Do-Sense-Feel philosophy: emotion and sensation stimulate deeper cognitive development." },
  { s: "Groups of four are given one golf ball, fifteen pipe cleaners and three straws, and must build the tallest free-standing tower to a specification in ten minutes.", q: "Which pedagogy is this?",
    o: ["Direct Instruction", "Collaborative &amp; Problem-Based Learning", "Flipped Classroom", "Multisensory Pedagogy"], a: 1,
    e: "A shared deliverable that genuinely cannot be produced alone, under constraints, with individual accountability inside the team. It also carries an experiential reflection stage." },
  { s: "You pose an open-ended design problem with no obvious solution. You refuse to give the answer, and instead ask questions that help students build their own approach.", q: "Which pedagogy is this?",
    o: ["Constructivism &amp; Active Learning", "Assessment-as-Learning", "Experiential Learning", "Flipped Classroom"], a: 0,
    e: "Students construct understanding rather than receive it, with the lecturer as facilitator. The withholding of the answer is the pedagogical move, not an omission." },
  { s: "Students go into the pilot plant and must trace the actual flow path on live Boiler Drum Control Equipment to match it against the diagram, against the clock.", q: "Which pedagogy is this?",
    o: ["Multisensory Pedagogy", "Challenge-Based Immersive Learning", "Direct Instruction", "Peer Assessment"], a: 1,
    e: "A real, bounded challenge in an authentic industrial setting, with time pressure and a findable right answer. Immersion in the real environment separates this from a classroom exercise." },
  { s: "The continuous assessment is itself the experiment. Students would still gain the understanding even if the task carried no marks at all.", q: "Which pedagogy is this?",
    o: ["Summative Testing", "Assessment-as-Learning", "Flipped Classroom", "Constructivism"], a: 1,
    e: "The ungraded-value criterion: if students would still learn from it without marks, the assessment is producing learning rather than only measuring it." }
];

const SINGLE = {
  method: { q: "Which elements are 'Micro Level' — the things you can modify?",
    o: ["Course syllabus and timetable", "Student list and curriculum", "Delivery methods and assessments", "Programme Outcomes (PO)"], a: 2,
    e: "Macro-level items such as the syllabus and timetable are hard to change. Micro-level items — delivery methods, assessments, teaching materials — are where you have full control to innovate." },
  cases: { q: "Why is a comprehensive assessment (90% drawing + 10% psychomotor demonstration) effective for software-based assignments?",
    o: ["It is easier for the lecturer to grade.", "It allows students to finish the test faster.", "It determines actual hands-on competency and eradicates plagiarism.", "It relies solely on cognitive recall."], a: 2,
    e: "Adding a live, hands-on component ensures the student actually possesses the competency to perform the task, which helps eliminate plagiarism in submitted work." },
  sotl: { q: "What is the primary goal of the Scholarship of Teaching and Learning (SoTL)?",
    o: ["To publish textbooks for university students", "To systematically investigate student learning to improve teaching and share findings", "To apply for more research grants in engineering", "To evaluate other lecturers' performance"], a: 1,
    e: "SoTL involves rigorous inquiry into student learning, using evidence to improve teaching practice, and sharing those findings publicly." },
  summary: { q: "Which of the following is a good tip for sustaining motivation throughout a 14-week semester?",
    o: ["Always follow an extremely strict and unchangeable teaching plan.", "Grade all assignments in one large batch at the end of the semester.", "Break down the work into small tasks and set realistic targets (e.g. mark 10 per day).", "Avoid asking for student opinions until the final course evaluation."], a: 2,
    e: "Breaking work into smaller, manageable tasks helps prevent burnout and sustains motivation throughout the semester." }
};

const EVIDENCE = [
  ["Students said they enjoyed it", "Convinces nobody."],
  ["Students said they learned more", "Self-report. Better, still weak."],
  ["Their performance on the task improved", "Now you have something."],
  ["CO attainment improved against a prior cohort", "This is publishable."],
  ["It transferred to another context", "The strongest claim, and the rarest."]
];

const ETHICS = [
  ["Consent", "Students must know their data may be used, and be free to decline without penalty."],
  ["Anonymity", "No names, no matric numbers, no identifiable photographs in anything you publish."],
  ["Ethics approval", "If you intend to publish, obtain it before you collect — not when a reviewer asks."],
  ["No cohort disadvantaged", "A comparison group cannot be given a worse education to prove your point."]
];

const MOTIVATION = [
  ["Dynamic Teaching Plan", "Be resilient and adaptable to change. Do not let unexpected disruptions derail your semester."],
  ["Break Down Tasks", "Set realistic targets suited to your capacity — marking 10 assignments a day — to avoid procrastination."],
  ["Combine Tasks", "Fill in grades in the system while simultaneously ticking e-attendance."],
  ["Listen to Students", "Ask them directly. Negotiate win-win solutions and run a student assessment at the end."],
  ["Keep Passion Fueled", "Attend education conferences, workshops and competitions, and work together with colleagues."],
  ["Follow Current Trends", "Adapt your delivery to what students actually use — IT, media, or short-form video."]
];

/* ===========================================================================
   HELPERS
   ========================================================================= */
const h = (s, ...v) => s.reduce((o, str, i) => o + str + (v[i] ?? ''), '');
const map = (arr, fn) => arr.map(fn).join('');
const pad = n => String(n).padStart(2, '0');

/* ===========================================================================
   VIEWS
   ========================================================================= */
const views = {};

views.welcome = () => h`
  <section>
    <div class="card">
      <span class="pill pill--accent">Workshop Module</span>
      <h2 class="h" style="font-size:32px;margin:16px 0 14px">Kursus Asas Pengajaran dan Pembelajaran (KAPP)</h2>
      <p class="lede">Welcome to the interactive learning module for new university lecturers. This platform
      contains the core concepts, case studies and activities for our session on innovation in teaching and learning.</p>
      <h4 class="h" style="margin:24px 0 12px">Learning Outcomes</h4>
      <ul class="ticks">
        <li><strong>Understand innovation:</strong> learn what true educational innovation means beyond just using technology.</li>
        <li><strong>Apply frameworks:</strong> use the design cycle to solve real classroom challenges.</li>
        <li><strong>Explore case studies:</strong> review proven examples of successful teaching innovations.</li>
      </ul>
    </div>
  </section>

  <section>
    <div class="dark">
      <div class="speaker">
        <img src="${PORTRAIT}" alt="Prof. Ts. Dr. Zurina Zainal Abidin">
        <div style="flex:1;min-width:300px">
          <h3 class="h" style="font-size:24px">Prof. Ts. Dr. Zurina Zainal Abidin</h3>
          <div style="font-size:14px;font-weight:700;letter-spacing:.06em;text-transform:uppercase;color:#a5b4fc;margin:8px 0 16px">
            Department of Chemical and Environmental Engineering, UPM</div>
          <p>A passionate educator and researcher dedicated to driving innovation in teaching and learning.
          Prof. Zurina believes in the Do-Sense-Feel philosophy to stimulate greater cognitive development,
          and empowers students through experiential learning.</p>
          <h4 class="h" style="font-size:16px;margin:20px 0 0">Awards &amp; Recognitions</h4>
          <div class="awards">
            <div><b>Anugerah Akademik Negara</b><small>Finalist 2025 (Teaching, Eng. Cluster)</small></div>
            <div><b>Vice Chancellor Fellowship Award</b><small>AFNC 2021 (Teaching Category)</small></div>
            <div><b>Top World 2% Scientist</b><small>Elsevier BV &amp; Stanford University (2022–2023)</small></div>
            <div><b>SEARCA Professorial Chair</b><small>Awarded for 2025–2026</small></div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <section>
    <h2 class="h">Teaching in a VUCA World</h2>
    <p class="lede">We are teaching in a world characterised by <strong>Volatility, Uncertainty, Complexity
    and Ambiguity</strong>. Before any method or tool, you need a philosophy you can be comfortable
    inhabiting — one that reflects who you actually are.</p>
    <div style="margin-top:16px;background:var(--warn-bg);border-left:4px solid var(--warn-line);border-radius:0 8px 8px 0;padding:14px 18px">
      <strong style="color:var(--head)">Adopt a consistent teaching philosophy where you can be yourself. Be authentic.</strong>
    </div>
  </section>

  <section>
    <h3 class="h">Core Teaching Philosophies</h3>
    <p class="small" style="margin-bottom:20px">These three run underneath every case study later in this workshop.</p>
    <div class="grid g3">
      ${map(PHILOSOPHIES, ([t, d], i) => h`
        <div class="card topline">
          <div class="dot" style="margin-bottom:14px">${i + 1}</div>
          <h4 class="h">${t}</h4>
          <p class="small">${d}</p>
        </div>`)}
    </div>
  </section>

  <section>
    <div class="dark">
      <h3 class="h" style="font-size:20px">Not knowing your student is like teaching without a soul</h3>
      <p style="font-size:15px">Palmer (2003). An authentic relationship between teacher and student helps
      students prioritise learning and succeed (Prewett et al., 2019).</p>
      <div class="grid g2" style="gap:10px;margin-top:16px">
        ${map(["Build rapport", "Memorise names", "Memorable moments", "Freedom of speech"],
          t => h`<div style="background:rgba(255,255,255,.1);border:1px solid rgba(255,255,255,.14);border-radius:8px;padding:12px;font-weight:700;text-align:center">${t}</div>`)}
      </div>
    </div>
  </section>

  <section>
    <div class="card">
      <h3 class="h">Reflect: does your philosophy show up in your classroom?</h3>
      <div style="margin-top:18px">
        ${map([
          ["I know my students", "I can name most of them and I know what they struggle with."],
          ["They can sense my presence", "They would say I am present and invested, not just delivering."],
          ["I am being myself", "My teaching reflects who I actually am, not an imitation of someone else."]
        ], ([t, d]) => h`
          <label style="display:flex;gap:16px;align-items:flex-start;border:1px solid var(--line);border-radius:12px;padding:16px;margin-bottom:12px;cursor:pointer">
            <input type="checkbox" class="reflect" style="width:20px;height:20px;margin-top:3px;accent-color:var(--accent-600)">
            <span><strong>${t}</strong><br><span class="small">${d}</span></span>
          </label>`)}
      </div>
      <div id="reflectDone" hidden style="margin-top:8px;background:var(--ok-bg);border:1px solid var(--ok-line);color:var(--ok-ink);border-radius:12px;padding:16px;font-weight:600">
        That is the foundation. Innovation, pedagogy and assessment all sit on top of it.
      </div>
    </div>
  </section>`;

views.innovation = () => h`
  <section>
    <h2 class="h">What Innovation Actually Is</h2>
    <div class="navy">
      <p class="stmt">Innovation is a deliberate change in the learning process that produces a
      demonstrable improvement in learning.</p>
      <p class="sub">The biggest misconception is that it requires expensive technology. It does not.</p>
    </div>
  </section>

  <section>
    <h3 class="h">Three tests — all three must pass</h3>
    <p class="small" style="margin-bottom:20px">Novelty fails the third test. Technology usually fails the second.</p>
    <div class="grid g3">
      ${map(TESTS, ([t, d, f], i) => h`
        <div class="card">
          <div class="dot" style="margin-bottom:14px">${i + 1}</div>
          <h4 class="h">${t}</h4>
          <p class="small">${d}</p>
          <div style="background:var(--no-bg);border:1px solid var(--no-line);border-radius:8px;padding:10px 12px;font-size:14px;color:var(--no-ink)">
            <strong style="color:var(--no-ink)">Fails when:</strong> ${f}</div>
        </div>`)}
    </div>
  </section>

  <section>
    <h3 class="h">Where innovation lives: four layers</h3>
    <p class="small" style="margin-bottom:20px">Most claimed innovation sits at the bottom layer. It becomes
    pedagogical innovation when it reaches the activity layer.</p>
    ${map(LAYERS, ([n, s, e, on]) => h`
      <div class="layer ${on ? 'layer--on' : ''}">
        <b>${n}<small>${s}</small></b><span>${e}</span></div>`)}
    <div style="margin-top:16px;background:var(--head);color:#fff;border-radius:12px;padding:20px">
      <strong style="color:#fff;font-size:18px">If the students' thinking is unchanged, you innovated the tool — not the pedagogy.</strong>
    </div>
  </section>

  <section>
    <h3 class="h">Innovation answers a problem — usually a dull one</h3>
    <p class="small" style="margin-bottom:20px">Nobody innovates because they woke up inspired. They innovate because something broke.</p>
    <div class="grid g2" style="gap:12px">
      ${map(DRIVERS, (d, i) => h`
        <div class="card card--flat" style="display:flex;gap:14px;align-items:flex-start;padding:16px">
          <div class="dot" style="width:26px;height:26px;font-size:13px">${i + 1}</div>
          <span class="small">${d}</span></div>`)}
    </div>
  </section>

  <section>
    <h3 class="h">Six places innovation can happen</h3>
    <p class="small" style="margin-bottom:20px">Most lecturers imagine only the fifth. The third is where the leverage actually is.</p>
    <div class="grid g3">
      ${map(TYPES, ([t, d], i) => h`
        <div class="card ${i === 2 ? 'card--tint' : ''}">
          <h4 class="h" style="font-size:17px">${t}</h4>
          <p class="small">${d}</p></div>`)}
    </div>
  </section>

  <section>
    <h3 class="h">Guessing game: is it innovation?</h3>
    <p class="small" style="margin-bottom:20px">Seven scenarios. Decide before you read the explanation.</p>
    <div id="quizInnovation"></div>
  </section>`;

views.pedagogy = () => h`
  <section>
    <h2 class="h">High-Impact Pedagogies</h2>
    <p class="lede">A pedagogy is the named model underneath your activity. Naming it lets you find the
    literature, defend the design, and eventually publish it.</p>
    <div style="margin-top:16px;background:var(--accent-50);border-left:4px solid var(--accent-500);border-radius:0 8px 8px 0;padding:14px 18px">
      <span class="small">I ran these for years before I could name any of them. Naming them is what turned activities into papers.</span>
    </div>
  </section>

  <section>
    <div class="grid g2">
      ${map(PEDAGOGIES, ([n, p, l, e], i) => h`
        <div class="card topline">
          <div style="display:flex;justify-content:space-between;gap:12px;align-items:flex-start;margin-bottom:10px">
            <h4 class="h" style="font-size:19px;margin:0">${n}</h4>
            <span class="pill" style="background:var(--accent-100);color:var(--accent-700);flex:none">${pad(i + 1)}</span>
          </div>
          <p style="font-weight:700;color:var(--head);font-size:16px">${p}</p>
          <p class="small"><strong>Looks like:</strong> ${l}</p>
          <p class="small"><strong>For example:</strong> ${e}</p>
        </div>`)}
    </div>
  </section>

  <section>
    <div style="background:var(--head);color:#fff;border-radius:16px;padding:28px">
      <h3 class="h" style="color:#fff;font-size:20px">How to choose</h3>
      <p style="color:#cbd5e1;margin:0">Pick the construct first, then design the activity from it — not the reverse.
      An activity chosen first and justified afterwards is how you end up with something that looks
      innovative and teaches nothing.</p>
    </div>
  </section>

  <section>
    <h3 class="h">Name that pedagogy</h3>
    <p class="small" style="margin-bottom:20px">Seven classroom scenarios.</p>
    <div id="quizPedagogy"></div>
  </section>`;

views.method = () => h`
  <section>
    <h2 class="h">Method to Craft Innovation</h2>
    <div class="dark">
      <p style="font-size:19px;color:#fff;font-weight:600">Every course you teach has two layers. One is
      decided for you and locked for the accreditation cycle. The other is entirely yours, every single semester.</p>
      <p style="margin:14px 0 0">Innovation is impossible in the first layer and unavoidable in the second.
      Knowing which is which is the whole method.</p>
    </div>
  </section>

  <section>
    <h3 class="h">Know your two levels</h3>
    <p class="small" style="margin-bottom:20px">Junior lecturers exhaust themselves fighting the macro column.
    Switch between them and see exactly where your room to move is.</p>
    <div class="switch" role="group" aria-label="Level" style="margin-bottom:22px">
      <button data-level="macro" aria-pressed="true">MACRO — already fixed</button>
      <button data-level="micro" aria-pressed="false">MICRO — entirely yours</button>
    </div>
    <div id="levels"></div>
    <div class="grid g3" style="margin-top:20px">
      <div class="card" style="text-align:center"><div style="font-size:34px;font-weight:700;color:var(--muted)">6</div>
        <div class="small" style="font-weight:600">Macro items — fixed</div></div>
      <div class="card card--tint" style="text-align:center"><div style="font-size:34px;font-weight:700;color:var(--accent-600)">6</div>
        <div class="small" style="font-weight:600">Micro items — yours</div></div>
      <div style="background:var(--head);color:#fff;border-radius:16px;padding:24px;display:grid;place-items:center;text-align:center">
        <strong style="color:#fff">Start every innovation in the micro column.</strong></div>
    </div>
  </section>

  <section>
    <h3 class="h">Interactive: the 5-step design cycle</h3>
    <p class="small" style="margin-bottom:20px">Click through the steps to explore the process.</p>
    <div class="steps">
      <div class="steps__list">
        ${map(CYCLE, ([t], i) => h`<button data-step="${i}" aria-pressed="${i === 0}"><b>Step ${i + 1}</b>${t}</button>`)}
      </div>
      <div class="steps__panel"><div class="card" id="cyclePanel"></div></div>
    </div>
  </section>

  <section><div id="quizMethod"></div></section>`;

views.cases = () => h`
  <section>
    <h2 class="h">Assessment &amp; Case Studies</h2>
    <p class="lede">Five innovations that ran in real courses. Every one began with a problem, and every one
    collected its evidence the first time it ran.</p>
  </section>

  <section>
    <div class="chips" role="group" aria-label="Case studies">
      ${map(CASES, (c, i) => h`<button data-case="${i}" aria-pressed="${i === 0}">${i + 1}. ${c.tab}</button>`)}
    </div>
    <div id="casePanel"></div>
  </section>

  <section>
    <h3 class="h">Quick wins: traditional versus innovative</h3>
    <p class="small" style="margin-bottom:20px">Small swaps that change what students actually do.</p>
    ${map(QUICKWINS, ([a, b, c]) => h`
      <div class="row">
        <div class="row__k" style="color:var(--muted);font-weight:600">${a}</div>
        <div class="row__v"><strong>${b}</strong>
          <div class="small" style="margin-top:6px;color:var(--accent-700);font-weight:600">${c}</div></div>
      </div>`)}
  </section>

  <section><div id="quizCases"></div></section>`;

views.activities = () => h`
  <section>
    <h2 class="h">Session Activities</h2>
    <p class="lede">Two things you will build in this room today. Both rest on the same idea: AI has collapsed
    the cost of <em>making</em> teaching material, so the scarce skill is now deciding what is worth making.</p>
  </section>

  <section>
    <div class="grid g2">
      <button class="card actPick" data-act="tiktok" aria-pressed="true" style="text-align:left;cursor:pointer">
        <div style="display:flex;gap:12px;align-items:center;margin-bottom:10px">
          <span class="dot dot--solid">01</span>
          <span class="small" style="font-weight:700;text-transform:uppercase;letter-spacing:.06em">24 minutes</span>
        </div>
        <h4 class="h">The TikTok Challenge</h4>
        <p class="small" style="margin:0">Sixty seconds on the innovation you just designed</p>
      </button>
      <button class="card actPick" data-act="vibe" aria-pressed="false" style="text-align:left;cursor:pointer">
        <div style="display:flex;gap:12px;align-items:center;margin-bottom:10px">
          <span class="dot dot--solid">02</span>
          <span class="small" style="font-weight:700;text-transform:uppercase;letter-spacing:.06em">25 minutes</span>
        </div>
        <h4 class="h">The Vibe Coding Challenge</h4>
        <p class="small" style="margin:0">Build a small game that teaches one concept from your course</p>
      </button>
    </div>
  </section>

  <section id="actPanel"></section>`;

views.sotl = () => h`
  <section>
    <h2 class="h">Research Integration &amp; SoTL</h2>
    <div class="card">
      <p><strong>SoTL</strong> is the Scholarship of Teaching and Learning — a shift where teaching is treated
      not as a task but as a scholarly endeavour. You investigate your own classroom systematically, gather
      evidence of student learning, and share the findings publicly.</p>
      <ul class="ticks" style="margin-top:18px">
        <li><strong>Systematic inquiry:</strong> treating teaching problems like research questions.</li>
        <li><strong>Evidence-based:</strong> collecting robust data to evaluate the impact of an innovation.</li>
        <li><strong>Public sharing:</strong> publishing in conferences such as PICTL, or in journals.</li>
      </ul>
    </div>
  </section>

  <section>
    <h3 class="h">Evidence hierarchy</h3>
    <p class="small" style="margin-bottom:20px">Weakest to strongest. Most teaching reports stop at level one,
    and level one convinces nobody.</p>
    ${map(EVIDENCE, ([t, d], i) => h`
      <div class="row" ${i >= 3 ? 'style="background:var(--accent-50);border-color:var(--accent-100)"' : ''}>
        <div style="flex:none"><span class="dot ${i >= 3 ? 'dot--solid' : ''}">${i + 1}</span></div>
        <div class="row__v" style="font-weight:${i >= 3 ? '700' : '400'};color:var(--head)">${t}</div>
        <div class="small" style="min-width:210px;color:var(--muted)">${d}</div>
      </div>`)}
    <div style="margin-top:16px;background:var(--warn-bg);border:1px solid var(--warn-line);border-radius:12px;padding:18px">
      <strong style="color:var(--warn-ink)">Satisfaction is not learning.</strong>
      <span class="small" style="color:var(--warn-ink)"> Students often rate the lecture they enjoyed above the activity that taught them more.</span>
    </div>
  </section>

  <section>
    <h3 class="h">Ethics first</h3>
    <div class="grid g2">
      ${map(ETHICS, ([t, d]) => h`<div class="card"><h4 class="h" style="font-size:17px">${t}</h4><p class="small">${d}</p></div>`)}
    </div>
  </section>

  <section>
    <div class="dark">
      <h3 class="h" style="font-size:20px">One activity, many outputs</h3>
      <p>None of these were planned in advance. All of them were possible only because the data was collected
      the first time the activity ran.</p>
      <div style="display:flex;gap:10px;flex-wrap:wrap;margin-top:16px">
        ${map(["Teaching grant", "Conference paper", "Copyright", "Competition medal", "Award portfolio", "Book chapter"],
          o => h`<span style="background:rgba(255,255,255,.12);border:1px solid rgba(255,255,255,.16);padding:8px 14px;border-radius:8px;font-weight:600;font-size:15px">${o}</span>`)}
      </div>
    </div>
  </section>

  <section><div id="quizSotl"></div></section>`;

views.challenge = () => h`
  <section>
    <h2 class="h">The Challenge</h2>
    <p class="lede">Pick one problem in your syllabus today and draft the plan. Not a curriculum overhaul —
    one thing, written down now, while you still believe it is possible.</p>
  </section>

  <section>
    <div class="card">
      <label class="f"><span>1. Identify the problem</span>
        <textarea id="fProblem" rows="3" placeholder="What is actually going wrong in your course?"></textarea></label>
      <label class="f"><span>2. Choose a pedagogical construct</span>
        <input type="text" id="fConstruct" placeholder="e.g. Flipped Classroom, Project-Based Learning"></label>
      <label class="f"><span>3. Design the activity</span>
        <textarea id="fActivity" rows="3" placeholder="What will the students actually do?"></textarea></label>
      <label class="f"><span>4. Build the evidence plan</span>
        <input type="text" id="fEvidence" placeholder="What data will you collect, and in which week?"></label>
      <div style="display:flex;gap:14px;align-items:center;flex-wrap:wrap;border-top:1px solid var(--line);padding-top:20px">
        <button class="btn" id="planBtn" disabled>Download my plan</button>
        <span class="small" id="planHint">Complete at least the problem and the activity.</span>
      </div>
    </div>
  </section>

  <section>
    <div style="background:var(--accent-50);border:1px solid var(--accent-100);border-radius:16px;padding:24px">
      <strong style="font-size:19px">Start small: one topic, one cohort, one low-stakes week. Not a full course redesign.</strong>
    </div>
  </section>`;

views.summary = () => h`
  <section>
    <h2 class="h">Summary &amp; Key Takeaways</h2>
    <p class="lede">Empowering sustainability within you — to survive fourteen weeks, and the semesters after them.</p>
  </section>

  <section>
    <div class="grid g2">
      ${map([
        ["Lecturers Are Thinkers", "Apply creativity and innovation to design purposeful, impactful materials."],
        ["Renew Intention &amp; Be Authentic", "Make sense of the content for your students and for yourself."],
        ["Modify the Micro Level", "That is where you have full control — and where innovation lives."],
        ["Integrate Research (SoTL)", "Collect data, evaluate impact, and publish your findings."]
      ], ([t, d]) => h`<div class="card topline"><h4 class="h">${t}</h4><p class="small">${d}</p></div>`)}
    </div>
  </section>

  <section>
    <h3 class="h">Moving Forward: Sustaining Motivation</h3>
    <div class="grid g3">
      ${map(MOTIVATION, ([t, d]) => h`
        <div class="card"><h4 class="h" style="font-size:17px">${t}</h4><p class="small">${d}</p></div>`)}
    </div>
  </section>

  <section>
    <div class="navy">
      <p class="stmt">Avoid syok sendiri — do not create innovations that delight the lecturer but confuse the student.</p>
      <p class="sub">Ask them. Their answer is the evidence.</p>
    </div>
  </section>

  <section><div id="quizSummary"></div></section>`;

/* ===========================================================================
   ACTIVITY PANELS
   ========================================================================= */
function panelTiktok() {
  return h`
    <div class="dark" style="margin-bottom:24px">
      <div style="display:flex;gap:14px;align-items:center;margin-bottom:12px">
        <span style="font-size:36px;font-weight:700;opacity:.45">01</span>
        <span class="pill" style="background:rgba(255,255,255,.18)">24 MINUTES</span>
      </div>
      <h3 class="h" style="font-size:24px;color:#fff">The TikTok Challenge</h3>
      <p style="margin:6px 0 0">Sixty seconds on the innovation you just designed</p>
    </div>
    <div class="grid g2" style="align-items:start">
      <div class="card card--tint">
        <span class="eyebrow">Your task</span>
        <p>Use AI tools to make a vertical video, 60 seconds or less, about the innovation on your canvas —
        the problem, and what students will now do differently. Post it to the challenge account.</p>
        <span class="eyebrow" style="margin-top:20px">Done looks like</span>
        <ul class="ticks">
          <li>Posted to the challenge account, with the hashtag</li>
          <li>AI-generated content toggle switched on</li>
          <li>In-app sounds only</li>
          <li>One sentence in the caption naming the problem it solves</li>
        </ul>
      </div>
      <div class="card">
        <span class="eyebrow">Timing</span>
        ${map([["5 min", "Script it from your canvas"], ["14 min", "Generate, assemble, trim"], ["5 min", "Post and tag"]],
          ([t, l]) => h`<div style="margin-bottom:16px"><span class="pill">${t}</span>
            <div class="small" style="margin-top:6px">${l}</div></div>`)}
        <div style="border-top:1px solid var(--line);padding-top:16px;margin-top:4px">
          <span class="small" style="color:var(--accent-700);font-weight:700;font-style:italic">
            Account created before today. If yours failed, pair up now.</span></div>
      </div>
    </div>
    <h4 class="h" style="margin:32px 0 8px">Before you post</h4>
    <p class="small" style="margin-bottom:16px">Five rules — each one a design decision worth copying with your own students.</p>
    ${map([
      ["Label the AI content", "Use the built-in AI-generated toggle. You are modelling the disclosure practice you want your own students using."],
      ["Challenge account only", "Never your personal account. An opt-out exists — the shared folder counts as submitted."],
      ["Nobody in frame who did not agree", "No students, no colleagues passing, no name tags or ID badges. A dedicated account is still public."],
      ["In-app sounds only", "External music invites a takedown, and a removed video is a lost artefact."],
      ["One shared hashtag", "So every entry is findable in the showcase — and afterwards, as evidence."]
    ], ([r, d], i) => h`
      <div class="row" ${i === 0 ? 'style="background:var(--accent-50);border-color:var(--accent-100)"' : ''}>
        <div class="row__k" style="display:flex;gap:12px;align-items:center"><span class="dot">${i + 1}</span>${r}</div>
        <div class="row__v">${d}</div></div>`)}
    <div style="background:var(--head);color:#fff;border-radius:16px;padding:26px;margin-top:24px">
      <h4 class="h" style="color:#fff">How it is judged</h4>
      <div class="grid g2" style="gap:12px;margin-top:14px">
        ${map(["Is the problem real — not a topic, but something going wrong?",
               "Is the change pedagogical — does what students DO change?",
               "Is there a hook in the first three seconds?",
               "Would a colleague steal this idea?"],
          j => h`<div style="background:rgba(255,255,255,.1);border:1px solid rgba(255,255,255,.14);border-radius:8px;padding:12px;font-size:15px">${j}</div>`)}
      </div>
      <p style="color:#94a3b8;font-size:14px;margin-top:16px;font-style:italic">
        Nobody has ever failed this for bad lighting. People fail it for describing a tool instead of a change.</p>
    </div>`;
}

function panelVibe() {
  return h`
    <div class="dark" style="margin-bottom:24px">
      <div style="display:flex;gap:14px;align-items:center;margin-bottom:12px">
        <span style="font-size:36px;font-weight:700;opacity:.45">02</span>
        <span class="pill" style="background:rgba(255,255,255,.18)">25 MINUTES</span>
      </div>
      <h3 class="h" style="font-size:24px;color:#fff">The Vibe Coding Challenge</h3>
      <p style="margin:6px 0 0">Build a small game that teaches one concept from your course</p>
    </div>

    <div class="card card--tint" style="margin-bottom:24px">
      <span class="eyebrow">Your task</span>
      <p style="margin:0">Describe a simple browser game in plain language and let AI build it. The game must
      teach one specific concept your students struggle with. You never read the code — you play it, judge it,
      and describe what is wrong until it is right.</p>
    </div>

    <h4 class="h" style="margin-bottom:14px">The loop</h4>
    <div class="grid g3">
      ${map([
        ["Describe", "In plain English or Malay. Who plays, what they do, what they should notice."],
        ["Play", "You get something working, usually imperfect. Play it as a student would."],
        ["Correct", "Say what is wrong in words — “the score should drop when the valve is wrong” — and it rebuilds."]
      ], ([t, d], i) => h`
        <div class="card"><div class="dot dot--solid" style="margin-bottom:12px">${i + 1}</div>
          <h4 class="h" style="font-size:17px">${t}</h4><p class="small">${d}</p></div>`)}
    </div>
    <p class="small" style="margin-top:14px;font-style:italic">You never read the code. You judge the behaviour —
    a skill you already have as an engineer.</p>

    <h4 class="h" style="margin:32px 0 8px">The prompt skeleton</h4>
    <p class="small" style="margin-bottom:16px">Fill these five fields on paper first. Vague in, vague out.</p>
    ${map([
      ["Who the learner is", "Second-year chemical engineering students"],
      ["What one concept", "Why the drying rate stops being constant"],
      ["What the player does", "Drag air temperature and velocity sliders to hit a target drying time"],
      ["What they should notice", "The critical moisture content shifts as conditions change"],
      ["One constraint", "One screen, no scrolling, works on a phone"]
    ], ([f, e], i) => h`
      <div class="row">
        <div class="row__k" style="display:flex;gap:12px;align-items:center"><span class="dot">${i + 1}</span>${f}</div>
        <div class="row__v" style="font-style:italic;color:var(--muted)">${e}</div></div>`)}

    <h4 class="h" style="margin:32px 0 8px">Game ideas to steal</h4>
    <p class="small" style="margin-bottom:16px">Pick one, or bring the concept your students always get wrong.</p>
    <div class="grid g3">
      ${map([
        ["P&amp;ID Symbol Match", "Timed matching game pairing instrumentation symbols to their real equipment photo."],
        ["Drying Curve Sliders", "Adjust temperature and air velocity to hit a target drying time; the curve redraws live."],
        ["Mass Balance Puzzle", "Drag stream values into a flowsheet until the balance closes; wrong answers show the error."],
        ["Unit Conversion Sprint", "Sixty seconds, as many correct engineering unit conversions as possible."],
        ["Separation Sorter", "Match a mixture to the correct separation method and justify it in one line."],
        ["Safety Hazard Spotter", "Find the hazards in a plant scene before the timer runs out."]
      ], ([t, d]) => h`<div class="card topline"><h4 class="h" style="font-size:17px">${t}</h4><p class="small">${d}</p></div>`)}
    </div>

    <div class="grid g2" style="margin-top:32px;align-items:start">
      <div class="card">
        <span class="eyebrow">Timing</span>
        ${map([["5 min", "Fill the five fields, on paper"], ["15 min", "Describe, play, correct, repeat"], ["5 min", "Swap with your neighbour and play theirs"]],
          ([t, l]) => h`<div style="margin-bottom:16px"><span class="pill">${t}</span>
            <div class="small" style="margin-top:6px">${l}</div></div>`)}
      </div>
      <div class="card" style="background:var(--ok-bg);border-color:var(--ok-line)">
        <span class="eyebrow" style="color:var(--ok-ink)">Done looks like</span>
        <ul class="ticks">
          <li>It opens and does not crash</li>
          <li>A student can do something that changes the outcome</li>
          <li>Something visibly responds to what they do</li>
          <li>You can say in one sentence what it teaches</li>
        </ul>
        <p class="small" style="margin-top:14px;font-style:italic">Twenty-five minutes is deliberately not enough
        to polish. The goal is proof that it is possible.</p>
      </div>
    </div>

    <div class="grid g2" style="margin-top:24px">
      ${map([
        ["Verify the engineering yourself", "It will produce a confident, plausible, wrong curve. It does not know your correlations, units or boundary conditions."],
        ["No student data goes in", "No names, no matric numbers, no marks, no submitted work. Not to draft a rubric, not “just this once”."]
      ], ([t, d], i) => h`
        <div class="card" style="background:var(--warn-bg);border-color:var(--warn-line)">
          <div style="font-size:28px;font-weight:700;color:var(--warn-ink)">${pad(i + 1)}</div>
          <h4 class="h" style="font-size:17px;margin-top:8px">${t}</h4>
          <p class="small">${d}</p></div>`)}
    </div>`;
}

/* ===========================================================================
   QUIZ — one implementation, used for both the 7-question sets and the
   single-question checks.
   ========================================================================= */
function mountQuiz(node, items, badge) {
  let i = 0, picked = null, checked = false, score = 0, done = false;

  function render() {
    if (done) {
      const pct = Math.round(score / items.length * 100);
      const verdict = pct >= 85 ? "You can reliably tell a tool swap from a real change in what students do."
        : pct >= 57 ? "Solid instinct. The tricky ones are where the same tool gives a different answer depending on what follows it."
        : "Worth revisiting the section above — the distinction is the layer you changed, not the tool you used.";
      node.innerHTML = h`
        <div class="quiz fade"><div class="result">
          <div class="ring">${pct}%</div>
          <h3 class="h" style="font-size:20px">${score} out of ${items.length} correct</h3>
          <p class="small" style="max-width:46ch;margin:10px auto 22px">${verdict}</p>
          <button class="btn btn--ghost" data-retry>Try again</button>
        </div></div>`;
      node.querySelector('[data-retry]').onclick = () => { i = 0; picked = null; checked = false; score = 0; done = false; render(); };
      return;
    }

    const q = items[i];
    const multi = items.length > 1;
    node.innerHTML = h`
      <div class="quiz fade">
        <div class="quiz__top">
          <span class="pill pill--accent">${badge}</span>
          ${multi ? h`<span class="quiz__count">Question ${i + 1} of ${items.length} &nbsp;&bull;&nbsp; Score ${score}</span>` : ''}
        </div>
        ${multi ? h`<div class="meter"><i style="width:${i / items.length * 100}%"></i></div>` : ''}
        ${q.s ? h`<div class="scenario">${q.s}</div>` : ''}
        <p class="qtext">${q.q}</p>
        <div data-opts>
          ${map(q.o, (o, n) => h`<button class="opt" data-i="${n}"><span class="mark"></span><span>${o}</span></button>`)}
        </div>
        <div data-foot></div>
      </div>`;

    const foot = node.querySelector('[data-foot]');
    const opts = Array.from(node.querySelectorAll('.opt'));

    opts.forEach(btn => btn.onclick = () => {
      if (checked) return;
      picked = Number(btn.dataset.i);
      opts.forEach(b => b.setAttribute('aria-pressed', String(b === btn)));
      foot.innerHTML = '<button class="btn" style="margin-top:16px" data-check>Check answer</button>';
      foot.querySelector('[data-check]').onclick = check;
    });

    function check() {
      checked = true;
      const right = picked === q.a;
      if (right) score++;
      opts.forEach(b => {
        const n = Number(b.dataset.i);
        b.disabled = true;
        b.removeAttribute('aria-pressed');
        b.dataset.s = n === q.a ? 'right' : (n === picked ? 'wrong' : 'mute');
        if (n === q.a) b.querySelector('.mark').textContent = '✓';
      });
      const last = i === items.length - 1;
      foot.innerHTML = h`
        <div class="verdict ${right ? 'verdict--ok' : 'verdict--no'}">
          <b>${right ? '✓ Correct' : 'Not quite.'}</b>
          <span style="font-size:16px">${q.e}</span>
          ${multi ? h`<div><button class="btn btn--dark" style="margin-top:16px" data-next>${last ? 'See my score' : 'Next question'}</button></div>` : ''}
        </div>`;
      const next = foot.querySelector('[data-next]');
      if (next) next.onclick = () => {
        if (last) { done = true; } else { i++; picked = null; checked = false; }
        render();
      };
    }
  }
  render();
}

/* ===========================================================================
   ROUTER
   ========================================================================= */
const TABS = [
  ['welcome',    'Welcome and Introduction'],
  ['innovation', '1. What Is Innovation?'],
  ['pedagogy',   '2. Pedagogies'],
  ['method',     '3. Method to Craft Innovation'],
  ['cases',      '4. Assessment &amp; Case Studies'],
  ['activities', '5. Session Activities'],
  ['sotl',       '6. Research &amp; SoTL'],
  ['challenge',  '7. Challenge'],
  ['summary',    '8. Summary &amp; Moving Forward']
];

const tabsEl = document.getElementById('tabs');
const viewEl = document.getElementById('view');

tabsEl.innerHTML = map(TABS, ([id, label], i) => h`
  <li><button class="tab" data-tab="${id}" aria-current="${i === 0}">
    <span class="n">${pad(i + 1)}</span><span>${label}</span></button></li>`);

tabsEl.addEventListener('click', e => {
  const b = e.target.closest('[data-tab]');
  if (b) show(b.dataset.tab);
});

function show(id) {
  tabsEl.querySelectorAll('[data-tab]').forEach(b => b.setAttribute('aria-current', String(b.dataset.tab === id)));
  viewEl.className = 'view fade';
  viewEl.innerHTML = views[id]();
  document.querySelector('main').scrollTop = 0;
  window.scrollTo(0, 0);
  wire(id);
}

/* Behaviour for each view, bound after render. */
function wire(id) {
  if (id === 'welcome') {
    const boxes = Array.from(viewEl.querySelectorAll('.reflect'));
    const done = viewEl.querySelector('#reflectDone');
    boxes.forEach(b => b.onchange = () => { done.hidden = !boxes.every(x => x.checked); });
  }

  if (id === 'innovation') mountQuiz(viewEl.querySelector('#quizInnovation'), INNOVATION_QUIZ, 'Guessing game');
  if (id === 'pedagogy')   mountQuiz(viewEl.querySelector('#quizPedagogy'), PEDAGOGY_QUIZ, 'Name that pedagogy');
  if (id === 'method')     mountQuiz(viewEl.querySelector('#quizMethod'), [SINGLE.method], 'Quick quiz');
  if (id === 'cases')      mountQuiz(viewEl.querySelector('#quizCases'), [SINGLE.cases], 'Quick quiz');
  if (id === 'sotl')       mountQuiz(viewEl.querySelector('#quizSotl'), [SINGLE.sotl], 'Quick quiz');
  if (id === 'summary')    mountQuiz(viewEl.querySelector('#quizSummary'), [SINGLE.summary], 'Quick quiz');

  if (id === 'method') {
    const box = viewEl.querySelector('#levels');
    const drawLevel = lvl => {
      box.className = 'fade';
      box.innerHTML = lvl === 'macro'
        ? h`<div class="card card--flat" style="background:var(--page);margin-bottom:14px">
              <strong>These are decided above you.</strong>
              <span class="small"> You cannot change the item — but every row still leaves you something.
              That last line is where the work is.</span></div>
            ${map(MACRO, ([item, owner, why, lev]) => h`
              <div class="row"><div class="row__k">${item}<small>${owner}</small></div>
                <div class="row__v">${why}<div class="hint">→ ${lev}</div></div></div>`)}`
        : h`<div class="card card--tint card--flat" style="margin-bottom:14px">
              <strong>Nobody has to approve these.</strong>
              <span class="small"> Every case study in this workshop lives entirely in this column —
              and so will whatever you design today.</span></div>
            <div class="grid g2">
            ${map(MICRO, ([item, why, eg], i) => h`
              <div class="card" style="border-left:4px solid var(--accent-500)">
                <div style="display:flex;gap:12px;align-items:center;margin-bottom:10px">
                  <span class="dot">${i + 1}</span><h4 class="h" style="font-size:17px;margin:0">${item}</h4></div>
                <p class="small">${why}</p>
                <div style="background:var(--page);border-radius:8px;padding:10px 12px;font-size:14px">
                  <strong>For example:</strong> ${eg}</div></div>`)}
            </div>`;
    };
    drawLevel('macro');
    viewEl.querySelectorAll('[data-level]').forEach(b => b.onclick = () => {
      viewEl.querySelectorAll('[data-level]').forEach(x => x.setAttribute('aria-pressed', String(x === b)));
      drawLevel(b.dataset.level);
    });

    const panel = viewEl.querySelector('#cyclePanel');
    const drawStep = n => {
      panel.className = 'card fade';
      panel.innerHTML = h`<div class="dot dot--solid" style="width:46px;height:46px;font-size:20px;margin-bottom:16px">${n + 1}</div>
        <h3 class="h" style="font-size:24px">${CYCLE[n][0]}</h3>
        <p class="lede" style="margin:0">${CYCLE[n][1]}</p>`;
    };
    drawStep(0);
    viewEl.querySelectorAll('[data-step]').forEach(b => b.onclick = () => {
      viewEl.querySelectorAll('[data-step]').forEach(x => x.setAttribute('aria-pressed', String(x === b)));
      drawStep(Number(b.dataset.step));
    });
  }

  if (id === 'cases') {
    const panel = viewEl.querySelector('#casePanel');
    const drawCase = n => {
      const c = CASES[n];
      panel.className = 'fade';
      panel.innerHTML = h`
        <div class="card">
          <span class="eyebrow">${c.context}</span>
          <h3 class="h" style="margin-bottom:20px">${c.title}</h3>
          ${map(c.rows, ([k, v]) => h`
            <div class="row" style="box-shadow:none;background:transparent;border:0;border-bottom:1px solid var(--line);border-radius:0;padding:14px 0;margin:0">
              <div class="row__k" style="min-width:150px;color:var(--accent-700);font-size:14px;letter-spacing:.06em;text-transform:uppercase">${k}</div>
              <div class="row__v">${v}</div></div>`)}
          <div style="margin-top:20px;background:var(--head);color:#fff;border-radius:12px;padding:18px">
            <span style="font-size:13px;font-weight:700;letter-spacing:.08em;text-transform:uppercase;color:#94a3b8">Outputs</span>
            <div style="font-weight:700;margin-top:6px">${c.output}</div></div>
        </div>`;
    };
    drawCase(0);
    viewEl.querySelectorAll('[data-case]').forEach(b => b.onclick = () => {
      viewEl.querySelectorAll('[data-case]').forEach(x => x.setAttribute('aria-pressed', String(x === b)));
      drawCase(Number(b.dataset.case));
    });
  }

  if (id === 'activities') {
    const panel = viewEl.querySelector('#actPanel');
    const draw = which => {
      panel.className = 'fade';
      panel.innerHTML = which === 'tiktok' ? panelTiktok() : panelVibe();
    };
    draw('tiktok');
    viewEl.querySelectorAll('.actPick').forEach(b => b.onclick = () => {
      viewEl.querySelectorAll('.actPick').forEach(x => x.setAttribute('aria-pressed', String(x === b)));
      draw(b.dataset.act);
    });
  }

  if (id === 'challenge') {
    const get = k => viewEl.querySelector('#f' + k);
    const btn = viewEl.querySelector('#planBtn');
    const hint = viewEl.querySelector('#planHint');
    const check = () => {
      const ok = get('Problem').value.trim() && get('Activity').value.trim();
      btn.disabled = !ok;
      hint.textContent = ok ? 'Ready. Keep it somewhere you will see it in week one.'
                            : 'Complete at least the problem and the activity.';
    };
    ['Problem', 'Construct', 'Activity', 'Evidence'].forEach(k => get(k).addEventListener('input', check));
    check();

    btn.onclick = () => {
      const text = [
        'MY INNOVATION PLAN',
        'Designing Meaningful Teaching Materials — Prof. Ts. Dr. Zurina Zainal Abidin',
        new Date().toLocaleString(), '',
        '1. THE PROBLEM', get('Problem').value || '(not completed)', '',
        '2. PEDAGOGICAL CONSTRUCT', get('Construct').value || '(not completed)', '',
        '3. THE ACTIVITY', get('Activity').value || '(not completed)', '',
        '4. EVIDENCE PLAN — what, and in which week', get('Evidence').value || '(not completed)', '',
        'Start small: one topic, one cohort, one low-stakes week.',
        'Collect the evidence the first time it runs — not afterwards.'
      ].join('\n');
      const url = URL.createObjectURL(new Blob([text], { type: 'text/plain;charset=utf-8' }));
      const a = document.createElement('a');
      a.href = url; a.download = 'my-innovation-plan.txt';
      document.body.appendChild(a); a.click(); a.remove();
      URL.revokeObjectURL(url);
      hint.textContent = 'Downloaded. Keep it somewhere you will see it in week one.';
    };
  }
}

/* Theme toggle — swaps the accent variable block on <html>. */
const themeBtn = document.getElementById('theme');
const themeName = document.getElementById('themeName');
themeBtn.onclick = () => {
  const next = document.documentElement.dataset.theme === 'blue' ? 'pink' : 'blue';
  document.documentElement.dataset.theme = next;
  themeName.textContent = next === 'blue' ? 'Blue' : 'Pink';
  themeBtn.setAttribute('aria-label', next === 'blue' ? 'Switch to pink theme' : 'Switch to blue theme');
};

show('welcome');
</script>
</body>
</html>
