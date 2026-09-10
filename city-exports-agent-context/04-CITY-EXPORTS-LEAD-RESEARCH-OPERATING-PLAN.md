# City Exports — Lead Research Operating Plan

**Prepared:** 10 September 2026  
**Purpose:** Simple, repeatable AI-assisted buyer discovery and verification

## 1. The operating idea

Use two independent research agents and one control agent:

1. **Discovery agent:** finds candidate companies.
2. **Verification agent:** challenges the candidates and checks evidence independently.
3. **Control agent:** deduplicates, audits, ranks and produces the final shortlist.

The two research agents must not simply repeat each other's conclusions. Independent checking is important because a plausible company description can still be the wrong buyer, a reseller or an inactive account.

## 2. Recommended account division

### Claude account 1 — Discovery Scout

Search one narrow product/category at a time. Find approximately 25–40 raw candidates through:

- competing distributors
- importer and wholesaler searches
- brands and labels traced back to importers
- ingredient users, processors and packers
- private-label and contract-production companies
- association/member and event lists
- supplier and transparency reports
- published sourcing requests

For every candidate, record the exact product evidence, legal identity if available, business model, source URLs and date checked. Mark buying intent as unknown unless a dated request exists.

### Claude account 2 — Independent Verification Scout

Receive a candidate list or conduct a separate search route. Do not assume the candidates are valid.

For each candidate:

- verify the official website and legal identity
- verify the exact product, not a neighbouring category
- determine whether the company imports, distributes, manufactures, packs or only retails
- check current activity and supply-chain disclosures
- determine whether external sourcing is plausible
- find the correct procurement route
- label every important statement `FACT`, `INFERENCE` or `UNKNOWN`
- reject duplicates, inactive companies, weak fits and origin mismatches

### ChatGPT — Control Tower

Read the master context and source documents, then audit both outputs.

The control agent must:

- remove duplicates and previously listed organisations
- verify or flag HS-code and import-number claims
- separate import proof, buyer/business fit and response proof
- identify contradictions between sources
- classify each account as Lane A, Lane B or reject/hold
- select only the strongest 7–8 accounts
- identify the correct person or official procurement route
- provide one next action per account
- avoid outreach unless the user explicitly asks for it

## 3. Tool stack

### Public-web search and extraction — Firecrawl

Use Firecrawl or equivalent web-research infrastructure to search, scrape, crawl and extract structured information from public pages, PDFs and dynamic websites.

Use it for discovery and evidence collection, not as a substitute for judgement. Save the source URL and date checked for every retained fact.

### Difficult websites and portals — browser control

Use a browser agent when a source requires clicking, pagination, a dynamic interface or the user's own authenticated session.

The user must sign in themselves. Never request or store account passwords in chat.

### Official market/import statistics

Prefer official sources such as Statistics Norway, UN Comtrade and Eurostat/Comext for country-level values, quantities, partner countries and HS-code trends.

Confirm that the HS code matches the exact product. Accurate data under the wrong code is still the wrong answer.

### Shipment-level evidence

Consider Volza, Panjiva or ImportGenius when shipment-level evidence is necessary. Check meaningful Norway coverage before paying. ImportYeti is primarily useful for its covered markets and should not automatically be treated as a Norway solution.

Shipment data can contain incomplete records, broad descriptions, consolidated shipments and classification errors. Use it as supporting evidence.

### Contact enrichment

Apollo, Hunter or similar tools may help identify procurement, category, sourcing and purchasing personnel and verify business emails.

Use them only after the company has passed business-fit screening. Contact enrichment does not prove that the company wants the product.

### Storage

Keep one master spreadsheet or database. Do not let each AI account maintain a separate private list.

Recommended columns:

`Company | Legal name | Website | Product | HS code | Buyer type | Official evidence | Import evidence | Shipment evidence | Procurement contact | Contact source | Intent lane | Confidence | Date checked | Unknowns | Next action | Status`

## 4. Daily research cycle

### Step 1 — Define the search card

Before starting agents, write:

- country
- exact product
- grade/specification
- intended use
- acceptable origin
- known HS code or competing codes
- existing companies to exclude
- what counts as a useful lead

Example: `Norway | shelled cashews | foodservice/ingredient supply | Indian origin possible | exclude all companies in current Norway files`.

### Step 2 — Run two independent searches

Ask the Discovery Scout for 25–40 candidates. Ask the Verification Scout to investigate a separate route or independently challenge the candidate set.

Do not broaden into unrelated categories simply to hit a number.

### Step 3 — Control-agent audit

Send both outputs to ChatGPT with the current context and source documents. Request a final 7–8 account shortlist with evidence, unknowns and next action.

### Step 4 — Human confirmation

The user opens the final source pages and confirms:

- the company is active
- the product fit is exact
- the business is a plausible buyer or purchasing intermediary
- the contact route is relevant
- the origin is commercially realistic
- the next action is clear

### Step 5 — Qualification outreach

Only after human confirmation, contact the correct route with a narrow qualification message. Ask about specification, quantity, timing, sample/evaluation and supplier onboarding. Do not lead with a generic catalogue.

## 5. Output thresholds

Use these labels:

- **Raw candidate:** found but not checked sufficiently.
- **Screened prospect:** product and business fit supported.
- **High-confidence target:** identity, exact product fit, current activity and procurement route supported.
- **Active opportunity:** dated request, RFQ, buyer confirmation, sample request or response.
- **Rejected/hold:** weak evidence, duplicate, inactive, inaccessible, impossible freight or origin mismatch.

The expected afternoon result is 7–8 high-confidence targets, not a promise of 7–8 active orders.

## 6. Prompt — Discovery Scout

> Read `AGENTS.md` and `00-CITY-EXPORTS-AGENT-CONTEXT.md`. Find additional Norwegian companies for [EXACT PRODUCT] within the existing City Exports categories. Do not count companies already present in the source documents. Search competing distributors, importers, ingredient users, processors, packers, private-label companies, contract manufacturers, industry networks, supply-chain reports and dated sourcing requests. Verify the exact product fit using primary sources. Return 25–40 candidates with legal identity, website, location, organisation number where available, exact product evidence, buying model, source URLs, date checked, buying-intent status, origin fit, procurement route and next action. Mark buying intent unknown unless there is a dated request. Do not infer demand from retail listings, stockouts or retail prices. Do not invent contacts or prices.

## 7. Prompt — Verification Scout

> Read `AGENTS.md` and `00-CITY-EXPORTS-AGENT-CONTEXT.md`. Independently verify these possible Norwegian buyers for [EXACT PRODUCT]: [PASTE CANDIDATES]. Do not assume they are valid. Check official product evidence, legal identity, current activity, business model, external sourcing, origin compatibility and procurement route. Reject duplicates, inactive companies, retailers without procurement evidence, weak product fits and origin mismatches. For each survivor, separate FACT, INFERENCE and UNKNOWN. Find a named procurement/category/sourcing person where possible; otherwise provide the official route to purchasing. Never guess an email address. Return a confidence score and one next action. Do not call a prospect an active buyer without a dated request, RFQ or buyer response.

## 8. Prompt — ChatGPT Control Tower

> Read `AGENTS.md`, `00-CITY-EXPORTS-AGENT-CONTEXT.md`, the three Norway source documents and the two agent outputs below. Audit the candidates for City Exports. Remove duplicates and previously listed organisations. Separate import/market proof, buyer/business fit and response proof. Verify important market numbers against official trade sources where possible. Reject weak or unsupported records. Select only the strongest 7–8 accounts. For each, provide: legal identity, exact product fit, buying model, evidence URLs and dates, origin fit, intent lane, correct procurement route, known facts, unknowns, one specific reason to approach and one next action. Do not invent demand, prices, contacts or supplier relationships. Do not draft outreach unless explicitly requested.

## 9. What the user must connect or provide

Minimum setup:

1. Firecrawl or equivalent web extraction access.
2. A shared master spreadsheet/database.
3. Browser access for difficult or authenticated portals.
4. One shipment-data trial only after selecting the exact product and confirming Norway coverage.
5. Apollo or another enrichment service only after company screening, for personnel/contact discovery.

Do not provide passwords in chat. Use OAuth or secure connector settings. Keep paid tools limited until the first controlled test proves that the data improves decisions.

## 10. Success criteria

The system should produce fewer, better accounts with traceable evidence. A successful cycle tells the user:

- which companies genuinely fit the exact product
- what evidence supports that conclusion
- whether current buying intent is known or unknown
- who should be approached
- what must be learned in the first conversation
- what evidence is still missing

