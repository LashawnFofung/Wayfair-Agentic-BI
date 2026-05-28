# PRD: AI Insights & Content Generation Agent




## Summary
The AI Insights & Content Generation Agent is an automated workflow engine that ingests qualitative market trends and competitive landscape data to dynamically generate brand-aligned, multi-channel marketing copy and structured design visual asset recommendations. As Step 4 of a five-part AI business intelligence pipeline (Moodboard → Trend Discovery → Competitor Monitoring → AI Insights → Dashboard), this agent translates raw, multi-source intelligence into high-converting marketing campaigns. Utilizing an automated n8n workflow orchestrated by Mistral AI, it replaces manual copywriting and creative brainstorming cycles, ensuring Wayfair rapidly capitalizes on market whitespace and shifting consumer demands.


## Goals

### Business Goals
- Accelerate Go-to-Market Copywriting: Compress the campaign creative brief lifecycle from 5 business days down to minutes.
- Eliminate AI Jargon / Enforce Tone Integrity: Ensure 100% adherence to Wayfair's distinct brand voice and specific style personas while filtering out repetitive "corporate fluff".
- Scale Multi-Channel Content Output: Automate simultaneous generation of cross-channel collateral (Editorial strategies, Instagram captions, Email marketing headers) from a single analytical report upload.
- Fuel Graphic Design Pipelines: Supply concrete, structured spatial, color, and tactile descriptions (mood_board_assets) to cross-functional visual layout engines.

<br>

### User Goals
- Content Strategists & Copywriters easily input trend parameters and immediately acquire high-converting, targeted copy options mapping to distinct aesthetic archetypes.
- Creative Directors seamlessly change style aesthetics or tone restrictions without modifying underlying application code.
- Marketing Managers quickly extract pre-formatted creative headlines and caption variations to execute rapid multi-variant social media test campaigns.

<br>

### Non-Goals
- No automatic publishing of copy variants directly to live social channels or production CMS systems (recommendations and generation exports only).
- No image rendering or asset generation within this iteration (v1 strictly delivers textual copy and structured hexadecimal styling schemas).
- No intake processing of unstructured raw audio/video trend streams (input data must be clean, structured text or pre-extracted HTML files).

<br>

## User Stories
Content Strategist
As a Content Strategist, I want to upload Project 2 Trend Discovery and Project 3 Competitor reports so that the model extracts actionable data without manual copy-pasting.
As a Content Strategist, I want to specify a "Style Persona" (e.g., Earthy Organic, Minimalist, Maximalist) so that the generated copy aligns perfectly with specific micro-trends and design styles.
As a Content Strategist, I want an "Anti-AI-ism Filter" applied to all outputs so that I don't waste time editing out generic corporate fluff or cliche phrases like "elevate your space."
Marketing Manager
As a Marketing Manager, I want a dedicated interactive component with one-click copy utilities for generated social media captions, headlines, and sub-headers so that I can rapidly spin up channel testing variables.
As a Marketing Manager, I want to dynamically update the execution or workflow readiness status of various copy components (To Do, Drafting, Ready) inside my dashboard view to track campaign preparation.
Functional Requirements
1. Ingestion & File Extraction (Priority: High)
HTML Stripping Engine: Core workflow node must receive raw web or report uploads (Project 2 and Project 3 artifacts) and systematically purge markup tags, rendering clean plain text strings for downstream context ingestion.
Multi-Variable Form Interface: The workflow entry interface must host dropdown controls for Style Persona profiles alongside an open text field for custom comma-separated Vibe Keywords.
2. Orchestrated Prompt & Anti-AI Guardrails (Priority: High)
Role-Based Execution: Integrates mistral-large-latest via an overarching systemic prompt establishing the model as an expert, highly refined senior content strategist at Wayfair.
Enforced JSON Structuring: The LLM prompt must contain strict formatting parameters requiring a non-negotiable JSON output schema including keys for editorial_strategy, instagram_caption, email_header, and a nested mood_board_assets array.
Lexicon Negative Restrictions (Anti-AI-ism Filter): Outlaws specific phrases, forbidding terms such as "elevate your space", "sanctuary", "game changer", or "redefine your home".
3. Front-End Content Delivery Engine (Priority: Medium)
Tabbed Interface Dashboard: Converts standard layout blocks into a 3-tab front-end browser view structured across Strategy, Design, and Creative modules.
Status Tracking Widgets: Uses local web storage variables to preserve user dropdown updates to workflow status states (To Do, Drafting, Ready).
Clipboard Interactivity: Employs explicit JavaScript handlers to allow users to copy generated marketing text immediately upon clicking.
User Experience
Entry Point & First-Time User Experience
Users navigate to the self-hosted n8n webhook link or configured browser web form.
The interface displays simple fields to upload background HTML data reports, select targeted Style Personas, and inject custom contextual keywords.
Core Experience Flow
[User Form Entry] ➔ [n8n Text Extraction] ➔ [Mistral LLM Execution] ➔ [JSON Schema Check] ➔ [Tabbed Dashboard Render]
Step 1: Input Parameter Selections: User loads source HTML trend files, picks a Persona (e.g., Maximalist), inputs a keyword like "velvet texture", and hits submit.
Step 2: Workflow Extraction: The n8n automation pipeline parses the input documents and strips out boilerplate report scripts or formatting wrappers.
Step 3: Guardrail Enforcement: The context string plus custom persona variables enter the Mistral model node under the constraints of the Anti-AI-ism filter.
Step 4: Layout Materialization: The JSON output passes down to an HTML template node that builds a responsive, stylized, multi-channel marketing dashboard.
Step 5: Output Review & Asset Capture: The user clicks through functional dashboard tabs, modifies status dropdowns, copies copy blocks to their clipboard, or outputs the layout as a PDF presentation report using native browser print styles.
Advanced Features & Edge Cases
JSON Validation Defect Handling: If the LLM produces corrupted JSON notation, the workflow falls back to a structural parsing safeguard that auto-formats or safely captures unparsed text blocks to avoid complete layout collapse.
Empty Visual Array Handling: When the prompt fails to extract valid hex color schemes or physical texture tokens, the system injects default baseline Wayfair asset codes to keep visual cards readable.
Narrative
Elena, a Digital Content Planner at Wayfair, sits down on Thursday morning to structure next week's micro-campaign on trend-forward accent pieces. She has the text outputs from the Trend Discovery and Competitor Monitoring teams, but digging through the metric spreadsheets and HTML tables to find actionable visual cues takes her hours. Furthermore, drafting tailored variations across several channel formats often forces her into a repetitive loop of uninspired corporate copywriting.
Elena opens the AI Insights & Content Generation Agent dashboard. She uploads the raw report files, sets her target Style Persona dropdown to "Earthy Organic," and types "terracotta, handcrafted" into the custom vibe keyword block. She clicks generate.
Behind the scenes, the n8n pipeline processes her parameters, cleans the report markup, and sends the prompt payload to Mistral. Mistral, operating under a strict anti-cliche filter, ignores standard boilerplate expressions and designs a curated strategy card.
Within ninety seconds, Elena's screen refreshes into a dashboard. Under the Creative tab, she discovers an Instagram copy option that reads cleanly and avoids generic corporate buzzwords. Under the Design tab, a dedicated layout displays an asset palette complete with specific interior styling directions and hex color swatches ready to send to the design studio. Elena switches a card's status flag from To Do to Ready, clicks a button to copy the caption, pastes it directly into her scheduling queue, and prints the layout as a polished PDF report for her creative director's afternoon sync.
Success Metrics
User-Centric Metrics
Content Assembly Speed: Reduce time spent drafting channel copy variations from hours to under 3 minutes per campaign.
UX Copy and Paste Engagement: Rate of user clicks on the dynamic dashboard copy-to-clipboard elements.
Content Persona Variety: Multi-persona execution frequency across team analysts (target: regular utilization of at least 3 distinct style profiles monthly).
Business & Workflow Metrics
AI Output Quality Acceptance Rate: Percentage of generated marketing copy requiring zero additional manual text removal post-generation (target: >85%).
Structured Visual Integration: Number of generation outputs successfully outputting accurate mood_board_assets blocks.
Schema Integrity Validation Rate: Rate of automated text passes converting into valid JSON objects without downstream failure (target: 100%).
Technical Considerations
Technical Needs
AI Orchestration Framework: n8n workflow software configured with active HTTP webhooks and functional data injection properties.
LLM API Endpoints: Stable access to the Mistral AI API platform utilizing the mistral-large-latest inference model.
Web UI Formatting Infrastructure: Core knowledge of semantic HTML5 layouts, embedded responsive CSS styles, and structural JavaScript code blocks.
Integration Points
Upstream Handoff: Ingests structural text components, volume indicators, and pricing opportunities outputted by Step 3 (Competitor Monitoring).
Downstream Integration: Supplies clean HTML data structures and color palette definitions to enrich the Step 5 consolidated Market Intelligence Dashboard interface.
Storage, Performance & Privacy
Transient Session Architecture: Generated campaign data is mapped instantly to the client's localized view engine; persistent user telemetry isn't collected, ensuring complete internal corporate security.
Browser Data Lifecycle: Interface state tracking markers (To Do / Drafting) rely exclusively on the client web browser's local storage environment, bypassing backend database complexity.
Execution Latency Requirements: Complete analytical parsing and layout delivery operations must finish within a maximum system runtime limit of 15 seconds per call.
Milestones & Sequencing
Project Estimate
Duration: 1 Week (Optimized, focused sprint framework).
Team Allocation
Lead AI Engineer: Builds n8n workflows, optimizes system logic prompts, and implements JSON structuring filters.
Front-End UX Developer: Creates response dashboards, integrates functional interactive widgets, and structures print styling behaviors.
Suggested Phases
Phase 1: Ingestion Architecture & Prompt Conditioning
Key Deliverables: Establish working n8n file ingestion nodes. Configure the Mistral prompt block with the persona rules engine and anti-cliche filters.
Dependencies: Configured and active Mistral AI API keys.
Phase 2: Interface Integration & Functional Testing
Key Deliverables: Embed JSON responses directly into tabbed HTML dashboards. Integrate clipboard copy buttons and localized status dropdown triggers.
Dependencies: Clean, error-free JSON outputs generated by Phase 1 workflow models.
Phase 3: Validation, Hardening & Pipeline Deployment
Key Deliverables: Run multi-variant stress tests against corrupt JSON arrays. Validate dashboard scaling and layout structure on cross-functional devices. Complete all system deployment documentation.
Dependencies: Step 5 team alignment on upstream schema expectations.
