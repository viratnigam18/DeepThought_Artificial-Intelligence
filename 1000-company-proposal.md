# Proposal: Scaling the Federer Search to 1000 Companies in 30 Days
### Multi-Agent RAG Pipeline Architecture

## Goal
Deliver a verified, highly accurate list of 1000 ICP-qualified "Federer" manufacturing companies across India within one month, eliminating the manual bottleneck of website evaluation and hallucination risks associated with standard LLM use.

## The Strategy: Autonomous Agent Framework
Given access to AI, APIs, and scraping tools, throwing humans at Google search is inefficient. I propose building a deterministic Multi-Agent workflow using LangGraph and the Gemini API. 

To achieve 1000 passes (assuming a 25-30% yield rate), we need to source an initial universe of ~4000 MSMEs. 

### Week 1: Data Acquisition Agent (The Top of the Funnel)
**Goal: Build the 4000-company universe while programmatically eliminating obvious failures.**
* **Sources:**
    * **DSIR Registry:** Parse the government's PDF of recognized in-house R&D units. (Strong signal for C3/C4).
    * **PLI Scheme Beneficiaries:** Scrape the government portals for Pharma, Medical Devices, and Auto Components PLI approvals. 
    * **MCA API (Antigravity):** Query NIC codes specifically for specialty manufacturing (e.g., 20119 - other basic chemicals, 2100 - pharmaceuticals, 26 - electronic/optical products).
* **Automated Pre-Filter:** The agent cross-references the scraped lists against MCA paid-up capital data to instantly drop companies with >Rs.500Cr revenue or institutional/PE ownership structures. 

### Week 2: The Scraper & Enrichment Agent
**Goal: Pull website data for the remaining ~3000 companies.**
* Deploy a Python/Playwright asynchronous scraper. 
* **Targeted Extraction:** Instead of scraping the whole site, the bot navigates explicitly to `/about`, `/management`, `/team`, `/products`, and `/certifications`. 
* The raw HTML is stripped into clean markdown and packaged into JSON blobs per company. If a site is dead or a 1-page placeholder, it is auto-disqualified.

### Week 3: The LLM Evaluation Agent (Gemini API)
**Goal: Score C1-C6 with strict Hallucination Controls.**
This is where most pipelines fail by allowing the LLM to guess. We constrain the AI using strict prompt engineering and structured JSON outputs.
* **Negative Prompting:** The system prompt explicitly instructs the Gemini model: *"Auto-reject CROs, Testing Labs, & pure software companies. Do NOT infer manufacturing capabilities from marketing copy."*
* **Forced Citation (Hallucination Control):** The LLM is **not allowed to summarize** the evidence for C1 (Manufacturer) and C4 (Tech DM). It must extract the *exact verbatim string quote* from the scraped website text. If it cannot find a quote, it must score it as a 'Fail'.

### Week 4: Human-in-the-Loop QA
**Goal: Verify the edge cases.**
* The pipeline outputs a master CSV.
* We do not review the "Strong Passes" or the "Fails". 
* Human review is strictly reserved for the ~300-400 "Borderline" companies (Score 40-59) or companies where the AI flagged conflicting data (e.g., high technical capability but missing revenue data). 

## Expected Yield
* **Initial Sourced:** 4000
* **Post-MCA Filter:** 3000
* **Post-Scrape (Dead links/Traders dropped):** 2500
* **Post-LLM Evaluation (Strong Pass + Borderline QA'd):** ~1000 Verified Federer Companies.