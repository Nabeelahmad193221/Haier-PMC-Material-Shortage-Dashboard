
<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8">
<meta name="viewport" content="width=device-width, initial-scale=1.0">
<meta name="description" content="Haier PMC Material Shortage Dashboard built with Power BI. Explore material availability, shortages, inventory and production planning insights.">
<title>Haier PMC | Material Shortage Dashboard</title>

<style>
:root {
  --navy: #071b40;
  --blue: #0759c7;
  --cyan: #36b9f5;
  --light: #f3f7fd;
  --white: #ffffff;
  --text: #172b4d;
  --muted: #687b96;
  --border: #e0eaf7;
  --shadow: 0 12px 35px rgba(22, 70, 130, .08);
}

* {
  margin: 0;
  padding: 0;
  box-sizing: border-box;
}

html { scroll-behavior: smooth; }

body {
  font-family: "Segoe UI", Arial, sans-serif;
  background: var(--light);
  color: var(--text);
  line-height: 1.7;
}

a { text-decoration: none; color: inherit; }

.container {
  width: min(1120px, 91%);
  margin: auto;
}

/* Navigation */

.navbar {
  background: rgba(255,255,255,.96);
  border-bottom: 1px solid var(--border);
  position: sticky;
  top: 0;
  z-index: 10;
  backdrop-filter: blur(12px);
}

.nav-inner {
  min-height: 72px;
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 20px;
}

.logo {
  font-size: 23px;
  font-weight: 850;
  color: var(--blue);
  letter-spacing: -.7px;
}

.logo span { color: var(--navy); }

.nav-links {
  display: flex;
  gap: 24px;
  font-size: 13px;
  font-weight: 650;
  color: var(--muted);
}

.nav-links a:hover { color: var(--blue); }

/* Hero */

.hero {
  position: relative;
  overflow: hidden;
  padding: 90px 0 80px;
  color: white;
  background:
    radial-gradient(circle at 85% 15%,
      rgba(54,185,245,.32), transparent 30%),
    linear-gradient(125deg, #071b40, #0759c7 72%, #0876d9);
}

.hero::after {
  content: "";
  position: absolute;
  width: 400px;
  height: 400px;
  border: 1px solid rgba(255,255,255,.13);
  border-radius: 50%;
  right: -100px;
  bottom: -250px;
  box-shadow: 0 0 0 45px rgba(255,255,255,.035),
              0 0 0 90px rgba(255,255,255,.025);
}

.eyebrow {
  display: inline-block;
  padding: 7px 13px;
  border: 1px solid rgba(255,255,255,.25);
  border-radius: 30px;
  background: rgba(255,255,255,.09);
  font-size: 12px;
  font-weight: 700;
  letter-spacing: 1px;
  text-transform: uppercase;
}

.hero h1 {
  max-width: 780px;
  margin: 23px 0 17px;
  font-size: clamp(34px, 5.5vw, 60px);
  line-height: 1.12;
  letter-spacing: -2px;
}

.hero h1 span { color: #75d8ff; }

.hero p {
  max-width: 680px;
  color: #d8e9ff;
  font-size: 16px;
}

.hero-buttons {
  display: flex;
  flex-wrap: wrap;
  gap: 12px;
  margin-top: 29px;
}

.btn {
  display: inline-block;
  padding: 12px 20px;
  border-radius: 9px;
  font-size: 13px;
  font-weight: 750;
  transition: .2s ease;
}

.btn-primary {
  background: white;
  color: var(--blue);
}

.btn-outline {
  border: 1px solid rgba(255,255,255,.4);
  color: white;
}

.btn:hover { transform: translateY(-2px); }

/* Main sections */

.section { padding: 65px 0; }

.section-head {
  margin-bottom: 28px;
}

.section-head .label {
  color: var(--blue);
  font-size: 11px;
  font-weight: 850;
  letter-spacing: 2px;
  text-transform: uppercase;
}

.section-head h2 {
  margin: 5px 0 8px;
  font-size: clamp(25px, 3vw, 35px);
  letter-spacing: -.8px;
  color: var(--navy);
}

.section-head p {
  max-width: 720px;
  color: var(--muted);
  font-size: 14px;
}

.grid {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 18px;
}

.card {
  background: white;
  padding: 24px;
  border: 1px solid var(--border);
  border-radius: 15px;
  box-shadow: var(--shadow);
  transition: .25s ease;
}

.card:hover {
  transform: translateY(-4px);
  border-color: #b8d9ff;
}

.card-icon {
  display: grid;
  place-items: center;
  width: 43px;
  height: 43px;
  margin-bottom: 16px;
  border-radius: 12px;
  background: #eaf4ff;
  color: var(--blue);
  font-size: 21px;
}

.card h3 {
  margin-bottom: 8px;
  font-size: 16px;
  color: var(--navy);
}

.card p {
  font-size: 13px;
  color: var(--muted);
}

/* KPI definitions */

.kpi-grid {
  display: grid;
  grid-template-columns: repeat(5, 1fr);
  gap: 12px;
}

.kpi {
  padding: 20px 15px;
  border: 1px solid var(--border);
  border-radius: 13px;
  background: white;
}

.kpi .symbol {
  color: var(--blue);
  font-size: 21px;
}

.kpi h3 {
  margin: 10px 0 5px;
  font-size: 13px;
  line-height: 1.5;
}

.kpi p {
  color: var(--muted);
  font-size: 11px;
}

/* Dashboard preview */

.preview {
  padding: 25px;
  border-radius: 18px;
  border: 1px solid #d7e7fb;
  background: linear-gradient(140deg, #eaf4ff, #fff);
}

.preview-top {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 15px;
  margin-bottom: 20px;
}

.preview-top h3 {
  font-size: 17px;
  color: var(--navy);
}

.status {
  padding: 5px 10px;
  border-radius: 20px;
  background: #dff7ec;
  color: #167b50;
  font-size: 11px;
  font-weight: 800;
}

.preview-grid {
  display: grid;
  grid-template-columns: 1fr 1fr;
  gap: 14px;
}

.preview-item {
  background: white;
  padding: 18px;
  border: 1px solid var(--border);
  border-radius: 11px;
}

.preview-item h4 {
  font-size: 13px;
  margin-bottom: 6px;
}

.preview-item p {
  color: var(--muted);
  font-size: 12px;
}

/* Tech stack */

.tech-list {
  display: flex;
  flex-wrap: wrap;
  gap: 10px;
}

.tech {
  padding: 9px 15px;
  border: 1px solid #d7e5f7;
  border-radius: 8px;
  background: white;
  color: #24476e;
  font-size: 12px;
  font-weight: 750;
}

/* Steps */

.steps {
  display: grid;
  grid-template-columns: repeat(3, 1fr);
  gap: 18px;
}

.step-number {
  color: var(--blue);
  font-size: 12px;
  font-weight: 850;
  letter-spacing: 1px;
}

/* Footer */

.footer {
  padding: 35px 0;
  background: var(--navy);
  color: white;
}

.footer-inner {
  display: flex;
  justify-content: space-between;
  align-items: center;
  gap: 20px;
}

.footer p {
  color: #b7c9e3;
  font-size: 12px;
}

.footer strong { font-size: 15px; }

/* Responsive */

@media (max-width: 850px) {
  .kpi-grid { grid-template-columns: repeat(3, 1fr); }
  .grid, .steps { grid-template-columns: repeat(2, 1fr); }
  .nav-links { gap: 12px; }
}

@media (max-width: 560px) {
  .nav-inner { padding: 13px 0; align-items: flex-start; }
  .nav-links { flex-wrap: wrap; justify-content: flex-end; }
  .nav-links a { font-size: 11px; }
  .hero { padding: 65px 0; }
  .hero h1 { letter-spacing: -1px; }
  .grid, .steps, .preview-grid { grid-template-columns: 1fr; }
  .kpi-grid { grid-template-columns: repeat(2, 1fr); }
  .section { padding: 45px 0; }
  .footer-inner { flex-direction: column; align-items: flex-start; }
}
</style>
</head>

<body>

<nav class="navbar">
  <div class="container nav-inner">
    <a href="#" class="logo">HAIER <span>| PMC</span></a>
    <div class="nav-links">
      <a href="#overview">Overview</a>
      <a href="#features">Features</a>
      <a href="#technology">Technology</a>
      <a href="#usage">How to Use</a>
    </div>
  </div>
</nav>

<header class="hero">
  <div class="container">
    <span class="eyebrow">Power BI · Manufacturing Analytics</span>

    <h1>
      Material Shortage<br>
      <span>Dashboard</span>
    </h1>

    <p>
      A centralized analytics solution for material availability,
      shortage monitoring, inventory visibility, and production
      planning support in manufacturing operations.
    </p>

    <div class="hero-buttons">
      <a href="#overview" class="btn btn-primary">
        Explore Project ↓
      </a>
      <a href="#features" class="btn btn-outline">
        Dashboard Features
      </a>
    </div>
  </div>
</header>

<main>

<section class="section" id="overview">
  <div class="container">
    <div class="section-head">
      <span class="label">01 / Project Overview</span>
      <h2>Turning Material Data into Insights</h2>
      <p>
        This Power BI project helps planning and operations teams
        understand material requirements, available stock, shortage
        risks, and the areas requiring attention.
      </p>
    </div>

    <div class="grid">
      <article class="card">
        <div class="card-icon">◈</div>
        <h3>Material Visibility</h3>
        <p>Compare required quantities with available stock and identify potential material gaps.</p>
      </article>

      <article class="card">
        <div class="card-icon">◎</div>
        <h3>Shortage Monitoring</h3>
        <p>Analyze material shortages by priority, model, department, and reporting period.</p>
      </article>

      <article class="card">
        <div class="card-icon">↗</div>
        <h3>Production Support</h3>
        <p>Provide useful information for replenishment planning and production continuity.</p>
      </article>
    </div>
  </div>
</section>

<section class="section" style="background:#eaf2fc;">
  <div class="container">
    <div class="section-head">
      <span class="label">02 / Performance Indicators</span>
      <h2>Key Performance Indicators</h2>
      <p>
        The dashboard is designed to monitor these operational
        metrics. Actual results depend on the connected dataset.
      </p>
    </div>

    <div class="kpi-grid">
      <article class="kpi">
        <div class="symbol">▦</div>
        <h3>Total Required Qty</h3>
        <p>Material demand</p>
      </article>

      <article class="kpi">
        <div class="symbol">▣</div>
        <h3>Available Stock</h3>
        <p>Stock availability</p>
      </article>

      <article class="kpi">
        <div class="symbol">△</div>
        <h3>Shortage Quantity</h3>
        <p>Uncovered demand</p>
      </article>

      <article class="kpi">
        <div class="symbol">％</div>
        <h3>Overall Availability</h3>
        <p>Stock coverage ratio</p>
      </article>

      <article class="kpi">
        <div class="symbol">!</div>
        <h3>Critical Materials</h3>
        <p>Urgent material risks</p>
      </article>
    </div>
  </div>
</section>

<section class="section" id="features">
  <div class="container">
    <div class="section-head">
      <span class="label">03 / Analytical Features</span>
      <h2>Dashboard Capabilities</h2>
      <p>
        Interactive reporting views help users investigate shortages
        and understand material requirements across operations.
      </p>
    </div>

    <div class="grid">
      <article class="card">
        <div class="card-icon">▥</div>
        <h3>Requirements vs Stock</h3>
        <p>Compare required material quantities with stock on hand.</p>
      </article>

      <article class="card">
        <div class="card-icon">◉</div>
        <h3>Priority Analysis</h3>
        <p>Review shortage distribution and identify urgent materials.</p>
      </article>

      <article class="card">
        <div class="card-icon">↕</div>
        <h3>Top 10 Shortages</h3>
        <p>Rank materials by shortage quantity for focused review.</p>
      </article>

      <article class="card">
        <div class="card-icon">⌘</div>
        <h3>Model-Wise Analysis</h3>
        <p>Compare shortage exposure across different product models.</p>
      </article>

      <article class="card">
        <div class="card-icon">⌁</div>
        <h3>Shortage Trends</h3>
        <p>Monitor changes in requirements and shortage quantities over time.</p>
      </article>

      <article class="card">
        <div class="card-icon">▤</div>
        <h3>Shift & Department</h3>
        <p>Explore material requirements and shortages across shifts and departments.</p>
      </article>
    </div>
  </div>
</section>

<section class="section" style="padding-top:0;">
  <div class="container">
    <div class="preview">
      <div class="preview-top">
        <h3>Interactive Reporting Experience</h3>
        <span class="status">Power BI Project</span>
      </div>

      <div class="preview-grid">
        <div class="preview-item">
          <h4>Filter & Explore</h4>
          <p>Date range, shift, product category, model, material code, shortage status, priority, and department.</p>
        </div>

        <div class="preview-item">
          <h4>Identify Material Risks</h4>
          <p>Review critical shortages and focus attention on materials requiring corrective action.</p>
        </div>

        <div class="preview-item">
          <h4>Support Planning</h4>
          <p>Use material requirement and availability information to support replenishment decisions.</p>
        </div>

        <div class="preview-item">
          <h4>Review Operations</h4>
          <p>Compare material shortages across models, shifts, departments, and time periods.</p>
        </div>
      </div>
    </div>
  </div>
</section>

<section class="section" id="technology">
  <div class="container">
    <div class="section-head">
      <span class="label">04 / Technology Stack</span>
      <h2>Tools & Technologies</h2>
      <p>Technologies used or applicable to this Power BI analytics workflow.</p>
    </div>

    <div class="tech-list">
      <span class="tech">Microsoft Power BI</span>
      <span class="tech">Power Query</span>
      <span class="tech">DAX</span>
      <span class="tech">Data Modeling</span>
      <span class="tech">Microsoft Excel</span>
      <span class="tech">Data Visualization</span>
      <span class="tech">Business Intelligence</span>
    </div>
  </div>
</section>

<section class="section" id="usage" style="background:#eaf2fc;">
  <div class="container">
    <div class="section-head">
      <span class="label">05 / Getting Started</span>
      <h2>How to Use This Project</h2>
      <p>Follow these steps when the Power BI project files are available.</p>
    </div>

    <div class="steps">
      <article class="card">
        <div class="step-number">STEP 01</div>
        <h3 style="margin-top:10px;">Get the Files</h3>
        <p>Clone or download the repository containing the Power BI report and authorized dataset.</p>
      </article>

      <article class="card">
        <div class="step-number">STEP 02</div>
        <h3 style="margin-top:10px;">Open in Power BI</h3>
        <p>Open the .pbix report in Power BI Desktop and configure its data source if required.</p>
      </article>

      <article class="card">
        <div class="step-number">STEP 03</div>
        <h3 style="margin-top:10px;">Explore Insights</h3>
        <p>Refresh the data and use the available filters to investigate material shortage risks.</p>
      </article>
    </div>
  </div>
</section>

<section class="section">
  <div class="container">
    <div class="section-head">
      <span class="label">06 / Business Value</span>
      <h2>Designed for Better Decisions</h2>
      <p>
        The dashboard can improve material visibility, help prioritize
        shortages, support inventory planning, and facilitate coordination
        between procurement and production teams. Results depend on data
        accuracy and operational processes.
      </p>
    </div>

    <div class="card">
      <h3>Data Privacy & Disclaimer</h3>
      <p>
        This project is for portfolio, learning, and analytical
        demonstration purposes unless otherwise authorized. Remove
        confidential business information before publishing. Do not
        present sample data as verified company results or imply official
        company endorsement without permission.
      </p>
    </div>
  </div>
</section>

</main>

<footer class="footer">
  <div class="container footer-inner">
    <div>
      <strong>Haier PMC | Material Shortage Dashboard</strong>
      <p style="margin-top:7px;">Power BI · Manufacturing Analytics · Supply Chain</p>
    </div>

    <p>Developed by <strong>Nabeel Ahmad</strong></p>
  </div>
</footer>

</body>
</html>
