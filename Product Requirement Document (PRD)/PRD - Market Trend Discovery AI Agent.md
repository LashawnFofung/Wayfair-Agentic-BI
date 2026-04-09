# PRD: Market Trend Discovery AI Agent

### Summary

An autonomous trend-scraping AI agent that continuously monitors platforms like Pinterest, top design blogs, and retailers to identify the next "Hero" products for the home decor industry. The agent assigns Trend Confidence Scores using multi-source social signals, surfaces niche versus saturated trends, and provides actionable insights through automated PDF reports and a dynamic, live Google Sheets dashboard designed for internal team use. Target users include Inventory Planners, Trend Researchers, and SEO Specialists who rely on actionable early trend detection.

---

## Goals

### Business Goals

* Achieve an 80% reduction in manual trend and product research time for key teams.
* Realize 95% signal relevance, confirmed via internal audit of surfaced trends.
* Accelerate identification of "Hero" products before the broader market recognizes the trend.
* Improve inventory planning accuracy, reducing overstock and increasing timely stock of trending styles.

### User Goals

* Enable Inventory Planners to confidently stock trending materials (e.g., "washable," "terracotta") before they peak.
* Empower Trend Researchers to discover and categorize emerging niche styles early.
* Allow SEO Specialists to quickly surface and leverage trending keywords tied to product descriptions.

### Non-Goals

* Direct competitor price matching and pricing analysis (already handled by Agent 3).
* Building consumer-facing search or visualization features.
* Real-time product pricing data integration.

---

## User Stories

**Inventory Planner**

* As an Inventory Planner, I want to see a confidence score for specific material types (e.g., "Terracotta Rugs"), so that I can make bulk stocking recommendations with certainty.
* As an Inventory Planner, I want trend recommendations by product category, so that stocking decisions remain segmented and relevant to each line.

**Trend Researcher**

* As a Trend Researcher, I want to identify niche styles before they become mainstream, so that I can keep our catalog ahead of the market.
* As a Trend Researcher, I want to see each trend labeled as “Niche” or “Saturated”, so that I focus research effort where it matters most.

**SEO Specialist**

* As an SEO Specialist, I want to see trending keywords extracted from top-performing trend signals, so that I can update product descriptions accordingly.
* As an SEO Specialist, I want to view a “momentum” indicator for keywords, so that I prioritize SEO updates based on emerging trends.

---

## Functional Requirements

* **Data Ingestion (Priority: P0)**

  * Multi-source ingestion engine, pulling trend and product signals from Pinterest, design blogs, and retailer listings via Extern API.
  * Data siloed by category (e.g., Rugs, Lighting, Decor) to prevent trend cross-contamination and maintain analytics purity.

* **AI Analysis (Priority: P0)**

  * Categorization using Gemini 1.5 Flash—automated Niche vs. Saturated trend classification per signal.
  * Trend Confidence Score calculation, requiring aggregation from at least three distinct data sources per trend.

* **Reporting (Priority: P1)**

  * Automated PDF Trend Report generation, scheduled (weekly/monthly) and available on-demand.
  * PDF to include summary statistics, top trends by category, confidence scores, and niche/saturated breakdowns.

* **Dashboard (Priority: P1)**

  * Internal Google Sheets dashboard, auto-updating via API, reflecting the most recent dataset and insights.
  * Dashboard to feature: confidence scores, niche/saturated trend labeling, trending keywords for SEO, and clear segmentation by product category.

---

## User Experience

**Entry Point & First-Time User Experience**

* Users access the internal Google Sheets dashboard via shared company workspace (G Suite link).
* First-time users are greeted with an “About” tab explaining data sources, updating cadence, and how to use category filters.
* Brief tooltip-style onboarding highlights navigation, how to drill into product categories, and how to request on-demand PDF reports.

**Core Experience**

* **Step 1:** User opens the live dashboard and lands on the “Summary” tab, displaying top-trending products across all categories with associated confidence scores and niche/saturated labels.

  * Minimal friction via automatic login with company credentials.
  * Success: Users see the current snapshot without manual refresh; last updated timestamp is clearly presented.

* **Step 2:** User filters dashboard view by category (e.g., Rugs, Lighting) using a dropdown selector; all data instantly segments with no cross-category signal bleed.

  * Data validation prevents users from selecting irrelevant combinations.
  * Frozen column and header rows ensure consistent visibility of key context.

* **Step 3:** User clicks into a specific trend (e.g., “Terracotta Rugs”) to view:

  * Source breakdown (Pinterest, Blog, Retail).
  * Trend Confidence Score derivation, showing each source’s relative weight and any gaps.
  * Associated trending keywords with momentum indicators.
  * Historical movement over time.

* **Step 4:** User has two options for reporting:

  * Trigger on-demand PDF Trend Report (sent via email or downloadable link).
  * Passively receive automated weekly/monthly reports summarizing top changes and actionable insights.

**Advanced Features & Edge Cases**

* Manual override: Users can flag a trend as “Watch” (monitor more closely) or “Dismiss” (deprioritize).
* Handling of insufficient data: If fewer than 3 platform signals are available, dashboard surfaces a data sufficiency warning and disables confidence scoring for that trend.
* Stale data handling: If any category or overall dataset has not refreshed within set SLA (<5 minutes), a prominent warning is displayed.

**UI/UX Highlights**

* Color-coded confidence score tiers (High: green, Medium: yellow, Low: red).
* Frozen header rows for persistent access to field names and last-updated status.
* Dropdown selectors for fast filtering by category or trend status.
* Mobile-friendly view for on-the-go management.
* Accessibility: Sufficient color contrast, readable fonts, keyboard navigation, and screen reader support.

---

## Narrative

Trend Researcher Jamie wrestles daily with the explosion of product styles across Pinterest boards and endless design blogs. Tracking the next big thing—like whether “Terracotta Rugs” is another fleeting fad or a coming mainstay—requires hours of sifting, cross-comparison, and highly manual note-taking. Meanwhile, Inventory Planner Lee anxiously waits for a clear signal that it’s finally safe to recommend washable terracotta material for next quarter’s bulk order, while Sam in SEO itches for real data to power compelling product copy.

Enter the Market Trend Discovery AI Agent: Jamie launches the internal Google Sheets dashboard and is greeted by a refreshed, color-coded landscape of products—trends parsed, scored, and explained. “Terracotta Rugs” surfaces with a High Confidence score, categorized as “Niche” across Pinterest, recent blogs, and select retailer sources—each weighted and timestamped for transparency. With one click, Jamie reviews momentum keywords and flags the trend as “Watch” for follow-up.

Lee quickly pivots, confident enough to add terracotta material to the inventory slate early—beating slower competitors. Sam, the SEO Specialist, grabs the surge in “washable terracotta” as a keyword, updating site copy for the season’s best chances. What once involved days of scattered research and gut instinct now happens in minutes. The business rides the crest of the trend wave, capturing early demand, minimizing overstock, and learning—week by week—where to double down next.

---

## Success Metrics

### User-Centric Metrics

* 80% reduction in time spent on manual trend research, measured via pre/post internal time tracking.
* Internal team user satisfaction score ≥ 4/5 (quarterly pulse survey after product launch).
* Frequency of on-demand report requests and dashboard filter use.

### Business Metrics

* Percentage of “Hero” products identified via the tool before external market peak.
* Inventory accuracy improvement year-over-year in categories supported by the tool.
* Reduction in overstock/outdated inventory for products flagged as “Saturated.”

### Technical Metrics

* 95% of surfaced trend signals demonstrated relevant context in spot-audit reviews.
* Dashboard refresh latency consistently below 5 minutes after data ingestion.
* 100% successful PDF report generation (monitored via delivery and error logs).

### Tracking Plan

* Number of dashboard opens per user and across team.
* Frequency of filter use by category/trend type.
* Volume and accuracy rate of on-demand PDF reports.
* User engagement with confidence scores (“views per trend”).
* Manual override/flag actions logged and reviewed for QA.

---

## Technical Considerations

### Technical Needs

* Extern API: Multi-source trend and product signal ingestion from Pinterest, blogs, and retailer feeds.
* Gemini 1.5 Flash: Automated analysis for Niche vs. Saturated, confidence scoring, and keyword extraction.
* Google Sheets API: For real-time, live data dashboard population and updating.
* PDF Generation Service: Automated creation and email delivery/storage of Trend Reports.
* Scheduled job runner: Ensures timely report creation and data refreshing.

### Integration Points

* Extern API for primary data ingestion.
* Google Sheets API for dashboard output.
* Gemini 1.5 Flash for in-line trend analysis and scoring.
* PDF rendering engine for reporting.
* Email or Cloud Storage system for distributing PDF reports.

### Data Storage & Privacy

* Trend data isolated in silos per product category to guarantee analytical integrity.
* No cross-category data sharing (e.g., Rug trends cannot pollute Lighting analytics).
* All datasets restricted to internal team access through Google Workspace.
* Data retention policy set for periodic deletion—stale signals purged quarterly.

### Scalability & Performance

* Dashboard designed to auto-update within 5 minutes of new data signal ingestion.
* System must handle addition of product categories and new data feeds with no notable performance drop.
* Supports up to dozens of concurrent team users for dashboard/reporting access.

### Potential Challenges

* Signal noise from low-quality or irrelevant sources could dilute confidence accuracy; requires automated and manual QA controls.
* Maintaining the purity of data silos as new product categories roll out over time.
* Gemini API rate limits or outages could impact daily analysis (risk management needed for bulk operations).

---

## Milestones & Sequencing

### Project Estimate

* Total: Large (2 weeks).

### Team 

* My Role
  * PM/TPM 
  * Engineer: backend (API/AI integration), dashboard/front-end (Google Sheets, PDF report integration)
  * Designer/Analyst (for report template polishing and narrative QA)

### Suggested Phases

**Phase 1: Data Ingestion & Category Silos (Weeks 1–2)**

* Key Deliverables: Backend engineer—data pipeline via Extern API, initial category siloing, Gemini 1.5 Flash integration for basic trend categorization.
* Dependencies: Extern API access; basic design guide for dashboard fields.

**Phase 2: Core Scoring Engine & Dashboard v1 (Weeks 1-2)**

* Key Deliverables: Backend + front-end engineers—trend confidence calculation logic (min 3 sources per signal), preliminary live Google Sheets dashboard, working category filters, Niche/Saturated labeling.
* Dependencies: Phase 1 ingestion completion.

**Phase 3: Reporting & Dashboard Refinement (Weeks 2)**

* Key Deliverables: Engineer + part-time designer—working PDF report generator (scheduled/on-demand), dashboard UI polish, keyword trending module for SEO.
* Dependencies: Scoring and dashboard live (Phase 2).

**Phase 4: QA, Testing, Rollout (Weeks 2)**

* Key Deliverables: All—signal relevance QA (target 95% audit hit rate), end-to-end dashboard/PDF tests, onboarding guides, internal launch.
* Dependencies: Completion of all product features and systems operational.

---
