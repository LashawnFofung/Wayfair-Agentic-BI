# PRD: Competitor Monitoring AI Agent

### Summary

The Competitor Monitoring AI Agent is an automated tool that scrapes Amazon and Walmart daily to uncover pricing gaps and product whitespace, empowering Wayfair’s pricing and category teams to make real-time decisions. As Step 3 of a five-part AI pipeline (Moodboard → Trend Discovery → Competitor Monitoring → AI Insights → Dashboard), this agent automates the generation of 'Match/Beat/Pivot' recommendations via Gemini, replacing slow, manual weekly audits and accelerating Wayfair’s competitive pricing strategy.

---

## Goals

### Business Goals

* Reduce pricing audit cycle from weekly to daily to improve responsiveness.
* Increase percentage of days Wayfair holds the Lowest Price badge on strategic SKUs.
* Identify and leverage competitor out-of-stock (OOS) events for Wayfair product pushes.
* Provide high-quality structured data for downstream agents (AI Insights and Dashboard).
* Ensure reliable monitoring with 0% schema breakage across Amazon and Walmart.

### User Goals

* Pricing Analysts effortlessly access up-to-date price comparisons and badge status by SKU and category.
* Category Managers are proactively alerted to competitor OOS events, enabling rapid decisions to promote Wayfair alternatives.
* Technical Product Owners have comprehensive oversight into pipeline health, schema consistency, and run integrity—without manual intervention.

### Non-Goals

* No direct price changes are made in the live Wayfair CMS (recommendations only).
* No scraping or monitoring of retailers beyond Amazon and Walmart in v1.
* No front-end user interface; all outputs delivered as structured HTML and PDF to Google Drive.

---

## User Stories

### Pricing Analyst

* As a Pricing Analyst, I want to see price comparisons for “5x7 Shag Rugs” across Amazon, Walmart, and Wayfair, so that I can quickly spot and address pricing gaps.
* As a Pricing Analyst, I want to know which SKUs have lost the Lowest Price badge, so that I can prioritize pricing actions.
* As a Pricing Analyst, I want output data in clean numeric formats (e.g., price as float), so that I can use the numbers directly in calculations.

### Category Manager

* As a Category Manager, I want to be alerted when competitor SKUs go OOS, so that I can promote relevant Wayfair alternatives for those items.
* As a Category Manager, I want to identify whitespace opportunities by category when competitors lack assortment.

### Technical Product Owner

* As a Technical Product Owner, I want to monitor scraper success, run logs, and health status, so that I can proactively address any failures.
* As a Technical Product Owner, I want to be notified if schema changes break the pipeline for any retailer, so that I can quickly troubleshoot.
* As a Technical Product Owner, I want comprehensive run logs with SKU counts, error rates, and stepwise status.

---

## Functional Requirements

* **Scraping Engine (Priority: High)**

  * Dual-path scraping logic for both Product URLs and Collection/Category URLs to accommodate different data structures.
  * Implementation of stealth headers and anti-bot techniques to reduce blocking by Amazon/Walmart.
  * Support for processing a minimum of 100 SKUs per scheduled run for both retailers.

* **Data Normalization (Priority: High)**

  * Custom JS/Regex normalization layer to parse price strings (e.g., “$120.00”) into float format (120.00).
  * Detection and standardization of Out-of-Stock (OOS) flags and missing or variant data fields.
  * Schema mapping to ensure consistency across retailer sources.

* **AI Recommendation Engine (Priority: High)**

  * Integration with Gemini to generate 'Match' (price parity), 'Beat' (undercut competitor by dynamic or fixed threshold), and 'Pivot' (suggest Wayfair alternatives on competitor OOS) recommendations.
  * Each SKU receives a recommendation based on up-to-date scraped data.

* **Output & Delivery (Priority: Medium)**

  * Export of structured data as both HTML and PDF reports to Google Drive, formatted for human readability and dashboard ingestion.
  * Seamless handoff of normalized data for use in downstream Step 4 (AI Insights) and Step 5 (Dashboard) agents.

---

## User Experience

**Entry Point & First-Time User Experience**

* The Technical Product Owner configures the scheduled run time or triggers the agent manually.
* First-time setup includes specifying source URLs/SKUs and Google Drive credentials.
* Minimal onboarding; documentation includes a sample SKU list, output format, and run instructions.

**Core Experience**

* **Step 1:** User (TPO) provides or confirms SKU/category URL list for the next scheduled run.
  * Input validation for URLs, duplicate detection, and category coverage.
  * UI: command-line or script configuration file (no live UI).
* **Step 2:** Agent initiates dual-path scraping:
  * Product URLs routed through product-specific logic.
  * Collection/Category URLs handled with pagination for batch product discovery.
  * Real-time error/log reporting for unreachable URLs or detection of bot defenses.
* **Step 3:** Data Normalization passes:
  * Price strings extracted and normalized to float.
  * OOS and missing fields flagged, schema mapped.
  * Structured JSON output.
* **Step 4:** Gemini AI engine ingests normalized data and issues 'Match', 'Beat', or 'Pivot' recommendations per SKU.
  * 'Beat' logic configurable as fixed % (default: 5%) or dynamic (future enhancement).
  * 'Pivot' recommends Wayfair alternatives for competitor OOS SKUs (if available).
* **Step 5:** Output reporting:
  * Human-readable HTML/PDF output with columns: SKU, Category, Wayfair Price, Amazon Price, Walmart Price, Delta, Badge Status, Recommendation.
  * Report auto-delivered to Google Drive, path and naming consistent for downstream pipeline.
  * Log files generated with run details, error counts, and schema validation outcome.

**Advanced Features & Edge Cases**

* Schema breakage detected: affected SKU skipped, TPO receives email/alert, run continues with unaffected SKUs.
* High-volume runs: batch management with partial retries and error isolation.
* OOS alternatives: where unavailable, 'Pivot' noted as 'No alternative found.'
* Report exports retried up to three times on transient Google Drive upload failures.

**UI/UX Highlights**

* Reports must be clearly organized by SKU, include color-coded status/recommendation labels, and support accessibility standards (font, color contrast).
* Output format is strictly tabular for easy review and dashboard ingestion.

---

## Narrative

Maya, a diligent Pricing Analyst at Wayfair, used to spend hours each Monday manually checking Amazon and Walmart for price changes on her most important rug SKUs. She’d navigate to dozens of product pages, copy price strings into spreadsheets, clean the data, and compare it against Wayfair prices—only to realize by Wednesday that a key competitor had been undercutting her prices all along. By then, Wayfair had already lost the coveted Lowest Price badge for days.

With the Competitor Monitoring AI Agent in place, Maya’s workflow is transformed. Every morning at 6am, the AI agent automatically scrapes Amazon and Walmart for the latest pricing and stock positions, normalizes the data, and generates ‘Match/Beat/Pivot’ recommendations using Gemini. By the time Maya opens her email at 8am, a Google Drive report awaits her: every SKU, color-coded deltas, clear badge status flags, and immediate alerts for any that demand attention.

Meanwhile, James, the Category Manager, sees that a leading competitor’s 5x7 Shag Rug is now out of stock. The report flags the opportunity, and suggests three Wayfair alternatives to push in real time. The technical product owner scans the run log—zero errors, zero schema breaks, no surprises. The result: Pricing and category teams recapture the badge faster, whitespace gets filled the same day, and the business is more agile than ever.

---

## Success Metrics

### User-Centric Metrics

* **Time-to-flag competitor price change:** Average time from competitor price move to report flagging (baseline: 7 days, target: <24 hours).
* **Pricing Analyst adoption rate:** Number of analysts using the reports weekly within first 30 days (target: 3+).
* **Category Manager action rate:** Number of OOS-driven Wayfair alternative pushes per month.

### Business Metrics

* **Lowest Price badge coverage:** % of time monitored SKUs keep the Lowest Price badge (target: improve by 15% in 60 days).
* **Frequency of whitespace detection:** Unique whitespace (OOS) events surfaced per category per month.

### Technical Metrics

* **SKUs processed per run:** Minimum 100+ SKUs/run; target to scale to 500+.
* **Schema breakage rate:** 0% runs with schema error on Amazon/Walmart.
* **Pipeline uptime:** >99% on scheduled runs.
* **Error rates:** Number and type of errors per run (to be minimized).

### Tracking Plan

* SKU count and coverage per run
* Error count and error types per run
* Distribution of recommendations (Match/Beat/Pivot %)
* Google Drive export success/failure logs
* Run duration/time per batch

---

## Technical Considerations

### Technical Needs

* **Scraping Engine:** Dual-path logic for Product and Collection/Category URLs across two retailer schemas.
* **Normalization Layer:** Custom Javascript/Regex routines to standardize and clean data across formats.
* **Gemini Integration:** Consumption of Gemini AI recommendations per normalized SKU batch.
* **Output Pipeline:** Automated export routines utilizing Google Drive APIs for HTML/PDF delivery.
* **Logging:** End-to-end logging with error capture; alerts for pipeline failures/schema changes.

### Integration Points

* **Upstream:** Receives prioritized SKUs/categories from Step 2 (Trend Discovery Agent).
* **Downstream:** Delivers structured, normalized SKU recommendation data to Step 4 (AI Insights) and Step 5 (Dashboard and auto-updating Google Sheets).

### Data Storage & Privacy

* Scraped data is retained *only* for the duration of report generation and delivery.
* No personally identifiable information (PII) handled at any step.
* Data is exported to Wayfair-controlled Google Drive; local files purged post-run.
* Compliance with Amazon/Walmart ToS flagged as an operational/legal risk.

### Scalability & Performance

* Architecture supports batch processing for 100+ SKUs/run at launch, with targeting of 500+ SKUs in v2.
* Scraping and normalization are parallelizable across categories/SKUs.
* Performance monitoring for bottlenecks in scraping, normalization, or Gemini response time.

### Potential Challenges

* **Bot detection/IP blocking:** Ongoing need to update headers, pacing, and proxy rotation to avoid blocks.
* **Retailer schema volatility:** Regular updates required to handle changed HTML/CSS structures.
* **AI recommendation accuracy:** Dependent on high data cleanliness.
* **API rate limits and transient upload failures.**

---

## Milestones & Sequencing

### Project Estimate

* **Medium:** 2 weeks for v1 launch.

### Team 

* My Role:
  * Engineer (responsible for scraper, normalization, and output)
  * Technical Product Manager (pipeline design, QA, reporting, handoff)

### Suggested Phases

**Phase 1 — Scraper + Normalization (Week 1–2)**

* Key Deliverables: Engineer builds dual-path scraper, integrates stealth headers, implements normalization routines; output validated on 20 test SKUs.
* Dependencies: Access to target Amazon and Walmart URLs/SKUs.

**Phase 2 — Gemini Integration + Output (Week 1-2)**

* Key Deliverables: Engineer and TPM integrate Gemini AI logic, develop Google Drive export functionality; QA on 100 SKUs in end-to-end test.
* Dependencies: Gemini API key, Google Drive API credentials.

**Phase 3 — Pipeline Hardening + Handoff (Week 2)**

* Key Deliverables: Engineer implements error handling for schema changes, builds comprehensive run logs, TPM finalizes intake/output schema for Step 4 and 5 handoff.
* Dependencies: Step 4/5 teams confirm downstream data format; documentation and runbook completed.

---
