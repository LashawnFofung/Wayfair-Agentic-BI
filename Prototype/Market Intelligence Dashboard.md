## Wayfair Agentic BI: Market Intelligence Dashboard

**Role:** Technical Product Manager & AI Engineer

**Frameworks:** CIRCLES Method™, North Star Metric, n8n Orchestration

  <h1></h1>
  
### Summary
This repository contains the architecture and strategic documentation for a suite of autonomous AI Agents designed to revolutionize Wayfair’s market positioning. By automating visual conceptualization, trend discovery, and competitive benchmarking, this ecosystem reduces the "Time-to-Insight" from 15+ hours to under 60 seconds.

 <h1></h1>
 
### 🛠️ The Architecture
The system is built on a self-hosted n8n instance running on Docker, utilizing Gemini 2.0 for cognitive reasoning and FLUX for visual synthesis.

 <h1></h1>
 
### The Three Core Agents
1.	Moodboard AI Agent: Converts abstract style descriptors into high-fidelity visual assets and material palettes.
2.	Market Trend Discovery Agent: Ingests social/blog signals to identify emerging "Hero" products before they manifest in sales data.
3.	Competitor Monitoring Agent: A dual-path scraper that normalizes data from Amazon and Walmart to identify pricing whitespace.

  <h1></h1>
  
### 🎨 Prototype: Market Intelligence Dashboard
As a TPM, I believe in functional prototyping. Below is a high-fidelity wireframe built in HTML/CSS.
How to view the Prototype:
To ensure this repository remains lightweight and "live," I have encoded the UI prototype into a Base64 string. This allows for a zero-dependency, instant-load visualization of the TPM vision.
Instructions:
1.	Copy the Base64 string from the /prototypes/dashboard_b64.txt file in this repo.
2.	Paste it into any Base64-to-HTML decoder or use it as a Data URL in your browser: data:text/html;base64,[STRING_HERE]

  <h1></h1>
  
### 📋 PRD Case Study: The CIRCLES Method™

I applied the CIRCLES Method to ensure every technical node served a business requirement.

| Stage | Activity | Result for Wayfair Agent |
| :--- | :--- | :--- |
| **C** | **Comprehend** the Situation | Identified a 3-month lag in traditional sales data vs. social trends. |
| **I** | **Identify** the Customer | **Primary:** Inventory Planners; **Secondary:** Pricing Analysts. |
| **R** | **Report** Customer Needs | Needs "Clean Data" and "Confidence Scores" to justify stock increases. |
| **C** | **Cut** through Prioritization | Prioritized **Dual-Path Scrapers** to handle Amazon's complex HTML. |
| **L** | **List** Solutions | Engineered modular n8n workflows for automated data ingestion. |
| **E** | **Evaluate** Trade-offs | Chose **Gemini 1.5 Flash** for speed vs. **Gemini 2.0** for reasoning. |
| **S** | **Summarize** Recommendation | Deploy a unified dashboard for real-time strategy recommendations. |
 
  <h1></h1>

### 📉 Success Metrics (North Star)
My North Star Metric for this project is Time-to-Insight (TTI).
- **Pre-Agent Baseline:** ~900 minutes (Manual research/scraping/design).
- **Post-Agent Performance:** ~1 minute (Fully automated orchestration).
- **ROI:** 99.8% reduction in labor latency.

   <h1></h1>
   
### 🧠 Technical Case Study: "Architect of Intelligence"
"Building the Dual-Path Amazon scraper made me realize how to structure inputs so the AI isn't just summarizing but identifying competitive whitespaces. It was a shift from being a 'tool user' to being an Architect of Intelligence." — Lashawn Fofung

<br>

### Key Engineering Wins:
- **Normalization Logic:** Used Regex and Custom JavaScript to clean inconsistent HTML strings (e.g., "$189.00") into numeric floats for delta calculations.
- **Orchestration:** Built complex branching logic in n8n to handle "Product" vs. "Collection" URL paths without schema breakage.
- **Vision Integration:** Successfully mapped LLM-refined prompts to the FLUX API for professional-grade moodboard generation.

   <h1></h1>

