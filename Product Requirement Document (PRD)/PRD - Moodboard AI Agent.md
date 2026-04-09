# PRD: Moodboard AI Agent

### Summary

Moodboard AI Agent is an AI-powered web tool that translates abstract style descriptors (e.g., “Modern Farmhouse”, “Coastal Luxe”) into high-fidelity visual moodboards within 60 seconds. It leverages Gemini 2.0 LLM reasoning to refine prompts and Hugging Face FLUX for parallel image generation. Designed for Creative Directors, Social Media Managers, and Interior Designers, this product automates manual image sourcing and visual prototyping.

---

## Goals

### Business Goals

* **Eliminate Manual Bottlenecks**: Remove the hours-long manual image sourcing step in seasonal campaign planning.
* **Fast Time-to-Visual**: Reduce moodboard creation time from several hours to under 60 seconds.
* **Increase Design Throughput**: Enable design teams to prototype and iterate on multiple concepts quickly for higher output during seasonal launches.
* **Drive Adoption**: Ensure adoption by at least three distinct creative personas within 60 days of launch.

### User Goals

* **Rapid Prototyping**: Instantly translate abstract style ideas into fully formed moodboards.
* **On-Brand Consistency**: Generate assets that reflect brand guidelines and current aesthetics without endless curation.
* **Client-Ready Outputs**: Present polished “concept feel” visuals to clients before narrowing in on specific SKUs or products.
* **Visual Alignment**: Achieve stakeholder buy-in faster with more accurate, on-point visuals.

### Non-Goals

* Integration with e-commerce shopping carts or product catalogs.
* Individual SKU selection, tagging, or price tracking.
* Workflow automation for post-moodboard tasks (e.g., campaign scheduling, detailed asset management).

---

## User Stories

* **Creative Director**

  * As a Creative Director, I want to input a theme descriptor (e.g., “Midcentury Cozy”) so that I can rapidly prototype campaign “looks” without manual image searching.
  * As a Creative Director, I want to review the technical prompts before image generation so I can ensure creative alignment.

* **Social Media Manager**

  * As a Social Media Manager, I want to generate on-brand moodboards keyed to trending styles, so my assets stay current and engaging.
  * As a Social Media Manager, I want to easily export the moodboard and color palette for use in post templates.

* **Interior Designer**

  * As an Interior Designer, I want to visualize a “concept feel” for a client presentation without selecting individual products, saving time during early-stage pitching.
  * As an Interior Designer, I want the final moodboard to include a color palette with hex codes for easy communication with clients and contractors.

**Acceptance Criteria** (for all personas):

* System produces a moodboard containing 4 distinct, relevant images.
* Primary color palette (with hex codes) is extracted and displayed.
* Completed board and palette can be exported as a single downloadable file.

---

## Functional Requirements

* **Theme-to-Prompt Parsing (Priority: P0)**

  * Gemini 2.0 API receives user’s abstract style descriptor.
  * AI refines and decomposes input into 4 technical, visually distinct prompts.
  * User is shown prompts for optional review and edit.

* **Image Generation (Priority: P0)**

  * Prompted by Gemini, 4 calls are made to Hugging Face FLUX API to generate distinct high-quality images.
  * Images are displayed in a single moodboard grid (2x2).

* **Color Palette Extraction (Priority: P1)**

  * Images processed for color quantization.
  * Primary color palette (including at least 4-6 hex codes) extracted and displayed beneath the moodboard.
  * Copy-to-clipboard functionality on each hex code.

---

## User Experience

**Entry Point & First-Time User Experience**

* User navigates to a clean, self-hosted web UI deployed from Docker.
* If first-time, a 30-second onboarding overlay explains the workflow (input descriptor → prompt review → moodboard + palette).
* No mandatory login; one-click start to encourage discovery.

**Core Experience**

* **Step 1:** User enters a style descriptor (e.g., “Modern Farmhouse”) into a prominent search-style field.
  * Minimal friction UI: large, inviting input and action button.
  * Input validates for non-empty content; if ambiguous/empty, prompts clarification with suggested examples.
* **Step 2:** Gemini 2.0 parses the descriptor into 4 technical prompts.
  * System displays the four prompts; user can edit or approve as-is.
  * UI clearly distinguishes between original input and AI’s breakdown, offering transparency.
* **Step 3:** Upon prompt approval, FLUX API generates 4 high-fidelity images in parallel.
  * Progress indicator animates, updates shown if API retry/backoff occurs.
* **Step 4:** Images are displayed in a seamless, full-bleed 2x2 grid as the completed moodboard.
  * Each image visually distinct, rendered at high resolution.
* **Step 5:** Below the image grid, extracted primary color palette is displayed as a horizontal strip of swatches, each with a hex code.
  * Each swatch: click-to-copy hex.
* **Step 6:** A single-click “Export” button bundles the grid and palette as a downloadable PNG or PDF.
  * Confirmation toast for successful export.

**Advanced Features & Edge Cases**

* On API rate limit/timeout: Workflow surfaces a progress spinner and message (“Retrying—Hang tight!”) and retries up to 3x before showing an error with actionable next steps.
* On ambiguous/empty input: Prompt overlay suggests style descriptor examples and requests user clarification.
* If image generation fails for one or more prompts, placeholders maintain visual grid but display tooltip error for the affected slot.

**UI/UX Highlights**

* Minimal, distraction-free layout focused on the creative task.
* Responsive and optimized for desktop and tablet (primary use cases).
* High-contrast, accessible color palette display with readable hex codes.
* Progress indicators for all asynchronous actions.
* Export and copy actions have instant feedback confirmation.
* No persistent personal data collection; privacy-first design.

---

## Narrative

A Creative Director at a leading home goods brand sits down to kick off development on a new autumn collection. Her challenge is to quickly converge the creative team around an inspiring vibe—something like “Warm Minimalist Autumn”—that will drive the season’s marketing, visual direction, and product styling. Traditionally, building a moodboard would involve hours spent in Pinterest rabbit holes, wrangling assets, and rounds of sharing and edits over Slack and email.

Today, she types “Warm Minimalist Autumn” into the Moodboard AI Agent’s sleek browser interface. Instantly, the Gemini engine parses her intent and proposes four refined prompts: cozy textures, muted foliage palettes, sculptural modern furnishings, and soft seasonal light. With a single click, four unique high-fidelity images materialize, comprising a perfectly cohesive moodboard. Below, the tool surfaces an extracted color palette—complete with hex codes—anchoring the visual story for the season.

Within 60 seconds, she exports a client-ready concept deck. What previously took a half-day of manual sourcing and asynchronous collaboration is now a one-minute workflow. The whole business is empowered to move faster; visual direction is locked earlier, the seasonal vision resonates more strongly, and the team has more time to drive execution, iterate on deeper creative tasks, and delight clients with best-in-class visuals.

---

## Success Metrics

### User-Centric Metrics

* **Moodboard generation time**: >95% of boards delivered in under 60 seconds (measured via backend logs).
* **Stakeholder visual style alignment**: ≥90% “on-point” score in post-session stakeholder surveys.
* **User engagement**: Number of completed moodboards and exports per user per week.

### Business Metrics

* **Time-to-first-visual**: Median time reduced from hours to under 5 minutes in tracked projects.
* **Persona adoption**: Active use by Creative Director, Social Media Manager, and Interior Designer personas within 60 days post-launch.

### Technical Metrics

* **API success rate**: >99% of Gemini and FLUX API calls succeed or recover via retry.
* **Image generation latency**: P95 under 60 seconds from input to export capability.
* **Uptime**: >99.5% on self-hosted Docker deployment.

### Tracking Plan

* Input submission events
* Prompt review/approval events
* Image generation completion events
* Download/export events
* Retry trigger events
* Hex copy-to-clipboard events

---

## Technical Considerations

### Technical Needs

* **Orchestration Layer**: Manages prompt parsing, parallel image generation, and workflow state.
* **API Integration**: Connectors for Gemini 2.0 (LLM) and Hugging Face FLUX (image generation).
* **Color Quantization Module**: Processes generated images for key palette extraction.
* **Frontend Web UI**: Simple, performant SPA, containerized via Docker.

### Integration Points

* **Gemini 2.0 API** (LLM for prompt refinement).
* **Hugging Face Inference API** (FLUX for image generation).

### Data Storage & Privacy

* No user accounts, persistent storage, or cloud uploads.
* All input and output data remains within the self-hosted Docker environment for IP and content security.
* Only transient in-memory state during session; nothing written to disk after export.

### Scalability & Performance

* Designed for single or small team concurrent usage.
* Horizontal scaling via Docker Compose possible for larger teams.
* Optimized parallel processing for 4-image workflows; backoff and retry logic for rare API congestion.

### Potential Challenges

* Managing API rate limits for both Gemini and FLUX (via exponential backoff and smart retry).
* Ensuring all AI calls, including image generation, fall within the 60s SLA.
* Robust error handling and user feedback in offline or partial-failure situations.

---

## Milestones & Sequencing

### Project Estimate

* **Medium (2 weeks)**

### My Role: 

  * Product Manager/Designer (user stories, flows, UI)
  * Engineer (backend orchestration, API integration, frontend, Docker)

### Suggested Phases

**Phase 1 — Core Pipeline (Week 1–2)**

* Key Deliverables:
  * Gemini prompt parsing to FLUX image generation: engineer
  * End-to-end workflow functional
  * Simple Dockerized UI: engineer
* Dependencies:
  * Gemini and Hugging Face API credentials

**Phase 2 — Polish & Color Extraction (Week 2)**

* Key Deliverables:
  * Color quantization and palette extraction: engineer
  * Moodboard grid UI with palette strip: designer/engineer
  * Export, retry logic, edge case handling: engineer
* Dependencies:
  * Stable pipeline from Phase 1

**Phase 3 — Validation & Launch (Week 1-2)**

* Key Deliverables:
  * Test with internal stakeholders (creative team, social, design, etc.): PM
  * Measure success metrics (SLA, approval rates)
  * Bugfixes, performance tuning, <60s generation SLA: engineer
* Dependencies:
  * Completed features and internal feedback

---
