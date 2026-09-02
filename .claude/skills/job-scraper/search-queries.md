# Search Queries for Job Scraper

<!-- SETUP: Customize these queries based on your skills, target roles, and location -->

## Installed portal CLIs (primary for `/scrape`)

`/scrape` discovers every portal skill under `.agents/skills/*/SKILL.md` and runs its CLI first. Shipped country-agnostic CLIs include `linkedin-search` and `freehire-search`; Danish demos and any skill you add with `/add-portal` are included the same way. You do **not** need a matching `site:` line below for those CLIs to run.

The `site:` query templates in this file are the **WebSearch fallback** — for portals without a CLI, company career pages, or when a CLI fails.

**Language scope:** write every query category in every language listed in your CLAUDE.md Languages table (typically 1-2, sometimes more). A posting requiring a language you have *not* declared, as a job condition, is excluded before scoring; a posting requiring a *higher level* than you declared in a language you *do* work in is flagged for your own judgment, not excluded — see `04-job-evaluation.md`'s Language Gate, the single source of truth for this rule. Translate each category's keywords rather than machine-translating word-for-word (e.g. "Frontend Developer" -> "Desarrollador Frontend", not a literal word-for-word translation) if you work in more than one language.

## Search Sites

Primary (your market's job boards):
- **linkedin.com/jobs** - LinkedIn job listings (global, filter by country/region); also covered by `linkedin-search` CLI
- **angel.co / Crunchbase** - Startup job boards (US focus, but includes remote roles globally)
- **hn.algolia.com** - Hacker News "Who is Hiring" posts (tech-heavy, remote-first)
- **remoteok.io / We Work Remotely** - Remote job boards (global)
- **Workable** - Direct company career pages (many companies use this)

Secondary (company career pages via Google):
- Direct Google searches with `site:` filters for fintech, AI/ML, and media tech companies

## Query Categories

Queries organized by priority and function. **Each category appears in both English and Portuguese** to capture roles in both languages and geographies.

**Organize by function, not job title.** Target roles include: Sr MLOps Engineer, Sr ML Engineer, Sr Backend Engineer, Scala Engineer, AI Engineer, Platform Engineer.

### Priority 1: MLOps & ML Infrastructure (Highest Priority)

Focus on infrastructure, platform, and systems engineering for ML/data.

**English:**
```
site:linkedin.com/jobs "MLOps Engineer" OR "ML Operations" OR "Machine Learning Ops" remote
site:linkedin.com/jobs "Sr MLOps" OR "Senior MLOps" AWS Kubernetes
site:linkedin.com/jobs "ML Infrastructure" OR "ML Platform" engineer
site:linkedin.com/jobs Databricks Airflow "data engineer" remote
site:linkedin.com/jobs "ML Engineer" Scala Python AWS remote
```

**Portuguese:**
```
site:linkedin.com/jobs "Engenheiro MLOps" OR "ML Operations" AWS Kubernetes
site:linkedin.com/jobs "ML Infrastructure" engenheiro Brasil remoto
```

### Priority 2: Backend Engineering & Distributed Systems

Backend systems, real-time data, payment infrastructure.

**English:**
```
site:linkedin.com/jobs "Sr Backend Engineer" OR "Senior Backend Engineer" Scala remote
site:linkedin.com/jobs "Backend Engineer" Kafka Spark Python remote
site:linkedin.com/jobs "Platform Engineer" OR "Infrastructure Engineer" AWS Kubernetes remote
site:linkedin.com/jobs "Distributed Systems" engineer fintech OR payment remote
site:linkedin.com/jobs Scala engineer "senior" backend remote
```

**Portuguese:**
```
site:linkedin.com/jobs "Engenheiro Backend" Scala Python fintech remoto
site:linkedin.com/jobs plataforma dados tempo real Kafka remoto
```

### Priority 3: Fintech & Fraud / Risk Analysis

Domain expertise: payment systems, fraud prevention, risk.

**English:**
```
site:linkedin.com/jobs fintech "ML Engineer" OR "Backend Engineer" Python remote
site:linkedin.com/jobs "Fraud Detection" OR "Risk Analysis" ML engineer remote
site:linkedin.com/jobs "Payment Systems" engineer backend AWS remote
site:linkedin.com/jobs "Financial Systems" backend Scala OR Python remote
```

**Portuguese:**
```
site:linkedin.com/jobs fintech "Engenheiro" dados tempo real Brasil
site:linkedin.com/jobs fraude detecção ML Python remoto
```

### Priority 4: AI/ML at Scale (Startups & AI-First Companies)

AI-native and ML-focused companies, research labs.

**English:**
```
site:linkedin.com/jobs "AI Engineer" OR "ML Engineer" remote scaling
site:linkedin.com/jobs "AI Platform" OR "ML Platform" infrastructure engineer
site:linkedin.com/jobs "Applied AI" backend engineer Databricks remote
site:linkedin.com/jobs "Large Language Models" OR "LLM" infrastructure remote
```

### Priority 5: Media/Broadcast & Real-Time Systems

Domain expertise: broadcasting, forecasting, real-time data.

**English:**
```
site:linkedin.com/jobs broadcast OR media "ML Engineer" forecasting remote
site:linkedin.com/jobs "Real-Time Analytics" OR "Stream Processing" engineer AWS remote
site:linkedin.com/jobs "Time Series" forecasting ML engineer remote
```

### Priority 6: E-commerce & Marketplace Infrastructure

Domain expertise: recommendation systems, scaling, recommendation.

**English:**
```
site:linkedin.com/jobs "Recommendation Systems" engineer ML remote
site:linkedin.com/jobs e-commerce "ML Engineer" OR "Backend Engineer" scale remote
site:linkedin.com/jobs marketplace infrastructure backend Spark remote
```

### Priority 7: Climate Tech, Instrumentation, Blockchain

Emerging domains with data infrastructure needs.

**English:**
```
site:linkedin.com/jobs climate tech "ML Engineer" OR "Data Engineer" remote
site:linkedin.com/jobs instrumentation OR IoT "backend engineer" OR "systems engineer" remote
site:linkedin.com/jobs blockchain infrastructure engineer Scala OR Go remote
```

## Location Filter

Remote first (no location constraints given your "US/BR timezone preferred, no scope restriction"):
- **Ideal:** Fully remote, US or Brazil-based companies (timezone alignment)
- **Acceptable:** Remote with occasional travel to US/Brazil hubs
- **Consider:** Relocation for extraordinary opportunities (top companies, significant growth trajectory)

## Language Filter

Your working languages: English (C1), Portuguese (Native), Spanish (Fluent reading).

Apply Language Gate from `04-job-evaluation.md`:
- Posting requiring English: ✅ PASS (C1 covers this)
- Posting requiring Portuguese: ✅ PASS (Native)
- Posting requiring Spanish: 🚩 FLAG if written requirement (reading fluency is real but limited on speaking)
- Posting requiring languages not listed (e.g., French, German): ❌ FAIL (not declared)

## Date Filter

Only include jobs posted within the last **21 days** (slightly longer than 14 days to capture enough volume given remote scope). Flag postings with date unknown.

## Salary & Compensation

Target minimum: **USD $5,000/month** for B2B contractor, **USD $6,000/month** target.

When salary is disclosed, verify it meets baseline before applying.

## Adapting Queries

To focus on a specific domain or industry:
- `/scrape fintech` → Priority 3 queries + custom fintech-specific searches
- `/scrape broadcast` → Priority 5 queries + media/broadcast specific
- `/scrape startup` → Combine Priority 1-2 with founder-friendly job boards (angel.co, Crunchbase)
