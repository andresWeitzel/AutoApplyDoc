<div align="center">
<img src="../screenshots/search.png" alt="AutoApply — Find your next opportunity" width="100%" />
<div align="right">
<img width="16" height="16" src="../icons/frontend/svg/react.svg" alt="React" />
<img width="16" height="16" src="../icons/frontend/svg/vite.svg" alt="Vite" />
<img width="16" height="16" src="../icons/backend/javascript-typescript/svg/nodejs-color.svg" alt="Node.js" />
<img width="16" height="16" src="../icons/automation/svg/playwright.svg" alt="Playwright" />
<img width="16" height="16" src="../icons/devops/png/git.png" alt="Git" />
<img width="16" height="16" src="../icons/devops/png/npm.png" alt="npm" />
</div>
</div>

<br>

<br>

<div align="right">
  <a href="../../../README.md" title="Español">
    <img src="./arg-flag.jpg" width="64" height="40" alt="Español" title="Español" />
  </a>
  <a href="./README.en.md" title="Inglés">
    <img src="./eeuu-flag.jpg" width="64" height="40" alt="Inglés" title="Inglés" />
  </a>
</div>

<div align="center">

# AutoApply ![(status-active)](../icons/badges/status-active.svg)

</div>

AutoApply is an application that finds roles matching your profile, fills the application and hands control back before you submit. You load your details **once** and every listing reuses them. It includes **filters** to refine the search, update your profile and manage history, settings and the rest of the flow. **Search, fill, confirm** — the final send is yours.

<div align="left">
<a href="https://autoapply-demo-1tjt.onrender.com/" target="_blank" rel="noopener noreferrer" title="Live"><img src="../icons/detail-actions/live-pill.svg" alt="Live" width="96" height="32" border="0" /></a>
</div>

<br>

## Index 📜

<details>
  <summary> View details </summary>

<br>

<div align="right">

`Last update: 06/10/26`

</div>

### Section 1) Description, configuration and technologies

* [1.0) Description.](#10-description-)
* [1.1) Project execution.](#11-project-execution-)
* [1.2) Project structure.](#12-project-structure-)
* [1.3) Technologies.](#13-technologies-)

### Section 2) Usage flow and behavior

* [2.0) App flow.](#20-app-flow-)
* [2.1) Profile and documents.](#21-profile-and-documents-)
* [2.2) Job search.](#22-job-search-)
* [2.3) Autofill and submit.](#23-autofill-and-submit-)
* [2.4) Privacy, data and limits.](#24-privacy-data-and-limits-)

### Section 3) Testing, hosted demo and references

* [3.0) Functional test.](#30-functional-test-)
* [3.1) Hosted sandbox (Render).](#31-hosted-sandbox-render-)
* [3.2) Contributing.](#32-contributing-)
* [3.3) License.](#33-license-)

</details>

<br>

## Section 1) Description, configuration and technologies

### 1.0) Description [🔝](#index-)

<details>
  <summary>View details</summary>

<br>

Applying today is a second job: the same phone number, the same CV and the same answers, over and over, on LinkedIn, Indeed, Bumeran and whichever ATS comes next.

AutoApply cuts that friction. **One profile. A search that understands your stack. Autofill that types for you.** A history so you do not apply twice. And a rule that does not bend: you send the application. This is not a bot that fires CVs blindly; it is an assistant that speeds up the repetitive part and leaves you what matters.

**Locally it is the real product.** It searches live listings, opens its own Chromium, fills portal and ATS forms, stores your profile and accounts, and you submit the application. Filters, history, settings and attachments run against the real world.

**The public demo is limited on purpose.** On [Render](https://autoapply-demo-1tjt.onrender.com/) you walk the same UI with a fictional profile and a test portal: no application Chromium, no real accounts, and **no applications sent to companies**. It is there to show the flow without installing anything and without risking data or other people’s vacancies.

Why it exists:

* Copy-paste across job boards burns hours and introduces mistakes. AutoApply concentrates your data and types it into the form.
* An “auto-apply” that hits Submit without review is the shortcut that does the most damage. Submit is **manual on purpose**.
* Recruiters and reviewers walk the **same UI** in the demo; the full flow runs locally (see 1.1 and 3.1).

What the product delivers:

* **Find roles that fit.** Portals such as LinkedIn, Indeed, Bumeran, Get on Board, Computrabajo, ZonaJobs, Tecnoempleo, Remotive and Remote OK, with filters for role, work mode, technologies and languages — plus a match score to prioritize, not to promise an offer.
* **Load the profile once.** Identity, contact, per-technology experience, education, CV (PDF, DOC, DOCX) and saved answers. The next listing reuses all of it.
* **Autofill, do not send blind.** Locally, own Chromium: text, selects, radios, attachments. The red **Stop** button returns control with what was already filled. In the demo, fill is shown on a controlled form.
* **Keep a trail.** Submitted history, opened opportunities and “not a fit”, so you neither repeat nor see again what you already dismissed.
* **Your data stays with you.** Locally, profile, accounts and backups on your machine. The demo does not read that disk: it uses sample data and resets with the sandbox.

**Requirements (local version):**

* [Node.js](https://nodejs.org/) **22.13+** (22.14 recommended).
* npm.
* Playwright Chromium (`npx playwright install chromium`).
* A graphical session: forms are visible and finished by hand.
* Internet for portals and, if you configure it, optional assistance.

**Requirements (demo):** Node.js and npm. It does not install or launch Chrome.

</details>

### 1.1) Project execution [🔝](#index-)

<details>
  <summary>View details</summary>

<br>

#### Local version (full app)

From the AutoApply project root:

```bash
npm ci
npx playwright install chromium
```

If `.env` is missing, copy the template (never commit `.env`):

```bash
cp .env.example .env
```

Start:

```bash
npm run dev
```

The app listens on `http://127.0.0.1:8787`. If that port is taken it tries 8788 and walks upward. The terminal prints the effective URL. UI, API and live reload share **one port**.

| Variable | Role |
|----------|------|
| `PORT` | Initial port (default `8787`; only ports from 8787 up are used) |
| `CURSOR_API_KEY` | Optional assistance for unrecognized controls and letter tweaks. Empty = local rules only |

**Do not** commit `.env`. No key is required for search, profile, autofill or history.

#### Public demo (what Render hosts)

```bash
npm ci
npm run build:demo
npm run start:demo
```

Opens `http://127.0.0.1:8788` (or the next free port). It can run next to the local app on 8787. After code changes, rebuild and restart the demo. It is limited on purpose: same UI, sample data, **no applications to companies**.

#### Useful scripts

| Script | Description |
|--------|-------------|
| `npm run dev` | Full local app (API + UI) |
| `npm start` | Same entry as `dev` |
| `npm run build:demo` | Build the public demo |
| `npm run start:demo` | Serve the demo (the process Render runs) |
| `npm test` | Native suite (`node --test`) |

</details>

### 1.2) Project structure [🔝](#index-)

<details>
  <summary>View details</summary>

```
autoapply/
├── Web UI
│   React + Vite: profile, search, apply, history and settings
├── Local API
│   Node.js in one process: persistence, search and fill
├── Form engine
│   Own Chromium (Playwright): fills fields; you submit
├── On-disk data
│   Profile, history, preferences and backups on the machine
├── Public demo
│   Render sandbox: fictional profile, no real accounts or submits
└── Documentation
    Spanish and English README (this repository)
```

This is not a microservice monorepo or a cloud ATS. One process, one UI, one managed browser. The demo **does not** reuse the personal boot path: it is a separate module, meant to be shown without leaking private data.

</details>

### 1.3) Technologies [🔝](#index-)

<details>
  <summary>View details</summary>

<br>

| **Technology** | **Version** | **Purpose** |
| -------------- | ----------- | ----------- |
| [React](https://react.dev/) | **19.x** | **UI** |
| [Vite](https://vite.dev/) | **8.x** | **Build and reload**; locally it is embedded in the server |
| [Node.js](https://nodejs.org/) | **≥ 22.13** | **Runtime** for the API and the demo |
| [Playwright](https://playwright.dev/) | **1.x** | **Chromium** for autofill (local version only) |
| [PDF.js](https://mozilla.github.io/pdf.js/) | **6.x** | **PDF résumé** reading |
| Native HTTP (`node:http`) | **built-in** | **Local API**, no Express |
| [Render](https://render.com/) | **Free** | **Public sandbox** for the demo |

**Built-in modules:** `node:http`, `node:fs` / `node:path`, `node:test`.

**Official docs:**

* React: <https://react.dev/>
* Vite: <https://vite.dev/>
* Playwright: <https://playwright.dev/>
* Node.js: <https://nodejs.org/docs/latest/api/>
* Render Blueprint spec: <https://render.com/docs/blueprint-spec>

The Render demo **does not** launch Playwright. The public walkthrough uses a same-origin test portal.

</details>

<br>

## Section 2) Usage flow and behavior

### 2.0) App flow [🔝](#index-)

<details>
  <summary>View details</summary>

<br>

The UI is the same idea locally and in the demo. The scope changes: **locally the flow is real** (portals, Chromium, applications you submit); **the demo is limited** to a catalog and a test form, for the usual reasons: no install, no leaked data, no other people’s vacancies.

| Environment | For |
|-------------|-----|
| **Local** | `http://127.0.0.1:8787` — personal use, Chromium, real portals |
| **Demo (Render)** | [autoapply-demo-1tjt.onrender.com](https://autoapply-demo-1tjt.onrender.com/) — fictional profile, no applications to companies |

1. Complete (or review) **My profile**: name, contact, experience, CV.
2. Pick a listing: paste it in **New application** or take it from **Job search**.
3. Optional: **Analyze** to see fields and suggested answers before opening the browser.
4. **Autofill** opens or reuses the tab in AutoApply Chromium and fills what it can resolve.
5. Review the real result: filled fields, pending required ones, validation and manual steps.
6. Handle CAPTCHA, codes and any control the app must not invent.
7. Submit **on the site**. AutoApply does not press the final button for you.
8. Confirm **I already submitted** to store it in history and enable duplicate checks.

Shortcuts: **Enter** analyzes; **Ctrl+Enter** (or **Cmd+Enter**) autofills. Several URLs build a queue; **Next in queue** moves when you want.

</details>

### 2.1) Profile and documents [🔝](#index-)

<details>
  <summary>View details</summary>

<br>

The profile is the product’s fuel. Name, last name, email and phone are enough to start; the rest (per-technology experience, education, availability, reusable answers) is what keeps forms from being half-empty.

| Piece | What it does |
|-------|----------------|
| Personal and professional data | Mapped onto text, dates, selects and radios |
| Per-technology experience | Years of Java are not treated as years of React |
| Saved answers | Repeated questions (work authorization, availability, pay) are reused |
| CV | PDF / DOC / DOCX, up to 8 MiB; more than one variant is allowed |
| Letter / comments | Base text; typed into a field or attached when the form asks |

The engine reads labels, names, accessible roles and nearby context. An empty placeholder does not count as an answer. Subjective scales and concrete project questions need their own reply: they are not filled with a generic paragraph.

Optional assistance (if an agent key is set) only runs when local rules are not enough. If it fails or is missing, the flow continues with the profile and the local lexicon. Always review suggested text before submitting.

</details>

### 2.2) Job search [🔝](#index-)

<details>
  <summary>View details</summary>

<br>

**Job search** queries public listings and filters them in AutoApply. A listed portal is not a guarantee it can always be scraped: if access is restricted, the app reports it and keeps what it did get.

Filters that matter in practice:

* Roles (up to three), location, work mode, contract type and seniority.
* Freshness: from a few hours to 30 days, or a custom window.
* Required, preferred and excluded technologies, with a catalog and custom options.
* English with a configurable ceiling (default is intermediate B1) plus extra languages.
* Words and companies to exclude.
* Hide listings you already confirmed as submitted.

**Save settings** persists the filter set on the local server. Editing the screen does not re-run the search: you have to search again. Cards show the criteria of **that** query, not filters you edited afterwards.

Each result shows company, date, matches and items still to review. **View listing** records the opportunity. **Take to apply** prepares New application. **I already applied** marks the submit without repeating the search.

</details>

### 2.3) Autofill and submit [🔝](#index-)

<details>
  <summary>View details</summary>

<br>

Autofill **is not** applying. Opening a listing, filling fields and confirming the submit are three different actions.

During fill:

* The listing tab is reused when possible.
* Login, verification or form screens are detected and handled accordingly.
* Saved accounts are used only on the domain they belong to.
* If a CAPTCHA or code appears, the app leaves the data filled and returns control. Solving it does not trigger a retry burst.

**Stop autofill** (red button) invalidates the run, waits for in-flight writes to finish and keeps the draft. It is not the same as closing the browser. Reloading the UI does not restart fill.

When the form has been verified as ready for review, an optional sound reminder repeats (15 / 30 / 60 s, or off). The sound does not submit anything: it only notifies.

After the portal’s own Submit, **I already submitted** closes the loop in AutoApply. Without that confirmation the listing does not enter submitted history and does not block a new attempt.

Common employment platforms (ATS and job boards) are recognized. Recognizing the URL is not full coverage of every variant of that site: forms change.

</details>

### 2.4) Privacy, data and limits [🔝](#index-)

<details>
  <summary>View details</summary>

<br>

#### What stays on your machine (local version)

Profile, portal accounts, history, search preferences and backups live in local files. The API listens on `127.0.0.1`. There is no multi-user auth and no public server for the personal app.

Credentials are stored as local JSON, **with no application-level encryption**. Protect access to the computer and to exported copies. `.gitignore` keeps data, backups and `.env` out of git.

A backup includes profile, accounts, histories, search settings and CVs as Base64. It **does not** include `.env`, the Chromium profile or the UI’s browser storage.

#### What the demo does (and does not)

* Fictional profile, invented listings, test portal.
* Per-visitor in-memory session with expiry.
* It does not read the personal disk, launch Chrome, or log into LinkedIn or any real employer.

#### Honest limits

* Final submit, CAPTCHA and MFA are manual.
* Search is not an exhaustive index or a 24/7 cron.
* Detecting a field does not replace reviewing the application.
* “Ready for review” does not mean the portal already received the CV.
* Render Free sleeps on inactivity; the first visit may take a while.

</details>

<br>

## Section 3) Testing, hosted demo and references

### 3.0) Functional test [🔝](#index-)

<details>
  <summary>View details</summary>

<br>

#### 3.0.1) Demo screenshots

<table>
  <tr>
    <td width="50%"><img src="../screenshots/profile.png" alt="Profile: load your details once" width="100%" /></td>
    <td width="50%"><img src="../screenshots/results.png" alt="Search results with match score" width="100%" /></td>
  </tr>
  <tr>
    <td width="50%"><img src="../screenshots/history.png" alt="Submitted applications history" width="100%" /></td>
    <td width="50%"><img src="../screenshots/settings.png" alt="Settings: sound alert and Stop" width="100%" /></td>
  </tr>
</table>

#### 3.0.2) Recommended walkthrough (demo)

1. Open **My profile** and look at (or edit) the fictional data. Do not load personal information into the public sandbox.
2. In **Job search**, move filters: freshness, technologies, languages, exclusions.
3. Open a listing or **Take to apply**. Catalog links render inside the test portal.
4. **Autofill**. Try **Stop** and continue by hand.
5. Submit the **fictional** application on the test portal. Confirm **I already submitted** (or **I already applied** on results).
6. **Reset demo** restores the initial example.

Test credentials for the fictional portal (they do not work on real sites):

`alex.rivera@example.invalid` / `Demo-Only-2026!`

#### 3.0.3) Automated tests

```bash
npm test
```

The suite covers filters, history, stop, persistence, demo isolation and UI walks with Playwright. You do not need AutoApply already running. Tests do not apply to companies or use real accounts.

#### 3.0.4) Process health

```bash
# local
curl -s http://127.0.0.1:8787/api/health

# local demo
curl -s http://127.0.0.1:8788/api/health

# Render demo
curl -s https://autoapply-demo-1tjt.onrender.com/api/health
```

</details>

### 3.1) Hosted sandbox (Render) [🔝](#index-)

<details>
  <summary>View details</summary>

<br>

Public demo: **[https://autoapply-demo-1tjt.onrender.com](https://autoapply-demo-1tjt.onrender.com/)**

The Render service **is the demo** (`build:demo` + `start:demo`), not the personal app. The cut is deliberate: locally it does search, fill and apply for real (you submit); here it never touches companies or real accounts. Free instance: HTTPS, fictional profile, no Playwright and no persistent disk.

| This yes | This no (Free) |
|----------|----------------|
| Walk profile, search, autofill and history with sample data | Apply to a real job |
| Per-visitor isolation while the container is awake | Keep yesterday’s data: sleep or redeploy resets the example |
| Health check at `/api/health` | Instant boot: the first visit may take ~30–60 s |
| Show the product to a reviewer | AutoApply Chrome, backups, personal CVs, real portal accounts |

Closing the browser **does not** wipe another visitor’s session. Sleep or a redeploy does reset the example. It is a sandbox to see the product, not an application tracker with history.

Blueprint: `render.yaml`. Node `22.14.0`. `NODE_ENV=production`.

</details>

### 3.2) Contributing [🔝](#index-)

<details>
  <summary>View details</summary>

<br>

1. Fork the project.
2. Create a branch (`git checkout -b feature/my-improvement`).
3. Commit (`git commit -m 'feat: short description'`).
4. Push (`git push origin feature/my-improvement`).
5. Open a Pull Request.

Do not commit secrets (`.env`, real profile, CVs, portal accounts, backups). Document product changes in both READMEs (this one + Spanish).

</details>

### 3.3) License [🔝](#index-)

<details>
  <summary>View details</summary>

<br>

ISC. Built by [Andrés Weitzel](https://github.com/andresWeitzel).

**Links:**

* **Spanish README:** [README.md](../../../README.md)
* **Sandbox (Render):** [autoapply-demo-1tjt.onrender.com](https://autoapply-demo-1tjt.onrender.com/)

</details>
