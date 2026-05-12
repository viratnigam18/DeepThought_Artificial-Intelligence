# DeepThought Business Analytics Assignment: Target Company Research

**Author:** Virat Nigam  
**Role:** Business Analytics Intern Candidate  

## Overview
This repository contains my submission for the DeepThought Business Analytics Internship assignment. The goal of this project is to identify, research, and evaluate manufacturing MSMEs in India that fit the **"Federer" Ideal Customer Profile (ICP)**: Rs.50Cr–Rs.500Cr revenue, differentiated products, technically-minded founders, and active growth signals.

Instead of relying solely on manual Google searches, this submission leverages structured government databases, MCA data filtering, and proposes an autonomous AI-agent framework to scale the research process deterministically.

## Repository Contents

### Part A: The 25-Company Sourcing
* 📄 **`target_companies_pune.csv`**: A highly curated list of 25 companies based in Pune, Maharashtra. It includes deep-dive evaluations across the 6 ICP criteria, complete with exact evidence, scoring, and personalization hooks. Includes "Pass", "Borderline", and "Auto-Fail" examples to demonstrate strict boundary adherence.
* 📝 **`methodology.md`**: A breakdown of the sourcing funnel, explaining how I bypassed generic service companies (CROs/Testing Labs) by starting with DSIR R&D registries and PLI scheme data, and how MCA data was used to enforce the Rs. 50Cr-500Cr revenue ceiling.

### Part B: Sourcing Strategy & Scale-Up Proposal
* 🚀 **`1000-company-proposal.md`**: A comprehensive, 30-day architectural plan to scale this research to 1,000 verified ICP companies. It details a Multi-Agent RAG pipeline (utilizing tools like LangGraph, Playwright, and Gemini APIs) to automate top-of-funnel sourcing, website scraping, and strict JSON-structured evaluation while aggressively mitigating LLM hallucinations through forced exact-match citations. 

*(Note: The mandatory hand-drawn system architecture diagram for the 1000-company pipeline has been submitted directly via the Internshala chat as requested).*

## Core Tech & Concepts Proposed
* **Data Sources:** DSIR Registry, PLI Beneficiary Data, MCA (Ministry of Corporate Affairs) API, Tofler/ZaubaCorp.
* **AI & Automation:** LangGraph (Multi-Agent Framework), Gemini API, Python, Playwright (Asynchronous web scraping).
* **Evaluation Logic:** Zero-shot prompting, structured JSON outputs, and programmatic pre-filtering (dropping PE-backed or >500Cr revenue entities).
