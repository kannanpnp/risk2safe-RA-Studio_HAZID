# ⚠️ PHA Studio — AI-Powered Process Hazard Analysis

> A single-file, self-contained web app for **HAZID**, **What-If**, and **Checklist** studies —
> powered by the Anthropic Claude API. No installation, no build step, no server required.
> Just open `index.html` in any browser.

---

## 📸 What it does

| Study Type | Methodology | What AI generates |
|---|---|---|
| **HAZID** | Crawley consequence-driven matrix (1987) | Effect → Cause → Consequence → Mitigations → Actions across 8 hazard categories |
| **What-If** | CCPS brainstorming framework (1992/2008) | Deviation questions with Causes, Consequences, Safeguards, Recommendations |
| **Checklist** | Scott-Crawley / CCPS (1992) | 12 compliance questions across 9 categories (fire, pressure, I&C, emergency, procedures…) |

**Everything is editable after generation** — click any cell to type directly in the table.
Add rows manually at any time. Export each study as CSV or JSON.
All data auto-saves to browser `localStorage` between sessions.

---

## 🚀 Run it instantly (no install needed)

1. Download `index.html`
2. Double-click it — it opens in your browser
3. Click **🔑 Set API Key** (top-right) → enter your Anthropic API key
4. Fill in **Project Setup** → describe your system
5. Switch to **HAZID / What-If / Checklist** → click **Generate with AI**

That's it.

---

## 🌐 Publish to GitHub Pages (2-minute setup)

### Option A — Upload via GitHub web interface

1. Go to [github.com](https://github.com) → **New repository**
2. Name it `pha-studio` (or anything you like) · set it **Public**
3. On the repo page click **Add file → Upload files** → drag in `index.html` and `README.md`
4. Commit to `main`
5. Go to **Settings → Pages → Source → Deploy from a branch → main / root** → Save
6. Wait ~60 seconds → your app is live at:

```
https://<your-username>.github.io/pha-studio/
```

### Option B — Git command line

```bash
git init pha-studio && cd pha-studio
cp /path/to/index.html .
cp /path/to/README.md .
git add .
git commit -m "Launch PHA Studio"
git remote add origin https://github.com/YOUR-USERNAME/pha-studio.git
git push -u origin main
```

Then enable Pages: **Settings → Pages → Branch: main / (root)** → Save.

---

## 🔑 Getting an Anthropic API Key

1. Sign in at [console.anthropic.com](https://console.anthropic.com)
2. Go to **API Keys** → **Create Key**
3. Copy the key (starts with `sk-ant-api03-…`)
4. Paste it into PHA Studio via the **🔑 Set API Key** button

The key is stored **only in your browser's `localStorage`** — it is never sent anywhere
except directly to `api.anthropic.com` when you click Generate.

> **Cost note:** Each "Generate with AI" call consumes roughly 500–1,000 output tokens
> (≈ USD 0.003–0.015 depending on your Anthropic plan). A full three-study session
> costs less than $0.05.

---

## 🔐 Security & Privacy

| What | Where it goes |
|---|---|
| API key | Browser `localStorage` only — never sent to any server except Anthropic |
| Study data (HAZID rows, checklists, etc.) | Browser `localStorage` only |
| System description / process conditions | Sent to Anthropic Claude API to generate scenarios |

**For shared or multi-user deployments** (e.g. a company intranet): proxy the API call
through a backend (Node.js, Python, Cloudflare Worker) so individual users never
see the API key. The `index.html` can be updated to call your proxy URL instead of
`api.anthropic.com` directly — change the `API_URL` constant at the top of the `<script>`.

---

## 📋 How to use each study type

### Project Setup (always start here)
Fill in the **System Description** (required) and **Process Conditions** before
generating anything. The AI uses these fields to create specific, realistic scenarios.
The more detail you provide, the better the output.

### HAZID
- Click **Generate with AI** to create 8 consequence-driven scenarios
- Edit Ref, Area, Effect, Cause, Consequence, Mitigations, Scenario in the table cells
- Adjust **S** (Severity 1–5) and **L** (Likelihood 1–5) dropdowns — Risk rating updates automatically
- Click **+ Add Row Manually** to add your own scenarios
- Export to **CSV** (for Excel) or **JSON** (for integration with other tools)

### What-If
- Click **Generate with AI** to create 8 deviation questions
- Covers: no flow, excess flow, high/low pressure, temperature excursion, equipment failure, utility loss
- Edit all fields inline; S × L risk rating updates in real-time
- Add unlimited rows manually

### Checklist
- Click **Generate with AI** to create 12 compliance questions
- Click each **Response** dropdown to mark: ✓ Yes / ✗ No / ~ Partial / TBD / N/A
- Click **status pills** (Compliant / Non-Compliant / etc.) to filter the table
- Non-Compliant items highlight red — focus your team's actions there

---

## 🗂 File structure

```
pha-studio/
├── index.html   ← the entire application (HTML + CSS + JS, zero dependencies)
└── README.md    ← this file
```

No `node_modules`. No build step. No framework. Pure HTML, CSS, and vanilla JavaScript.

---

## 🛠 Customisation

Everything is in a single file — open `index.html` in any text editor.

| What to change | Where to look |
|---|---|
| AI model | `const MODEL = 'claude-sonnet-4-20250514'` near top of `<script>` |
| Number of generated rows | Prompt text inside `generateHazid()`, `generateWhatif()`, `generateChecklist()` |
| Risk matrix thresholds | `riskMeta()` function |
| Colour scheme | CSS custom properties at the top of `<style>` (`:root { --amber: … }`) |
| Table columns | Add/remove `<th>` in `<thead>` and matching fields in `*RowHTML()` functions |
| Add a new study type | Copy the HAZID section pattern — it's fully self-contained |

---

## 📐 Methodology references

- **HAZID**: Crawley, F.K. (1987). *Application of HAZOP study techniques to the design of offshore installation topside facilities*, IBC Technical Services, London. Consequence-driven 3-column matrix: Effect | Cause | Consequence.
- **What-If**: Center for Chemical Process Safety (CCPS) (1992/2008). *Guidelines for Hazard Evaluation Procedures*, 2nd/3rd edition. AIChE / Wiley.
- **Checklist**: Scott, D. & Crawley, F.K. (1992). *Process Plant Design and Operation*, IChemE Rugby. Extended with CCPS categories.
- **Risk matrix**: Severity × Likelihood grid aligned with IEC 61511 / ISO 45001 / API RP 580 semi-quantitative risk ranking.

---

## 📄 License

MIT — free to use, modify, and distribute. Attribution appreciated but not required.

---

*Built for HSE and process-safety professionals in oil & gas, petrochemical, and refining industries.*
