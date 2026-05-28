# PRD: AI Insights & Content Generation Agent




## Summary
The AI Insights & Content Generation Agent is an automated workflow engine that ingests qualitative market trends and competitive landscape data to dynamically generate brand-aligned, multi-channel marketing copy and structured design visual asset recommendations. As Step 4 of a five-part AI business intelligence pipeline (Moodboard → Trend Discovery → Competitor Monitoring → AI Insights → Dashboard), this agent translates raw, multi-source intelligence into high-converting marketing campaigns. Utilizing an automated n8n workflow orchestrated by Mistral AI, it replaces manual copywriting and creative brainstorming cycles, ensuring Wayfair rapidly capitalizes on market whitespace and shifting consumer demands.


## Goals

### Business Goals
- <b>Accelerate Go-to-Market Copywriting:</b> Compress the campaign creative brief lifecycle from 5 business days down to minutes.
- <b>Eliminate AI Jargon / Enforce Tone Integrity:</b> Ensure 100% adherence to Wayfair's distinct brand voice and specific style personas while filtering out repetitive "corporate fluff".
- <b>Scale Multi-Channel Content Output:</b> Automate simultaneous generation of cross-channel collateral (Editorial strategies, Instagram captions, Email marketing headers) from a single analytical report upload.
- <b>Fuel Graphic Design Pipelines:</b> Supply concrete, structured spatial, color, and tactile descriptions (mood_board_assets) to cross-functional visual layout engines.

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

### Content Strategist
- As a Content Strategist, I want to upload Project 2 Trend Discovery and Project 3 Competitor reports so that the model extracts actionable data without manual copy-pasting.
- As a Content Strategist, I want to specify a "Style Persona" (e.g., Earthy Organic, Minimalist, Maximalist) so that the generated copy aligns perfectly with specific micro-trends and design styles.
- As a Content Strategist, I want an "Anti-AI-ism Filter" applied to all outputs so that I don't waste time editing out generic corporate fluff or cliche phrases like "elevate your space."

<br>

### Marketing Manager
- As a Marketing Manager, I want a dedicated interactive component with one-click copy utilities for generated social media captions, headlines, and sub-headers so that I can rapidly spin up channel testing variables.
- As a Marketing Manager, I want to dynamically update the execution or workflow readiness status of various copy components (To Do, Drafting, Ready) inside my dashboard view to track campaign preparation.

<br>

## Functional Requirements
<b>1. Ingestion & File Extraction (Priority: High)</b>
  - <b>HTML Stripping Engine:</b> Core workflow node must receive raw web or report uploads (Project 2 and Project 3 artifacts) and systematically purge markup tags, rendering clean plain text strings for downstream context ingestion.
  - <b>Multi-Variable Form Interface:</b> The workflow entry interface must host dropdown controls for Style Persona profiles alongside an open text field for custom comma-separated Vibe Keywords.

<br>

<b>2. Orchestrated Prompt & Anti-AI Guardrails (Priority: High)</b>
  - <b>Role-Based Execution:</b> Integrates mistral-large-latest via an overarching systemic prompt establishing the model as an expert, highly refined senior content strategist at Wayfair.
  - <b>Enforced JSON Structuring:</b> The LLM prompt must contain strict formatting parameters requiring a non-negotiable JSON output schema including keys for editorial_strategy, instagram_caption, email_header, and a nested mood_board_assets array.
  - <b>Lexicon Negative Restrictions (Anti-AI-ism Filter):</b> Outlaws specific phrases, forbidding terms such as "elevate your space", "sanctuary", "game changer", or "redefine your home".

<br>

<b>3. Front-End Content Delivery Engine (Priority: Medium)</b>
  - <b>Tabbed Interface Dashboard:</b> Converts standard layout blocks into a 3-tab front-end browser view structured across Strategy, Design, and Creative modules.
  - <b>Status Tracking Widgets:</b> Uses local web storage variables to preserve user dropdown updates to workflow status states (To Do, Drafting, Ready).
  - <b>Clipboard Interactivity:</b> Employs explicit JavaScript handlers to allow users to copy generated marketing text immediately upon clicking.

<br>

## User Experience

### Entry Point & First-Time User Experience
  - Users navigate to the self-hosted n8n webhook link or configured browser web form.
  - The interface displays simple fields to upload background HTML data reports, select targeted Style Personas, and inject custom contextual keywords.

<br>

### Core Experience Flow

[User Form Entry] ➔ [n8n Text Extraction] ➔ [Mistral LLM Execution] ➔ [JSON Schema Check] ➔ [Tabbed Dashboard Render]

- <b>Step 1: Input Parameter Selections:</b> User loads source HTML trend files, picks a Persona (e.g., Maximalist), inputs a keyword like "velvet texture", and hits submit.
- <b>Step 2: Workflow Extraction:</b> The n8n automation pipeline parses the input documents and strips out boilerplate report scripts or formatting wrappers.
- <b>Step 3: Guardrail Enforcement:</b> The context string plus custom persona variables enter the Mistral model node under the constraints of the Anti-AI-ism filter.
- <b>Step 4: Layout Materialization:</b> The JSON output passes down to an HTML template node that builds a responsive, stylized, multi-channel marketing dashboard.
- <b>Step 5: Output Review & Asset Capture:</b> The user clicks through functional dashboard tabs, modifies status dropdowns, copies copy blocks to their clipboard, or outputs the layout as a PDF presentation report using native browser print styles.


<br>

## Advanced Features & Edge Cases
- <b>JSON Validation Defect Handling:</b> If the LLM produces corrupted JSON notation, the workflow falls back to a structural parsing safeguard that auto-formats or safely captures unparsed text blocks to avoid complete layout collapse.
- <b>Empty Visual Array Handling:</b> When the prompt fails to extract valid hex color schemes or physical texture tokens, the system injects default baseline Wayfair asset codes to keep visual cards readable.

<br>

## Narrative
Elena, a Digital Content Planner at Wayfair, sits down on Thursday morning to structure next week's micro-campaign on trend-forward accent pieces. She has the text outputs from the Trend Discovery and Competitor Monitoring teams, but digging through the metric spreadsheets and HTML tables to find actionable visual cues takes her hours. Furthermore, drafting tailored variations across several channel formats often forces her into a repetitive loop of uninspired corporate copywriting.
Elena opens the AI Insights & Content Generation Agent dashboard. She uploads the raw report files, sets her target Style Persona dropdown to "Earthy Organic," and types "terracotta, handcrafted" into the custom vibe keyword block. She clicks generate.
Behind the scenes, the n8n pipeline processes her parameters, cleans the report markup, and sends the prompt payload to Mistral. Mistral, operating under a strict anti-cliche filter, ignores standard boilerplate expressions and designs a curated strategy card.
Within ninety seconds, Elena's screen refreshes into a dashboard. Under the Creative tab, she discovers an Instagram copy option that reads cleanly and avoids generic corporate buzzwords. Under the Design tab, a dedicated layout displays an asset palette complete with specific interior styling directions and hex color swatches ready to send to the design studio. Elena switches a card's status flag from To Do to Ready, clicks a button to copy the caption, pastes it directly into her scheduling queue, and prints the layout as a polished PDF report for her creative director's afternoon sync.

<br>

## Success Metrics

### User-Centric Metrics
- <b>Content Assembly Speed:</b> Reduce time spent drafting channel copy variations from hours to under 3 minutes per campaign.
- <b>UX Copy and Paste Engagement:</b> Rate of user clicks on the dynamic dashboard copy-to-clipboard elements.
- <b>Content Persona Variety:</b> Multi-persona execution frequency across team analysts (target: regular utilization of at least 3 distinct style profiles monthly).

<br>

### Business & Workflow Metrics
- <b>AI Output Quality Acceptance Rate:</b> Percentage of generated marketing copy requiring zero additional manual text removal post-generation (target: >85%).
- <b>Structured Visual Integration:</b> Number of generation outputs successfully outputting accurate mood_board_assets blocks.
- <b>Schema Integrity Validation Rate:</b> Rate of automated text passes converting into valid JSON objects without downstream failure (target: 100%).

<br>

## Technical Considerations

### Technical Needs
- <b>AI Orchestration Framework:</b> n8n workflow software configured with active HTTP webhooks and functional data injection properties.
- <b>LLM API Endpoints:</b> Stable access to the Mistral AI API platform utilizing the mistral-large-latest inference model.
- <b>Web UI Formatting Infrastructure:</b> Core knowledge of semantic HTML5 layouts, embedded responsive CSS styles, and structural JavaScript code blocks.

<br>

### Integration Points
- <b>Upstream Handoff:</b> Ingests structural text components, volume indicators, and pricing opportunities outputted by Step 3 (Competitor Monitoring).
- <b>Downstream Integration:</b> Supplies clean HTML data structures and color palette definitions to enrich the Step 5 consolidated Market Intelligence Dashboard interface.

<br>

### Storage, Performance & Privacy
- <b>Transient Session Architecture:</b> Generated campaign data is mapped instantly to the client's localized view engine; persistent user telemetry isn't collected, ensuring complete internal corporate security.
- <b>Browser Data Lifecycle:</b> Interface state tracking markers (To Do / Drafting) rely exclusively on the client web browser's local storage environment, bypassing backend database complexity.
- <b>Execution Latency Requirements:</b> Complete analytical parsing and layout delivery operations must finish within a maximum system runtime limit of 15 seconds per call.


## Milestones & Sequencing

### Project Estimate
- <b>Duration:</b> 1 Week (Optimized, focused sprint framework).

<br>

### Team Allocation
- <b>Lead AI Engineer:</b> Builds n8n workflows, optimizes system logic prompts, and implements JSON structuring filters.
- <b>Front-End UX Developer:</b> Creates response dashboards, integrates functional interactive widgets, and structures print styling behaviors.

<br>

### Suggested Phases
### Phase 1: Ingestion Architecture & Prompt Conditioning
- <b>Key Deliverables:</b> Establish working n8n file ingestion nodes. Configure the Mistral prompt block with the persona rules engine and anti-cliche filters.
- <b>Dependencies:</b> Configured and active Mistral AI API keys.

<br>

### Phase 2: Interface Integration & Functional Testing
- <b>Key Deliverables:</b> Embed JSON responses directly into tabbed HTML dashboards. Integrate clipboard copy buttons and localized status dropdown triggers.
- <b>Dependencies:</b> Clean, error-free JSON outputs generated by Phase 1 workflow models.

<br>

### Phase 3: Validation, Hardening & Pipeline Deployment
- <b>Key Deliverables:</b> Run multi-variant stress tests against corrupt JSON arrays. Validate dashboard scaling and layout structure on cross-functional devices. Complete all system deployment documentation.
- <b>Dependencies:</b> Step 5 team alignment on upstream schema expectations.
