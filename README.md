# 🎯 HubSpot-ICP-Enrichment

**AI-powered ICP (Ideal Customer Profile) scoring and enrichment pipeline for HubSpot CRM.**

Automatically scores companies against configurable ICP criteria, enriches HubSpot records with structured data, and detects buying signals — all with dual AI provider failover for 99.9% reliability.

Built with **n8n**, **Google Gemini**, **Groq Llama 3.3**, **Tavily**, **HubSpot API**, and **Cloudflare Tunnels**.

> 🚀 Turn any HubSpot company into a fully-scored, enriched lead in under 60 seconds — automatically.

---

## ✨ What It Does

Given a HubSpot company ID (via API call, webhook, or bulk trigger), this system automatically:

1. 🔍 **Fetches** company data from HubSpot
2. 🕷️ **Crawls** the company's website (homepage, meta tags, tech stack detection)
3. 🌐 **Researches** the company via Tavily AI web search
4. 🧠 **Analyzes** with Google Gemini AI (industry, size, funding, growth signals)
5. 🎯 **Scores** the company against ICP criteria (0-100)
6. 🔥 **Classifies** as HOT / WARM / COLD / DISQUALIFIED
7. 📊 **Updates** HubSpot with all enrichment data
8. ⚡ **Auto-triggers** on new company creation (via HubSpot webhooks)
9. 📦 **Bulk processes** entire HubSpot database

---

## 🏗️ Architecture

### Three Ways to Trigger Enrichment

**1. Manual API Call** — Direct webhook for single company
```bash
curl -X POST http://localhost:5678/webhook/enrich \
  -H "Content-Type: application/json" \
  -d '{"company_id": "12345"}'
