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

**2. HubSpot Auto-Trigger** — Fires automatically on company creation text

HubSpot creates company → Webhook to Cloudflare Tunnel → n8n workflow triggers → 
Enrichment happens → HubSpot updated within 60 seconds

**3. Bulk Enrichment** — Process entire database text

Manual trigger → Fetch all companies → Loop through each → 
Rate-limited processing → Wait between calls → Update HubSpot
AI Failover System
Every AI call has automatic failover for 99.9% uptime:

Primary: Google Gemini (gemini-flash-latest)
Backup: Groq Llama 3.3 70B Versatile
If Gemini rate-limits or fails → Groq automatically takes over. Zero downtime.

ICP Scoring Rubric
Sample ICP (100 points total)
Configured for B2B SaaS companies:

Criteria	Weight	Perfect Match
Industry Match	25 pts	Pure SaaS/B2B Software
Company Size	20 pts	50-500 employees
Funding Stage	15 pts	Series A, B, or C
Tech Stack	15 pts	Modern cloud tools (AWS, GCP, React)
Growth Signals	15 pts	Hiring in past 90 days
Location	10 pts	US/Europe

Tier Classification
HOT (80-100) — Perfect ICP fit, prioritize immediately
WARM (60-79) — Good fit, worth outreach
COLD (40-59) — Partial fit, low priority
DISQUALIFIED (0-39) — Not our ICP

Use Cases
🏢 RevOps Teams — Automated lead prioritization
🎨 Marketing Agencies — Client lead qualification
👨‍💻 Sales Teams — Focus on HOT leads only
💼 Founders — Personal ICP enforcement
🧠 SDR Managers — Objective lead routing

Built By
Ujjwal Bisen
GTM Engineer | AI Automation Specialist

🔗 GitHub
📚 Related Project: AI-SDR-Automation
