<html lang="en">
<head>
<meta charset="utf-8">
<meta name="viewport" content="width=device-width, initial-scale=1">
<title>Designing Meaningful Teaching Materials — KAPP Workshop</title>
<style>
/* ===========================================================================
   TOKENS
   Warm paper palette, clay accent, serif display. Type scale runs large:
   this is read on a projector and over a lecturer's shoulder.
   ========================================================================= */
:root {
  --bone:      #F0EEE6;   /* page */
  --paper:     #FAF9F5;   /* cards */
  --paper-dim: #E9E6DA;   /* inset panels */
  --ink:       #191813;   /* headings, body */
  --ink-soft:  #3C3931;   /* secondary body */
  --ink-faint: #6B665A;   /* captions only */
  --rule:      #DCD8CB;   /* hairlines */
  --clay:      #C15F3C;   /* accent */
  --clay-dim:  #F2E4DC;   /* accent wash */
  --navy:      #16305C;   /* the definition panel */
  --moss:      #47603F;   /* correct */
  --moss-dim:  #E6EBE1;
  --brick:     #9E3B29;   /* incorrect */
  --brick-dim: #F5E3DF;

  --serif: Georgia, 'Iowan Old Style', 'Times New Roman', serif;
  --sans:  system-ui, -apple-system, 'Segoe UI', Helvetica, Arial, sans-serif;
  --mono:  ui-monospace, SFMono-Regular, Menlo, Consolas, monospace;

  --measure: 68ch;
  --pad: clamp(1.25rem, 4vw, 3rem);
}

* { box-sizing: border-box; }

html { -webkit-text-size-adjust: 100%; }

body {
  margin: 0;
  background: var(--bone);
  color: var(--ink);
  font: 400 17px/1.65 var(--sans);
  font-synthesis-weight: none;
}

h1, h2, h3, h4 { font-family: var(--serif); font-weight: 600; line-height: 1.2; margin: 0; }
p { margin: 0 0 1em; }
p:last-child { margin-bottom: 0; }
strong { font-weight: 650; color: var(--ink); }
em { font-style: italic; }

/* Utility label — mono, tracked out, sits above a rule. Used for every
   section eyebrow so the reader always knows where they are. */
.eyebrow {
  font: 600 13px/1 var(--mono);
  letter-spacing: .14em;
  text-transform: uppercase;
  color: var(--clay);
  display: block;
  margin-bottom: .75rem;
}

.rule { border: 0; border-top: 1px solid var(--rule); margin: 0 0 1.5rem; }

/* ===========================================================================
   FRAME
   ========================================================================= */
.masthead {
  display: flex; align-items: center; gap: 1rem;
  padding: 1rem var(--pad);
  background: var(--paper);
  border-bottom: 1px solid var(--rule);
  position: sticky; top: 0; z-index: 20;
}
.masthead__mark {
  width: 38px; height: 38px; flex: none;
  background: var(--navy); color: #fff;
  display: grid; place-items: center;
  font: 600 15px/1 var(--serif);
  border-radius: 3px;
}
.masthead__title { font-size: 17px; letter-spacing: -.01em; }
.masthead__sub {
  font: 500 13px/1 var(--mono); letter-spacing: .08em;
  text-transform: uppercase; color: var(--ink-faint); margin-top: .35rem;
}
.masthead__meta { margin-left: auto; text-align: right; font: 500 13px/1.4 var(--mono); color: var(--ink-faint); }
.masthead__meta b { display: block; font: 600 15px/1.4 var(--mono); color: var(--ink); }

.shell { display: flex; align-items: flex-start; }

/* --- Sidebar ---------------------------------------------------------- */
.rail {
  flex: none; width: 268px;
  border-right: 1px solid var(--rule);
  padding: 2rem 0 3rem 1.5rem;
  position: sticky; top: 71px; height: calc(100vh - 71px);
  overflow-y: auto;
}
.rail h2 {
  font: 600 13px/1 var(--mono); letter-spacing: .14em;
  text-transform: uppercase; color: var(--ink-faint);
  margin: 0 0 1.25rem;
}
.rail ol { list-style: none; margin: 0; padding: 0 1rem 0 0; }
.rail li { margin-bottom: 2px; }
.rail button {
  display: flex; gap: .75rem; align-items: baseline;
  width: 100%; text-align: left;
  background: none; border: 0; border-radius: 4px;
  padding: .6rem .7rem;
  font: 400 16px/1.35 var(--sans); color: var(--ink-soft);
  cursor: pointer;
}
.rail button:hover { background: var(--paper); color: var(--ink); }
.rail button .num { font: 500 13px/1.4 var(--mono); color: var(--ink-faint); flex: none; }
.rail button[aria-current="true"] {
  background: var(--paper); color: var(--ink); font-weight: 600;
  box-shadow: inset 3px 0 0 var(--clay);
}
.rail button[aria-current="true"] .num { color: var(--clay); }

/* --- Main ------------------------------------------------------------- */
main { flex: 1; min-width: 0; padding: 2.5rem var(--pad) 6rem; }
.view { max-width: 940px; }
.view > section { margin-bottom: 3.5rem; }
.view > section:last-child { margin-bottom: 0; }

h1.page { font-size: clamp(2rem, 4vw, 2.6rem); letter-spacing: -.02em; margin-bottom: .75rem; }
h2.sec  { font-size: 1.55rem; letter-spacing: -.01em; margin-bottom: .5rem; }
h3.sub  { font-size: 1.2rem; margin-bottom: .5rem; }
.lede { font-size: 1.1rem; color: var(--ink-soft); max-width: var(--measure); }

/* ===========================================================================
   COMPONENTS
   ========================================================================= */
.card {
  background: var(--paper);
  border: 1px solid var(--rule);
  border-radius: 6px;
  padding: 1.5rem;
}
.grid { display: grid; gap: 1rem; }
.grid--2 { grid-template-columns: repeat(2, minmax(0,1fr)); }
.grid--3 { grid-template-columns: repeat(3, minmax(0,1fr)); }

/* The definition panel — the one navy object in the whole document. */
.panel-navy {
  background: var(--navy); color: #F2F4F8;
  border-radius: 6px; padding: 2rem;
}
.panel-navy .stmt { font-family: var(--serif); font-size: 1.45rem; line-height: 1.35; color: #fff; }
.panel-navy .note { color: #B9C6DE; font-size: 1rem; margin-top: 1rem; }

.panel-dark {
  background: var(--ink); color: #EDEAE1;
  border-radius: 6px; padding: 1.5rem;
}
.panel-clay { background: var(--clay-dim); border: 1px solid #E4CFC3; border-radius: 6px; padding: 1.5rem; }
.panel-inset { background: var(--paper-dim); border-radius: 6px; padding: 1.25rem; }

/* Numbered marker — only used where the content is genuinely ordered. */
.marker {
  font: 600 13px/1 var(--mono); color: var(--clay);
  letter-spacing: .1em; display: block; margin-bottom: .5rem;
}

.chip {
  display: inline-block; font: 600 13px/1 var(--mono);
  letter-spacing: .06em; text-transform: uppercase;
  background: var(--ink); color: var(--paper);
  padding: .4rem .6rem; border-radius: 3px;
}
.chip--quiet { background: var(--paper-dim); color: var(--ink-soft); }
.chip--clay  { background: var(--clay); color: #fff; }

/* SIGNATURE: the four layers of innovation, drawn as physical depth.
   Each layer steps further in; the activity layer is the one that matters,
   so it alone carries the clay edge. */
.layers { border-left: 1px solid var(--rule); padding-left: 0; }
.layer {
  border: 1px solid var(--rule); border-left: 3px solid var(--rule);
  background: var(--paper); border-radius: 0 4px 4px 0;
  padding: 1rem 1.25rem; margin-bottom: .5rem;
  display: flex; gap: 1.5rem; flex-wrap: wrap;
}
.layer[data-depth="1"] { margin-left: 0; }
.layer[data-depth="2"] { margin-left: 1.5rem; }
.layer[data-depth="3"] { margin-left: 3rem; border-left-color: var(--clay); background: var(--clay-dim); }
.layer[data-depth="4"] { margin-left: 4.5rem; }
.layer .name { font-family: var(--serif); font-size: 1.05rem; font-weight: 600; min-width: 190px; }
.layer .name small { display: block; font: 400 14px/1.4 var(--sans); color: var(--ink-faint); }
.layer .eg { color: var(--ink-soft); font-size: 15px; flex: 1; min-width: 240px; }

/* Toggle group (macro/micro, activity switch) */
.switch { display: inline-flex; background: var(--paper-dim); border-radius: 5px; padding: 3px; gap: 3px; }
.switch button {
  border: 0; background: none; cursor: pointer; border-radius: 4px;
  padding: .55rem 1rem; font: 600 15px/1 var(--sans); color: var(--ink-soft);
}
.switch button[aria-pressed="true"] { background: var(--paper); color: var(--ink); box-shadow: 0 1px 2px rgba(0,0,0,.08); }

/* Definition-list rows used for macro items and prompt skeletons */
.row {
  display: flex; gap: 1.25rem; flex-wrap: wrap;
  border: 1px solid var(--rule); background: var(--paper);
  border-radius: 5px; padding: 1.1rem 1.25rem; margin-bottom: .6rem;
}
.row__key { min-width: 210px; font-weight: 650; }
.row__key small { display: block; font: 500 12.5px/1.4 var(--mono); letter-spacing: .06em; text-transform: uppercase; color: var(--ink-faint); margin-top: .25rem; }
.row__val { flex: 1; min-width: 260px; color: var(--ink-soft); font-size: 15.5px; }
.leverage { margin-top: .6rem; padding: .6rem .75rem; background: var(--moss-dim); border-radius: 4px; color: #2F4229; font-size: 15px; }

.tick { list-style: none; margin: 0; padding: 0; }
.tick li { position: relative; padding-left: 1.6rem; margin-bottom: .55rem; color: var(--ink-soft); }
.tick li::before { content: "→"; position: absolute; left: 0; color: var(--clay); font-family: var(--mono); }

/* Steps (design cycle) */
.steps { display: flex; gap: 1.5rem; flex-wrap: wrap; }
.steps__list { flex: 1 1 260px; }
.steps__list button {
  display: block; width: 100%; text-align: left; cursor: pointer;
  background: var(--paper); border: 1px solid var(--rule); border-radius: 5px;
  padding: .85rem 1rem; margin-bottom: .5rem; font: 400 16px/1.3 var(--sans); color: var(--ink-soft);
}
.steps__list button[aria-pressed="true"] { background: var(--ink); color: var(--paper); border-color: var(--ink); }
.steps__list button[aria-pressed="true"] .marker { color: var(--clay-dim); }
.steps__panel { flex: 2 1 340px; }

/* Quiz */
.quiz { border: 1px solid var(--rule); background: var(--paper); border-radius: 6px; padding: 1.75rem; }
.quiz__top { display: flex; justify-content: space-between; align-items: center; gap: 1rem; flex-wrap: wrap; margin-bottom: 1rem; }
.quiz__meter { height: 4px; background: var(--paper-dim); border-radius: 2px; overflow: hidden; margin-bottom: 1.5rem; }
.quiz__meter i { display: block; height: 100%; background: var(--clay); transition: width .3s ease; }
.quiz__scenario {
  font-family: var(--serif); font-size: 1.15rem; line-height: 1.45;
  border-left: 3px solid var(--clay); padding: .25rem 0 .25rem 1.1rem; margin-bottom: 1.25rem;
}
.quiz__q { font-weight: 650; margin-bottom: 1rem; }
.opt {
  display: block; width: 100%; text-align: left; cursor: pointer;
  background: var(--paper); border: 1px solid var(--rule); border-radius: 5px;
  padding: .9rem 1.1rem; margin-bottom: .5rem; font: 400 16px/1.4 var(--sans); color: var(--ink);
}
.opt:hover:not(:disabled) { border-color: var(--ink-faint); }
.opt[aria-pressed="true"] { border-color: var(--clay); background: var(--clay-dim); }
.opt[data-state="right"] { border-color: var(--moss); background: var(--moss-dim); }
.opt[data-state="wrong"] { border-color: var(--brick); background: var(--brick-dim); }
.opt[data-state="mute"] { opacity: .5; }
.opt:disabled { cursor: default; }
.verdict { margin-top: 1.25rem; padding: 1.1rem 1.25rem; border-radius: 5px; }
.verdict--right { background: var(--moss-dim); border: 1px solid #C3D2BB; }
.verdict--wrong { background: var(--brick-dim); border: 1px solid #E2BFB7; }
.verdict h4 { font-family: var(--sans); font-size: 16px; font-weight: 700; margin-bottom: .4rem; }
.score { text-align: center; padding: 2rem 1rem; }
.score__pct { font-family: var(--serif); font-size: 3.2rem; line-height: 1; color: var(--clay); }

/* Buttons */
.btn {
  display: inline-flex; align-items: center; gap: .5rem; cursor: pointer;
  background: var(--ink); color: var(--paper); border: 1px solid var(--ink);
  border-radius: 4px; padding: .7rem 1.2rem; font: 600 16px/1 var(--sans);
}
.btn:hover { background: #000; }
.btn--clay { background: var(--clay); border-color: var(--clay); color: #fff; }
.btn--clay:hover { background: #A94F30; }
.btn:disabled { opacity: .4; cursor: not-allowed; }
.btn--ghost { background: none; color: var(--ink); border-color: var(--rule); }
.btn--ghost:hover { background: var(--paper-dim); }

/* Forms */
label.field { display: block; margin-bottom: 1.25rem; }
label.field > span { display: block; font-weight: 650; margin-bottom: .4rem; }
textarea, input[type=text] {
  width: 100%; font: 400 16px/1.55 var(--sans); color: var(--ink);
  background: var(--paper); border: 1px solid var(--rule); border-radius: 5px;
  padding: .75rem .9rem; resize: vertical;
}
textarea:focus, input[type=text]:focus, .opt:focus-visible, .btn:focus-visible,
.rail button:focus-visible, .switch button:focus-visible, .steps__list button:focus-visible {
  outline: 2px solid var(--clay); outline-offset: 2px;
}

/* Case studies */
.case__nav { display: flex; gap: .5rem; flex-wrap: wrap; margin-bottom: 1.5rem; }
.case__nav button {
  cursor: pointer; background: var(--paper); border: 1px solid var(--rule);
  border-radius: 4px; padding: .5rem .8rem; font: 500 15px/1 var(--sans); color: var(--ink-soft);
}
.case__nav button[aria-pressed="true"] { background: var(--clay); border-color: var(--clay); color: #fff; }

.speaker { display: flex; gap: 1.75rem; flex-wrap: wrap; align-items: flex-start; }
.speaker img { width: 132px; height: 132px; border-radius: 50%; object-fit: cover; border: 1px solid var(--rule); flex: none; }

.awards { display: grid; grid-template-columns: repeat(2, minmax(0,1fr)); gap: .6rem; margin-top: 1rem; }
.awards div { background: rgba(255,255,255,.07); border: 1px solid rgba(255,255,255,.12); border-radius: 4px; padding: .7rem .85rem; }
.awards b { font-size: 15px; }
.awards small { display: block; color: #AEBCD4; font-size: 13.5px; margin-top: .2rem; }

.fade { animation: fade .28s ease both; }
@keyframes fade { from { opacity: 0; transform: translateY(6px); } to { opacity: 1; transform: none; } }

@media (prefers-reduced-motion: reduce) {
  *, *::before, *::after { animation-duration: .001ms !important; transition-duration: .001ms !important; }
}

@media (max-width: 900px) {
  .grid--2, .grid--3, .awards { grid-template-columns: 1fr; }
  .shell { display: block; }
  .rail {
    width: auto; height: auto; position: static;
    border-right: 0; border-bottom: 1px solid var(--rule);
    padding: 1rem 0 1rem 1rem; overflow-x: auto;
  }
  .rail h2 { display: none; }
  .rail ol { display: flex; gap: .5rem; padding-right: 1rem; }
  .rail li { margin: 0; }
  .rail button { white-space: nowrap; border: 1px solid var(--rule); background: var(--paper); }
  .layer[data-depth] { margin-left: 0; }
}
</style>
</head>
<body>

<header class="masthead">
  <div class="masthead__mark">Z</div>
  <div>
    <h1 class="masthead__title">Designing Meaningful Teaching Materials</h1>
    <div class="masthead__sub">Prof. Ts. Dr. Zurina Zainal Abidin</div>
  </div>
  <div class="masthead__meta">
    <b>120 min</b>
    9 sections
  </div>
</header>

<div class="shell">
  <nav class="rail" aria-label="Workshop sections">
    <h2>Workshop Structure</h2>
    <ol id="rail"></ol>
  </nav>
  <main>
    <div id="view" class="view" role="region" aria-live="polite"></div>
  </main>
</div>

<script>
/* ===========================================================================
   DATA
   All workshop content lives here so the markup below stays structural.
   ========================================================================= */
const PORTRAIT = "data:image/jpeg;base64,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";

const PHILOSOPHIES = [
  ["Connectivity, compassion and empathy", "Teaching without knowing your students is like teaching without a soul. Build rapport, memorise names, create memorable moments."],
  ["Do-Sense-Feel (multisensory)", "Use the human senses — visual, auditory, kinesthetic, tactile — to create the feel or emotion that stimulates greater cognitive development."],
  ["Togetherness and empowerment", "Adopt a growth mindset and build authentic mentorship. Your authentic relationship is what empowers them."]
];

const TESTS = [
  ["It is intentional", "It answers a problem you actually identified in your own course — not a trend, and not a call for proposals.", "Chasing a tool because everyone is talking about it."],
  ["It changes what students do", "Their cognitive process differs. What happens inside the student's head is not the same as before.", "Same task, new device. The thinking is unchanged."],
  ["It is evidenced", "You can show that something improved — marks, attainment, competency, or transfer.", "Students said they enjoyed it, and nothing else was measured."]
];

const LAYERS = [
  [1, "Theory", "The account of how people learn", "Constructivism, active learning, multisensory learning"],
  [2, "Pedagogical approach", "The named model you draw on", "PBL, flipped classroom, experiential, collaborative, challenge-based"],
  [3, "Learning activity", "The specific thing students do", "Build the tower, dry the sample, trace the line on the real plant"],
  [4, "Tool", "What you deliver it with", "Kahoot, video, Visio, a rubric, an AI model"]
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
  ["Technology-enabled", "Only counts when the tool changes the activity, not just the delivery."],
  ["Learning support", "Peer teaching, mentoring, self-access material, video demos."]
];

const PEDAGOGIES = [
  ["Constructivism &amp; active learning", "Students construct understanding rather than receive it.", "An open-ended problem with no obvious solution; the lecturer facilitates instead of answering.", "Students derive the design approach themselves before you show the standard method."],
  ["Flipped classroom (Kelas Berbalik)", "Direct instruction moves out; class time becomes the hard part.", "Material consumed at home, contact hours spent on challenge and collaboration.", "P&amp;ID symbols compiled as pre-work, then a three-hour tracing challenge in class."],
  ["Experiential / hands-on", "Learning through concrete experience, then reflection (Kolb's cycle).", "Students do the real thing under professional constraints, then analyse what happened.", "Drying apple samples, collecting data, and defending the rate curve."],
  ["Multisensory pedagogy", "Multiple senses at once build richer cognitive connections.", "Something to see, touch, hear or smell — not a description of it.", "A real rose lets one smell its sweetness and feel the petals; an image cannot."],
  ["Collaborative &amp; problem-based learning", "Genuine interdependence, where the task cannot be done alone.", "Small teams, a shared deliverable, and individual accountability within it.", "Groups of four building a free-standing Power Tower against a specification."],
  ["Challenge-based immersive learning", "A real, bounded challenge in an authentic setting drives the learning.", "Time pressure, real equipment, and a problem with a right answer they must find.", "Tracing the flow on actual Boiler Drum Control Equipment in the pilot plant."],
  ["Assessment-as-learning", "The assessment produces learning while it measures it.", "A test students would still benefit from even if it were ungraded.", "An experiment-based continuous assessment replacing the paper test."]
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
  ["Learning activities", "The single highest-value thing you control: what students actually do.", "Build a tower, dry a sample, trace a live line on the pilot plant."],
  ["Assessment design &amp; format", "Within the approved weighting, the form of the assessment is yours.", "An experiment-based test instead of a paper test, at the same 15%."],
  ["Sequencing within a topic", "What comes first changes what students are ready to understand.", "Let them fail at the problem first, then teach the method they needed."],
  ["Feedback &amp; classroom climate", "How safe it feels to be wrong determines how much thinking happens out loud.", "Live polling that redirects your teaching instead of just scoring them."]
];

const CYCLE = [
  ["Identify the problem", "What is actually going wrong in your course?"],
  ["Diagnose the cause", "Why is it happening — beyond the symptom?"],
  ["Choose a pedagogical construct", "Name the model: flipped classroom, PBL, experiential learning."],
  ["Design the activity", "What will students actually do?"],
  ["Build the evidence plan", "Decide what data you collect before you run it."]
];

const CASES = [
  {
    tab: "Video demos",
    title: "Biochemical Engineering laboratory aided by video demo",
    context: "Biochemical Engineering, 2015 · Funded by GIPP UPM",
    rows: [
      ["Problem", "A shortage of funding to hire lab demonstrators disrupted the smooth running of the laboratory — several rigs run at once and all need supervision."],
      ["Objective", "Reduce dependency on demonstrators and technicians, and keep the lab courses sustainable."],
      ["Innovation", "Produce laboratory video demos of the procedures to assist student learning."],
      ["Method", "Students conducted experiments with and without the video demonstrations."],
      ["Assessment", "Lab reports and total assignment marks."],
      ["Impact", "Over 80% agreed the videos enhanced understanding, helped them visualise the steps, and improved motivation."]
    ],
    output: "GIPP grant · 2 copyrights · 1 conference paper · 1 silver medal"
  },
  {
    tab: "Power Tower",
    title: "Teamwork and real-life application in CAD",
    context: "Computer Aided Drawing",
    rows: [
      ["Problem", "Assignments were purely drawings. The routine creates boredom and has little relation to real-life application."],
      ["Objective", "Enhance the learning experience through experiential, collaborative STEM activity tied to real applications."],
      ["Innovation", "STEM-based hands-on activity added, giving a genuine basis for teamwork assessment."],
      ["Method", "Groups of four, three-hour session, building a free-standing Power Tower from a golf ball, 15 pipe cleaners and 3 straws."],
      ["Assessment", "Prototype, teamwork and reflection analysis, graded against specified Programme Outcomes."],
      ["Impact", "100% found it fun, 98% critical thinking, 96% analytical, 98% teamwork."]
    ],
    output: "1 bronze medal in PICTL"
  },
  {
    tab: "Comprehensive assessment",
    title: "Comprehensive CAD assessment",
    context: "Computer Aided Drawing · Tackling plagiarism",
    rows: [
      ["Problem", "Similarities in submitted drawings raised plagiarism concerns, and grading on the drawing alone could not verify actual hands-on competency."],
      ["Objective", "Tackle plagiarism and introduce a standard that evaluates competency, not just the artefact."],
      ["Innovation", "A comprehensive assessment combining cognitive (drawing) and psychomotor (live demonstration) components."],
      ["Method", "Drawing assignment 90%, plus a ten-minute hands-on demonstration worth 10%, guided by rubric."],
      ["Assessment", "100% total: 90% drawing, 10% psychomotor."],
      ["Impact", "Eradicated the plagiarism loophole. Students agreed the combination better reflected their real skills."]
    ],
    output: "1 gold medal in PICTL"
  },
  {
    tab: "Experiment as test",
    title: "Experiment-based assessment replacing the classroom test",
    context: "Physical Separation",
    rows: [
      ["Problem", "Typical assessment was classroom-based, paper-based, individual and cognitive — providing no meaningful learning experience."],
      ["Objective", "Enhance the learning experience through assessment itself, using an experiential and collaborative approach."],
      ["Innovation", "The test became the experiment."],
      ["Method", "Pairs over a three-hour session, drying apple samples and calculating moisture loss."],
      ["Assessment", "Experiment data collected, analysed, and engineering calculations graded."],
      ["Impact", "Over 75% strongly agreed that working in pairs let them work and learn more effectively."]
    ],
    output: "A test that teaches while it measures"
  },
  {
    tab: "P&amp;ID tracing",
    title: "Industrial application — tracing line activities",
    context: "Computer Aided Drawing · Industrial application",
    rows: [
      ["Problem", "P&amp;ID diagrams are widely used in industry, complicated to read, and must be related back to the actual plant."],
      ["Objective", "Expose students to reading a P&amp;ID against a real plant, as it is used in industry."],
      ["Innovation", "Challenge-based tracing line activities on actual Boiler Drum Control Equipment."],
      ["Method", "A 3-in-1 PID Maze: symbol compilation as flipped pre-work, a three-hour tracing challenge, then a mystery-unravel presentation of the flow logic."],
      ["Assessment", "Drawing portfolio (cognitive), quiz, and tracing line activity (psychomotor)."],
      ["Impact", "Highly interactive, work-related knowledge replicating a real plant, with commercialisation potential for TVET training."]
    ],
    output: "1 gold medal in PICTL 2020"
  }
];

const QUICKWINS = [
  ["2-hour monologue lecture", "Microlearning and polling in 15-minute chunks", "Passive listening becomes active recall"],
  ["Paper-based quiz", "Experiment-based assessment", "Rote memorisation becomes experiential learning"],
  ["Standard written essay", "A 60-second video pitch of one concept", "Regurgitation becomes synthesis"],
  ["100% final product grade", "Process-oriented grading of drafts, teamwork and prototype", "Outcome-focused becomes process-focused"]
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
    o: ["Multisensory pedagogy", "Flipped classroom", "Constructivism", "Assessment-as-learning"], a: 1,
    e: "Direct instruction moved out of the classroom, and contact time was repurposed for the difficult, collaborative work. That is the defining structure of a flipped classroom." },
  { s: "Pairs of students dry apple samples in an oven, weigh them at intervals, plot the drying curve, and calculate the critical moisture content.", q: "Which pedagogy is this?",
    o: ["Flipped classroom", "Experiential / hands-on", "Direct instruction", "Peer instruction"], a: 1,
    e: "Concrete experience followed by analysis and reflection — Kolb's experiential cycle. Students learn the concept by generating the data themselves." },
  { s: "You bring real roses into class so students can smell the sweetness and feel the petals, rather than showing a photograph on a slide.", q: "Which pedagogy is this?",
    o: ["Multisensory pedagogy", "Experiential learning", "Constructivism", "Challenge-based learning"], a: 0,
    e: "Multisensory pedagogy engages several senses at once to build richer cognitive connections. Do-Sense-Feel: emotion and sensation stimulate deeper cognitive development." },
  { s: "Groups of four are given one golf ball, fifteen pipe cleaners and three straws, and must build the tallest free-standing tower to a specification in ten minutes.", q: "Which pedagogy is this?",
    o: ["Direct instruction", "Collaborative &amp; problem-based learning", "Flipped classroom", "Multisensory pedagogy"], a: 1,
    e: "A shared deliverable that cannot be produced alone, under constraints, with individual accountability inside the team. It also carries an experiential reflection stage." },
  { s: "You pose an open-ended design problem with no obvious solution. You refuse to give the answer, and instead ask questions that help students build their own approach.", q: "Which pedagogy is this?",
    o: ["Constructivism &amp; active learning", "Assessment-as-learning", "Experiential learning", "Flipped classroom"], a: 0,
    e: "Students construct understanding rather than receive it, with the lecturer as facilitator. Withholding the answer is the pedagogical move, not an omission." },
  { s: "Students go into the pilot plant and must trace the actual flow path on live Boiler Drum Control Equipment to match it against the diagram, against the clock.", q: "Which pedagogy is this?",
    o: ["Multisensory pedagogy", "Challenge-based immersive learning", "Direct instruction", "Peer assessment"], a: 1,
    e: "A real, bounded challenge in an authentic industrial setting, with time pressure and a findable right answer. Immersion in the real environment separates this from a classroom exercise." },
  { s: "The continuous assessment is itself the experiment. Students would still gain the understanding even if the task carried no marks at all.", q: "Which pedagogy is this?",
    o: ["Summative testing", "Assessment-as-learning", "Flipped classroom", "Constructivism"], a: 1,
    e: "The ungraded-value criterion: if students would still learn from it without marks, the assessment is producing learning rather than only measuring it." }
];

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

/* ===========================================================================
   HELPERS
   ========================================================================= */
const h = (strings, ...vals) => strings.reduce((out, s, i) => out + s + (vals[i] ?? ''), '');
const list = (arr, fn) => arr.map(fn).join('');

/* ===========================================================================
   VIEWS
   Each returns an HTML string. Interactive behaviour is bound in wire().
   ========================================================================= */
const views = {};

views.welcome = () => h`
  <section>
    <span class="eyebrow">Kursus Asas Pengajaran dan Pembelajaran</span>
    <h1 class="page">Designing meaningful teaching materials</h1>
    <p class="lede">An interactive session for new university lecturers: what educational
    innovation actually means, how to craft it, and five case studies that were built
    with nothing more than a problem and a plan.</p>
  </section>

  <section>
    <div class="card">
      <span class="eyebrow">What you will leave with</span>
      <ul class="tick">
        <li><strong>A working definition of innovation</strong> that survives contact with a sceptical colleague.</li>
        <li><strong>A named pedagogy</strong> underneath whatever you are already doing.</li>
        <li><strong>A one-page plan</strong> for one problem in your own course, with an evidence date attached.</li>
      </ul>
    </div>
  </section>

  <section>
    <div class="panel-navy">
      <div class="speaker">
        <img src="${PORTRAIT}" alt="Prof. Ts. Dr. Zurina Zainal Abidin">
        <div style="flex:1;min-width:280px">
          <h2 style="font-size:1.5rem;color:#fff">Prof. Ts. Dr. Zurina Zainal Abidin</h2>
          <div style="font:600 13px/1.4 var(--mono);letter-spacing:.08em;text-transform:uppercase;color:#9FB2D2;margin:.5rem 0 1rem">
            Chemical and Environmental Engineering, UPM
          </div>
          <p style="color:#D5DCEA;font-size:16px">An educator and researcher driving innovation in teaching and learning.
          Believes in the Do-Sense-Feel philosophy to stimulate cognitive development, and empowers
          students through experiential learning.</p>
          <div class="awards">
            <div><b>Anugerah Akademik Negara</b><small>Finalist 2025 · Teaching, Engineering cluster</small></div>
            <div><b>Vice Chancellor Fellowship</b><small>AFNC 2021 · Teaching category</small></div>
            <div><b>Top 2% World Scientist</b><small>Elsevier &amp; Stanford, 2022–2023</small></div>
            <div><b>SEARCA Professorial Chair</b><small>Awarded 2025–2026</small></div>
          </div>
        </div>
      </div>
    </div>
  </section>

  <section>
    <span class="eyebrow">Where we begin</span>
    <h2 class="sec">Teaching in a VUCA world</h2>
    <p class="lede">We teach in conditions that are volatile, uncertain, complex and ambiguous.
    Before any method or tool, you need a philosophy you can comfortably inhabit — one that
    reflects who you actually are.</p>
    <div class="panel-clay" style="margin-top:1.25rem">
      <p style="font-family:var(--serif);font-size:1.2rem;margin:0">Adopt a consistent teaching philosophy where you can be yourself. Be authentic.</p>
    </div>
  </section>

  <section>
    <span class="eyebrow">Three philosophies</span>
    <h2 class="sec">What runs underneath every case study</h2>
    <hr class="rule">
    <div class="grid grid--3">
      ${list(PHILOSOPHIES, ([t, d], i) => h`
        <div class="card">
          <span class="marker">${String(i + 1).padStart(2, '0')}</span>
          <h3 class="sub">${t}</h3>
          <p style="color:var(--ink-soft);font-size:15.5px">${d}</p>
        </div>`)}
    </div>
  </section>

  <section>
    <div class="panel-dark">
      <h3 class="sub" style="color:#fff">Not knowing your student is like teaching without a soul</h3>
      <p style="color:#C7C2B4;font-size:16px">Palmer (2003). An authentic relationship between teacher and student
      helps students prioritise learning and succeed (Prewett et al., 2019).</p>
      <div class="grid grid--2" style="gap:.6rem;margin-top:1rem">
        ${list(["Build rapport", "Memorise names", "Memorable moments", "Freedom of speech"], t => h`
          <div style="background:rgba(255,255,255,.07);border:1px solid rgba(255,255,255,.12);border-radius:4px;padding:.7rem .9rem;font-weight:600">${t}</div>`)}
      </div>
    </div>
  </section>

  <section>
    <span class="eyebrow">Reflect</span>
    <h2 class="sec">Does your philosophy show up in your classroom?</h2>
    <hr class="rule">
    <div class="card">
      ${list([
        ["I know my students", "I can name most of them and I know what they struggle with."],
        ["They can sense my presence", "They would say I am present and invested, not just delivering."],
        ["I am being myself", "My teaching reflects who I actually am, not an imitation of someone else."]
      ], ([t, d], i) => h`
        <label class="field" style="display:flex;gap:.9rem;align-items:flex-start;margin-bottom:1rem;cursor:pointer">
          <input type="checkbox" class="reflect" style="width:20px;height:20px;margin-top:3px;accent-color:var(--clay)">
          <span style="margin:0"><strong>${t}</strong><br>
          <span style="font-weight:400;color:var(--ink-soft);font-size:15.5px">${d}</span></span>
        </label>`)}
      <div id="reflect-done" hidden class="panel-inset" style="background:var(--moss-dim);margin-top:.5rem">
        That is the foundation. Innovation, pedagogy and assessment all sit on top of it.
      </div>
    </div>
  </section>`;

views.innovation = () => h`
  <section>
    <span class="eyebrow">Section 1</span>
    <h1 class="page">What innovation actually is</h1>
  </section>

  <section>
    <div class="panel-navy">
      <p class="stmt">Innovation is a deliberate change in the learning process that produces
      a demonstrable improvement in learning.</p>
      <p class="note">The biggest misconception is that it requires expensive technology. It does not.</p>
    </div>
  </section>

  <section>
    <span class="eyebrow">The test</span>
    <h2 class="sec">Three tests — all three must pass</h2>
    <p class="lede">Novelty fails the third test. Technology usually fails the second.</p>
    <hr class="rule" style="margin-top:1.25rem">
    <div class="grid grid--3">
      ${list(TESTS, ([t, d, f], i) => h`
        <div class="card">
          <span class="marker">Test ${i + 1}</span>
          <h3 class="sub">${t}</h3>
          <p style="color:var(--ink-soft);font-size:15.5px">${d}</p>
          <div class="panel-inset" style="background:var(--brick-dim);padding:.7rem .85rem;font-size:14.5px">
            <strong>Fails when:</strong> ${f}
          </div>
        </div>`)}
    </div>
  </section>

  <section>
    <span class="eyebrow">The signature idea</span>
    <h2 class="sec">Where innovation lives</h2>
    <p class="lede">Four layers, each sitting deeper inside the course than the last. Most claimed
    innovation never leaves the bottom one.</p>
    <hr class="rule" style="margin-top:1.25rem">
    <div class="layers">
      ${list(LAYERS, ([d, name, sub, eg]) => h`
        <div class="layer" data-depth="${d}">
          <div class="name">${name}<small>${sub}</small></div>
          <div class="eg">${eg}</div>
        </div>`)}
    </div>
    <div class="panel-dark" style="margin-top:1.25rem">
      <p style="font-family:var(--serif);font-size:1.15rem;margin:0;color:#fff">
        If the students' thinking is unchanged, you innovated the tool — not the pedagogy.</p>
    </div>
  </section>

  <section>
    <span class="eyebrow">Where it starts</span>
    <h2 class="sec">Innovation answers a problem — usually a dull one</h2>
    <p class="lede">Nobody innovates because they woke up inspired. They innovate because something broke.</p>
    <hr class="rule" style="margin-top:1.25rem">
    <div class="grid grid--2">
      ${list(DRIVERS, d => h`<div class="card" style="padding:1rem 1.15rem;font-size:15.5px;color:var(--ink-soft)">${d}</div>`)}
    </div>
  </section>

  <section>
    <span class="eyebrow">Scope</span>
    <h2 class="sec">Six places innovation can happen</h2>
    <p class="lede">Most lecturers imagine only the fifth. The third is where the leverage is.</p>
    <hr class="rule" style="margin-top:1.25rem">
    <div class="grid grid--3">
      ${list(TYPES, ([t, d], i) => h`
        <div class="card" ${i === 2 ? 'style="background:var(--clay-dim);border-color:#E4CFC3"' : ''}>
          <h3 class="sub" style="font-size:1.05rem">${t}</h3>
          <p style="color:var(--ink-soft);font-size:15px">${d}</p>
        </div>`)}
    </div>
  </section>

  <section>
    <span class="eyebrow">Guessing game</span>
    <h2 class="sec">Is it innovation?</h2>
    <p class="lede">Seven scenarios. Decide before you read the explanation.</p>
    <hr class="rule" style="margin-top:1.25rem">
    <div id="quiz-innovation"></div>
  </section>`;

views.pedagogy = () => h`
  <section>
    <span class="eyebrow">Section 2</span>
    <h1 class="page">High-impact pedagogies</h1>
    <p class="lede">A pedagogy is the named model underneath your activity. Naming it lets you find
    the literature, defend the design, and eventually publish it.</p>
    <div class="panel-clay" style="margin-top:1.25rem">
      <p style="margin:0;font-size:16px">I ran these for years before I could name any of them.
      Naming them is what turned activities into papers.</p>
    </div>
  </section>

  <section>
    <hr class="rule">
    <div class="grid grid--2">
      ${list(PEDAGOGIES, ([n, p, l, e]) => h`
        <div class="card">
          <h3 class="sub">${n}</h3>
          <p style="font-weight:600;font-size:16px">${p}</p>
          <p style="color:var(--ink-soft);font-size:15.5px"><strong>Looks like:</strong> ${l}</p>
          <p style="color:var(--ink-soft);font-size:15.5px"><strong>For example:</strong> ${e}</p>
        </div>`)}
    </div>
  </section>

  <section>
    <div class="panel-dark">
      <h3 class="sub" style="color:#fff">How to choose</h3>
      <p style="color:#C7C2B4;margin:0">Pick the construct first, then design the activity from it — not the reverse.
      An activity chosen first and justified afterwards is how you end up with something that
      looks innovative and teaches nothing.</p>
    </div>
  </section>

  <section>
    <span class="eyebrow">Name that pedagogy</span>
    <h2 class="sec">Seven classroom scenarios</h2>
    <hr class="rule" style="margin-top:1.25rem">
    <div id="quiz-pedagogy"></div>
  </section>`;

views.method = () => h`
  <section>
    <span class="eyebrow">Section 3</span>
    <h1 class="page">Method to craft innovation</h1>
  </section>

  <section>
    <div class="panel-dark">
      <p style="font-family:var(--serif);font-size:1.3rem;line-height:1.4;color:#fff">
        Every course has two layers. One is decided for you and locked for the accreditation cycle.
        The other is entirely yours, every single semester.</p>
      <p style="color:#C7C2B4;margin:1rem 0 0">Innovation is impossible in the first and unavoidable
      in the second. Knowing which is which is the whole method.</p>
    </div>
  </section>

  <section>
    <span class="eyebrow">Know your two levels</span>
    <h2 class="sec">What you can and cannot change</h2>
    <p class="lede">Junior lecturers exhaust themselves fighting the macro column.</p>
    <div style="margin:1.5rem 0">
      <div class="switch" role="group" aria-label="Level">
        <button data-level="macro" aria-pressed="true">Macro — already fixed</button>
        <button data-level="micro" aria-pressed="false">Micro — entirely yours</button>
      </div>
    </div>
    <div id="levels"></div>
  </section>

  <section>
    <span class="eyebrow">The cycle</span>
    <h2 class="sec">Five steps from problem to evidence</h2>
    <hr class="rule" style="margin-top:1.25rem">
    <div class="steps">
      <div class="steps__list" id="cycle-list">
        ${list(CYCLE, ([t], i) => h`
          <button data-step="${i}" aria-pressed="${i === 0}">
            <span class="marker">Step ${i + 1}</span>${t}
          </button>`)}
      </div>
      <div class="steps__panel"><div class="card" id="cycle-panel"></div></div>
    </div>
  </section>`;

views.cases = () => h`
  <section>
    <span class="eyebrow">Section 4</span>
    <h1 class="page">Assessment and case studies</h1>
    <p class="lede">Five innovations that ran in real courses. Every one began with a problem,
    and every one collected its evidence the first time it ran.</p>
  </section>

  <section>
    <div class="case__nav" role="group" aria-label="Case studies">
      ${list(CASES, (c, i) => h`<button data-case="${i}" aria-pressed="${i === 0}">${i + 1}. ${c.tab}</button>`)}
    </div>
    <div id="case-panel"></div>
  </section>

  <section>
    <span class="eyebrow">Quick wins</span>
    <h2 class="sec">Small swaps that change what students do</h2>
    <hr class="rule" style="margin-top:1.25rem">
    ${list(QUICKWINS, ([a, b, c]) => h`
      <div class="row">
        <div class="row__key" style="color:var(--ink-faint)">${a}</div>
        <div class="row__val"><strong style="color:var(--ink)">${b}</strong>
          <div style="margin-top:.35rem;font-size:14.5px;color:var(--ink-faint)">${c}</div>
        </div>
      </div>`)}
  </section>`;

views.activities = () => h`
  <section>
    <span class="eyebrow">Section 5</span>
    <h1 class="page">Session activities</h1>
    <p class="lede">Two things you will build in this room. Both rest on the same idea: AI has
    collapsed the cost of <em>making</em> teaching material, so the scarce skill is deciding
    what is worth making.</p>
  </section>

  <section>
    <div class="switch" role="group" aria-label="Activity">
      <button data-act="tiktok" aria-pressed="true">01 · TikTok challenge</button>
      <button data-act="vibe" aria-pressed="false">02 · Vibe coding challenge</button>
    </div>
  </section>

  <section id="activity-panel"></section>`;

views.sotl = () => h`
  <section>
    <span class="eyebrow">Section 6</span>
    <h1 class="page">Research integration and SoTL</h1>
    <p class="lede">The Scholarship of Teaching and Learning treats teaching not as a task but as
    a scholarly endeavour: investigate your own classroom systematically, gather evidence, share it.</p>
  </section>

  <section>
    <span class="eyebrow">Evidence hierarchy</span>
    <h2 class="sec">Weakest to strongest</h2>
    <p class="lede">Most teaching reports stop at level one, and level one convinces nobody.</p>
    <hr class="rule" style="margin-top:1.25rem">
    ${list(EVIDENCE, ([t, d], i) => h`
      <div class="row" ${i >= 3 ? 'style="background:var(--clay-dim);border-color:#E4CFC3"' : ''}>
        <div class="row__key" style="min-width:60px"><span class="marker" style="margin:0">${i + 1}</span></div>
        <div class="row__val" style="color:var(--ink);font-weight:${i >= 3 ? '650' : '400'}">${t}</div>
        <div style="min-width:200px;color:var(--ink-faint);font-size:15px">${d}</div>
      </div>`)}
    <div class="panel-clay" style="margin-top:1.25rem">
      <p style="margin:0;font-weight:600">Satisfaction is not learning. Students often rate the lecture
      they enjoyed above the activity that taught them more.</p>
    </div>
  </section>

  <section>
    <span class="eyebrow">Before you collect anything</span>
    <h2 class="sec">Ethics first</h2>
    <hr class="rule" style="margin-top:1.25rem">
    <div class="grid grid--2">
      ${list(ETHICS, ([t, d]) => h`
        <div class="card"><h3 class="sub" style="font-size:1.05rem">${t}</h3>
        <p style="color:var(--ink-soft);font-size:15.5px">${d}</p></div>`)}
    </div>
  </section>

  <section>
    <div class="panel-dark">
      <h3 class="sub" style="color:#fff">One activity, many outputs</h3>
      <p style="color:#C7C2B4">None of these were planned in advance. All were possible only because
      the data was collected the first time the activity ran.</p>
      <div style="display:flex;gap:.5rem;flex-wrap:wrap;margin-top:1rem">
        ${list(["Teaching grant", "Conference paper", "Copyright", "Competition medal", "Award portfolio", "Book chapter"],
          o => h`<span style="background:rgba(255,255,255,.09);border:1px solid rgba(255,255,255,.14);padding:.45rem .75rem;border-radius:4px;font-size:15px;font-weight:600">${o}</span>`)}
      </div>
    </div>
  </section>`;

views.challenge = () => h`
  <section>
    <span class="eyebrow">Section 7</span>
    <h1 class="page">Your challenge</h1>
    <p class="lede">Pick one problem in your syllabus today and draft the plan. Not a curriculum
    overhaul — one thing, written down now, while you still believe it is possible.</p>
  </section>

  <section>
    <div class="card">
      <label class="field"><span>1 · Identify the problem</span>
        <textarea id="f-problem" rows="3" placeholder="What is actually going wrong in your course?"></textarea></label>
      <label class="field"><span>2 · Choose a pedagogical construct</span>
        <input type="text" id="f-construct" placeholder="Flipped classroom, PBL, experiential learning…"></label>
      <label class="field"><span>3 · Design the activity</span>
        <textarea id="f-activity" rows="3" placeholder="What will students actually do?"></textarea></label>
      <label class="field"><span>4 · Build the evidence plan</span>
        <input type="text" id="f-evidence" placeholder="What data, and in which week?"></label>
      <div style="display:flex;gap:.75rem;align-items:center;flex-wrap:wrap">
        <button class="btn btn--clay" id="download-plan" disabled>Download my plan</button>
        <span id="plan-hint" style="color:var(--ink-faint);font-size:15px">Fill in the problem and the activity to enable this.</span>
      </div>
    </div>
  </section>

  <section>
    <div class="panel-clay">
      <p style="font-family:var(--serif);font-size:1.2rem;margin:0">Start small: one topic, one cohort,
      one low-stakes week.</p>
    </div>
  </section>`;

views.summary = () => h`
  <section>
    <span class="eyebrow">Section 8</span>
    <h1 class="page">Summary and moving forward</h1>
    <p class="lede">Empowering sustainability within you — to survive fourteen weeks, and the
    semesters after them.</p>
  </section>

  <section>
    <div class="grid grid--2">
      ${list([
        ["Lecturers are thinkers", "Apply creativity and innovation to design purposeful, impactful materials."],
        ["Renew your intention, be authentic", "Make sense of the content for your students and for yourself."],
        ["Modify the micro level", "That is where you have full control — and where innovation lives."],
        ["Integrate research", "Collect data, evaluate impact, and publish your findings."]
      ], ([t, d]) => h`
        <div class="card"><h3 class="sub" style="font-size:1.1rem">${t}</h3>
        <p style="color:var(--ink-soft);font-size:15.5px">${d}</p></div>`)}
    </div>
  </section>

  <section>
    <div class="panel-navy">
      <p class="stmt">Avoid syok sendiri — do not create innovations that delight the lecturer
      but confuse the student.</p>
      <p class="note">Ask them. Their answer is the evidence.</p>
    </div>
  </section>`;

/* ===========================================================================
   ACTIVITY PANELS
   ========================================================================= */
function activityTiktok() {
  return h`
    <div class="panel-clay" style="margin-bottom:1.5rem">
      <span class="eyebrow">Activity 01 · 24 minutes</span>
      <h2 class="sec">Sixty seconds on the innovation you just designed</h2>
    </div>
    <div class="grid grid--2" style="align-items:start">
      <div class="card">
        <span class="eyebrow">Your task</span>
        <p>Use AI tools to make a vertical video, 60 seconds or less, about the innovation on your
        canvas — the problem, and what students will now do differently. Post it to the challenge account.</p>
        <span class="eyebrow" style="margin-top:1.25rem">Done looks like</span>
        <ul class="tick">
          <li>Posted to the challenge account, with the hashtag</li>
          <li>AI-generated content toggle switched on</li>
          <li>In-app sounds only</li>
          <li>One sentence in the caption naming the problem it solves</li>
        </ul>
      </div>
      <div class="card">
        <span class="eyebrow">Timing</span>
        ${list([["5 min", "Script it from your canvas"], ["14 min", "Generate, assemble, trim"], ["5 min", "Post and tag"]],
          ([t, l]) => h`<div style="margin-bottom:1rem"><span class="chip">${t}</span>
          <div style="margin-top:.4rem;color:var(--ink-soft)">${l}</div></div>`)}
        <hr class="rule" style="margin:1.25rem 0 1rem">
        <p style="color:var(--clay);font-weight:600;font-size:15.5px;margin:0">
          Account created before today. If yours failed, pair up now.</p>
      </div>
    </div>
    <h3 class="sub" style="margin:2rem 0 .5rem">Before you post</h3>
    <p class="lede" style="margin-bottom:1rem">Five rules — each one a design decision worth copying with your own students.</p>
    ${list([
      ["Label the AI content", "Use the built-in AI-generated toggle. You are modelling the disclosure practice you want your students using."],
      ["Challenge account only", "Never your personal account. An opt-out exists — the shared folder counts as submitted."],
      ["Nobody in frame who did not agree", "No students, no colleagues passing, no name tags. A dedicated account is still public."],
      ["In-app sounds only", "External music invites a takedown, and a removed video is a lost artefact."],
      ["One shared hashtag", "So every entry is findable in the showcase — and afterwards, as evidence."]
    ], ([r, d]) => h`<div class="row"><div class="row__key">${r}</div><div class="row__val">${d}</div></div>`)}
    <div class="panel-dark" style="margin-top:1.5rem">
      <h3 class="sub" style="color:#fff">How it is judged</h3>
      <ul class="tick" style="margin-top:.75rem">
        ${list([
          "Is the problem real — not a topic, but something going wrong?",
          "Is the change pedagogical — does what students do change?",
          "Is there a hook in the first three seconds?",
          "Would a colleague steal this idea?"
        ], j => h`<li style="color:#C7C2B4">${j}</li>`)}
      </ul>
      <p style="color:#8F897A;font-size:15px;margin-top:1rem;font-style:italic">
        Nobody has ever failed this for bad lighting. People fail it for describing a tool instead of a change.</p>
    </div>`;
}

function activityVibe() {
  return h`
    <div class="panel-inset" style="margin-bottom:1.5rem">
      <span class="eyebrow">Activity 02 · 25 minutes</span>
      <h2 class="sec">Build a small game that teaches one concept</h2>
    </div>
    <div class="card" style="margin-bottom:1.5rem">
      <span class="eyebrow">Your task</span>
      <p style="margin:0">Describe a simple browser game in plain language and let AI build it. The game must
      teach one specific concept your students struggle with. You never read the code — you play it,
      judge it, and describe what is wrong until it is right.</p>
    </div>

    <h3 class="sub" style="margin-bottom:.75rem">The loop</h3>
    <div class="grid grid--3">
      ${list([
        ["Describe", "In plain English or Malay. Who plays, what they do, what they should notice."],
        ["Play", "You get something working, usually imperfect. Play it as a student would."],
        ["Correct", "Say what is wrong in words — “the score should drop when the valve is wrong” — and it rebuilds."]
      ], ([t, d], i) => h`
        <div class="card"><span class="marker">${String(i + 1).padStart(2, '0')}</span>
        <h4 class="sub" style="font-size:1.05rem">${t}</h4>
        <p style="color:var(--ink-soft);font-size:15px">${d}</p></div>`)}
    </div>

    <h3 class="sub" style="margin:2rem 0 .5rem">The prompt skeleton</h3>
    <p class="lede" style="margin-bottom:1rem">Fill these five fields on paper first. Vague in, vague out.</p>
    ${list([
      ["Who the learner is", "Second-year chemical engineering students"],
      ["What one concept", "Why the drying rate stops being constant"],
      ["What the player does", "Drag air temperature and velocity sliders to hit a target drying time"],
      ["What they should notice", "The critical moisture content shifts as conditions change"],
      ["One constraint", "One screen, no scrolling, works on a phone"]
    ], ([f, e], i) => h`
      <div class="row"><div class="row__key"><span class="marker" style="display:inline;margin:0">${i + 1}</span> ${f}</div>
      <div class="row__val" style="font-style:italic">${e}</div></div>`)}

    <h3 class="sub" style="margin:2rem 0 .5rem">Game ideas to steal</h3>
    <div class="grid grid--3">
      ${list([
        ["P&amp;ID symbol match", "Timed matching game pairing instrumentation symbols to their real equipment photo."],
        ["Drying curve sliders", "Adjust temperature and air velocity to hit a target drying time; the curve redraws live."],
        ["Mass balance puzzle", "Drag stream values into a flowsheet until the balance closes; wrong answers show the error."],
        ["Unit conversion sprint", "Sixty seconds, as many correct engineering unit conversions as possible."],
        ["Separation sorter", "Match a mixture to the correct separation method and justify it in one line."],
        ["Safety hazard spotter", "Find the hazards in a plant scene before the timer runs out."]
      ], ([t, d]) => h`
        <div class="card"><h4 class="sub" style="font-size:1rem">${t}</h4>
        <p style="color:var(--ink-soft);font-size:15px">${d}</p></div>`)}
    </div>

    <div class="grid grid--2" style="margin-top:2rem;align-items:start">
      <div class="card">
        <span class="eyebrow">Timing</span>
        ${list([["5 min", "Fill the five fields, on paper"], ["15 min", "Describe, play, correct, repeat"], ["5 min", "Swap with your neighbour and play theirs"]],
          ([t, l]) => h`<div style="margin-bottom:1rem"><span class="chip">${t}</span>
          <div style="margin-top:.4rem;color:var(--ink-soft)">${l}</div></div>`)}
      </div>
      <div class="card" style="background:var(--moss-dim);border-color:#C3D2BB">
        <span class="eyebrow" style="color:var(--moss)">Done looks like</span>
        <ul class="tick">
          <li>It opens and does not crash</li>
          <li>A student can do something that changes the outcome</li>
          <li>Something visibly responds to what they do</li>
          <li>You can say in one sentence what it teaches</li>
        </ul>
      </div>
    </div>

    <div class="grid grid--2" style="margin-top:1.5rem">
      ${list([
        ["Verify the engineering yourself", "It will produce a confident, plausible, wrong curve. It does not know your correlations, units or boundary conditions."],
        ["No student data goes in", "No names, no matric numbers, no marks, no submitted work. Not to draft a rubric, not “just this once”."]
      ], ([t, d], i) => h`
        <div class="card" style="background:var(--brick-dim);border-color:#E2BFB7">
          <span class="marker" style="color:var(--brick)">Warning ${i + 1}</span>
          <h4 class="sub" style="font-size:1.05rem">${t}</h4>
          <p style="color:var(--ink-soft);font-size:15.5px">${d}</p></div>`)}
    </div>`;
}

/* ===========================================================================
   QUIZ
   One implementation, used by both quizzes.
   ========================================================================= */
function mountQuiz(node, items, badge) {
  let i = 0, picked = null, checked = false, score = 0, finished = false;

  function draw() {
    if (finished) {
      const pct = Math.round(score / items.length * 100);
      const verdict = pct >= 85 ? "You can reliably tell a tool swap from a real change in what students do."
        : pct >= 57 ? "Solid instinct. The tricky ones are where the same tool gives a different answer depending on what follows it."
        : "Worth another look above — the distinction is the layer you changed, not the tool you used.";
      node.innerHTML = h`
        <div class="quiz fade"><div class="score">
          <div class="score__pct">${pct}%</div>
          <h3 class="sub" style="margin:.75rem 0 .5rem">${score} of ${items.length} correct</h3>
          <p style="color:var(--ink-soft);max-width:44ch;margin:0 auto 1.5rem">${verdict}</p>
          <button class="btn btn--ghost" data-retry>Start again</button>
        </div></div>`;
      node.querySelector('[data-retry]').onclick = () => { i = 0; picked = null; checked = false; score = 0; finished = false; draw(); };
      return;
    }

    const q = items[i];
    node.innerHTML = h`
      <div class="quiz fade">
        <div class="quiz__top">
          <span class="chip chip--clay">${badge}</span>
          <span style="font:500 14px/1 var(--mono);color:var(--ink-faint)">
            ${i + 1} / ${items.length} &nbsp;·&nbsp; score ${score}</span>
        </div>
        <div class="quiz__meter"><i style="width:${i / items.length * 100}%"></i></div>
        <p class="quiz__scenario">${q.s}</p>
        <p class="quiz__q">${q.q}</p>
        <div data-opts>
          ${list(q.o, (o, idx) => h`<button class="opt" data-i="${idx}">${o}</button>`)}
        </div>
        <div data-foot style="margin-top:1.25rem"></div>
      </div>`;

    const foot = node.querySelector('[data-foot]');
    const opts = [...node.querySelectorAll('.opt')];

    opts.forEach(btn => btn.onclick = () => {
      if (checked) return;
      picked = +btn.dataset.i;
      opts.forEach(b => b.setAttribute('aria-pressed', b === btn));
      foot.innerHTML = '<button class="btn" data-check>Check answer</button>';
      foot.querySelector('[data-check]').onclick = check;
    });

    function check() {
      checked = true;
      const right = picked === q.a;
      if (right) score++;
      opts.forEach(b => {
        const idx = +b.dataset.i;
        b.disabled = true;
        b.removeAttribute('aria-pressed');
        b.dataset.state = idx === q.a ? 'right' : (idx === picked ? 'wrong' : 'mute');
      });
      const last = i === items.length - 1;
      foot.innerHTML = h`
        <div class="verdict ${right ? 'verdict--right' : 'verdict--wrong'}">
          <h4>${right ? 'Correct' : 'Not quite'}</h4>
          <p style="margin:0;font-size:16px">${q.e}</p>
          <button class="btn" style="margin-top:1rem" data-next>${last ? 'See my score' : 'Next question'}</button>
        </div>`;
      foot.querySelector('[data-next]').onclick = () => {
        if (last) { finished = true; } else { i++; picked = null; checked = false; }
        draw();
      };
    }
  }
  draw();
}

/* ===========================================================================
   ROUTER + WIRING
   ========================================================================= */
const TABS = [
  ['welcome',    'Welcome and introduction'],
  ['innovation', 'What is innovation?'],
  ['pedagogy',   'Pedagogies'],
  ['method',     'Method to craft innovation'],
  ['cases',      'Assessment and case studies'],
  ['activities', 'Session activities'],
  ['sotl',       'Research and SoTL'],
  ['challenge',  'Challenge'],
  ['summary',    'Summary and moving forward']
];

const railEl = document.getElementById('rail');
const viewEl = document.getElementById('view');

railEl.innerHTML = list(TABS, ([id, label], i) => h`
  <li><button data-tab="${id}" aria-current="${i === 0}">
    <span class="num">${String(i + 1).padStart(2, '0')}</span>${label}</button></li>`);

railEl.addEventListener('click', e => {
  const btn = e.target.closest('[data-tab]');
  if (btn) show(btn.dataset.tab);
});

function show(id) {
  railEl.querySelectorAll('[data-tab]').forEach(b => b.setAttribute('aria-current', b.dataset.tab === id));
  viewEl.className = 'view fade';
  viewEl.innerHTML = views[id]();
  window.scrollTo({ top: 0, behavior: 'instant' });
  wire(id);
}

function wire(id) {
  if (id === 'welcome') {
    const boxes = [...viewEl.querySelectorAll('.reflect')];
    const done = viewEl.querySelector('#reflect-done');
    boxes.forEach(b => b.onchange = () => { done.hidden = !boxes.every(x => x.checked); });
  }

  if (id === 'innovation') mountQuiz(viewEl.querySelector('#quiz-innovation'), INNOVATION_QUIZ, 'Is it innovation?');
  if (id === 'pedagogy')   mountQuiz(viewEl.querySelector('#quiz-pedagogy'), PEDAGOGY_QUIZ, 'Name that pedagogy');

  if (id === 'method') {
    const box = viewEl.querySelector('#levels');
    const drawLevel = lvl => {
      box.className = 'fade';
      box.innerHTML = lvl === 'macro'
        ? h`<div class="panel-inset" style="margin-bottom:1rem">
              <strong>These are decided above you.</strong> You cannot change the item — but every row
              still leaves you something. That last line is where the work is.</div>
            ${list(MACRO, ([item, owner, why, lev]) => h`
              <div class="row"><div class="row__key">${item}<small>${owner}</small></div>
                <div class="row__val">${why}<div class="leverage">→ ${lev}</div></div></div>`)}`
        : h`<div class="panel-clay" style="margin-bottom:1rem">
              <strong>Nobody has to approve these.</strong> Every case study in this workshop lives
              entirely in this column — and so will whatever you design today.</div>
            <div class="grid grid--2">
            ${list(MICRO, ([item, why, eg]) => h`
              <div class="card" style="border-left:3px solid var(--clay)">
                <h4 class="sub" style="font-size:1.05rem">${item}</h4>
                <p style="color:var(--ink-soft);font-size:15.5px">${why}</p>
                <div class="panel-inset" style="padding:.7rem .85rem;font-size:14.5px">
                  <strong>For example:</strong> ${eg}</div></div>`)}
            </div>`;
    };
    drawLevel('macro');
    viewEl.querySelectorAll('[data-level]').forEach(b => b.onclick = () => {
      viewEl.querySelectorAll('[data-level]').forEach(x => x.setAttribute('aria-pressed', x === b));
      drawLevel(b.dataset.level);
    });

    const panel = viewEl.querySelector('#cycle-panel');
    const drawStep = n => {
      panel.className = 'card fade';
      panel.innerHTML = h`<span class="marker">Step ${n + 1} of 5</span>
        <h3 class="sub" style="font-size:1.35rem;margin-bottom:.6rem">${CYCLE[n][0]}</h3>
        <p style="color:var(--ink-soft);font-size:17px;margin:0">${CYCLE[n][1]}</p>`;
    };
    drawStep(0);
    viewEl.querySelectorAll('[data-step]').forEach(b => b.onclick = () => {
      viewEl.querySelectorAll('[data-step]').forEach(x => x.setAttribute('aria-pressed', x === b));
      drawStep(+b.dataset.step);
    });
  }

  if (id === 'cases') {
    const panel = viewEl.querySelector('#case-panel');
    const drawCase = n => {
      const c = CASES[n];
      panel.className = 'fade';
      panel.innerHTML = h`
        <div class="card">
          <span class="eyebrow">${c.context}</span>
          <h2 class="sec" style="margin-bottom:1.25rem">${c.title}</h2>
          ${list(c.rows, ([k, v]) => h`
            <div class="row" style="background:transparent;border:0;border-bottom:1px solid var(--rule);border-radius:0;padding:.9rem 0;margin:0">
              <div class="row__key" style="min-width:150px;font:600 13px/1.5 var(--mono);letter-spacing:.08em;text-transform:uppercase;color:var(--clay)">${k}</div>
              <div class="row__val">${v}</div></div>`)}
          <div class="panel-dark" style="margin-top:1.25rem">
            <span style="font:600 13px/1 var(--mono);letter-spacing:.1em;text-transform:uppercase;color:#8F897A">Outputs</span>
            <p style="margin:.5rem 0 0;color:#fff;font-weight:600">${c.output}</p></div>
        </div>`;
    };
    drawCase(0);
    viewEl.querySelectorAll('[data-case]').forEach(b => b.onclick = () => {
      viewEl.querySelectorAll('[data-case]').forEach(x => x.setAttribute('aria-pressed', x === b));
      drawCase(+b.dataset.case);
    });
  }

  if (id === 'activities') {
    const panel = viewEl.querySelector('#activity-panel');
    const drawAct = which => {
      panel.className = 'fade';
      panel.innerHTML = which === 'tiktok' ? activityTiktok() : activityVibe();
    };
    drawAct('tiktok');
    viewEl.querySelectorAll('[data-act]').forEach(b => b.onclick = () => {
      viewEl.querySelectorAll('[data-act]').forEach(x => x.setAttribute('aria-pressed', x === b));
      drawAct(b.dataset.act);
    });
  }

  if (id === 'challenge') {
    const f = k => viewEl.querySelector('#f-' + k);
    const btn = viewEl.querySelector('#download-plan');
    const hint = viewEl.querySelector('#plan-hint');
    const check = () => {
      const ok = f('problem').value.trim() && f('activity').value.trim();
      btn.disabled = !ok;
      hint.textContent = ok ? 'Keep it somewhere you will see it in week one.'
                            : 'Fill in the problem and the activity to enable this.';
    };
    ['problem', 'construct', 'activity', 'evidence'].forEach(k => f(k).addEventListener('input', check));
    check();

    btn.onclick = () => {
      const text = [
        'MY INNOVATION PLAN',
        'Designing Meaningful Teaching Materials — Prof. Ts. Dr. Zurina Zainal Abidin',
        new Date().toLocaleString(), '',
        '1. THE PROBLEM', f('problem').value || '(not completed)', '',
        '2. PEDAGOGICAL CONSTRUCT', f('construct').value || '(not completed)', '',
        '3. THE ACTIVITY', f('activity').value || '(not completed)', '',
        '4. EVIDENCE PLAN — what, and in which week', f('evidence').value || '(not completed)', '',
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

show('welcome');
</script>
</body>
</html>
