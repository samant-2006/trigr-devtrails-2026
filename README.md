# TRIGR — *When the Weather Strikes, Your Payout Already Knows*

> Guidewire DEVTrails 2026 · Chennai · 4-Member Team  
> Parametric Income Insurance · Behavioral AI Engine · Food Delivery Segment

\---

## Why We Built This

We live in Chennai.

We've watched delivery partners park their bikes on Velachery Main Road during October northeast monsoons, sitting under shop awnings, staring at their phones. Orders stopped. Earnings gone. Nothing to do but wait.

The existing conversation around gig worker insurance is stuck on *what* happened — "it rained, pay the worker." We asked a different question:

**What if the system already knew *how much* that specific worker was going to earn tonight — before the rain even hit?**

That's TRIGR. Not generic parametric insurance. Behavioral parametric insurance — where every payout is triggered automatically, calculated personally, and settled instantly.

\---

## The Name

Every payout in TRIGR is trigger-based. No human files a claim. No adjuster reviews it. The weather triggers it, the AI validates it, the money moves. We are literally a trigger engine for income protection.

**The name is the product.**

\---

## The Core Idea: Worker DNA

Every delivery partner has a **behavioral fingerprint** — call it their Worker DNA.

Muthu works 6 PM to 11 PM, earns peak income during dinner rush, operates primarily across Adyar and Besant Nagar, and historically completes 18–22 orders on Tuesday nights. When a cyclone warning shuts down Chennai at 8 PM on a Tuesday, Muthu doesn't lose "average gig worker income." He loses *his* income — ₹740, not the generic ₹400 a flat-rate system would pay.

TRIGR's Behavioral AI builds this fingerprint from day one and refines it every week. The premium Muthu pays is calibrated to his pattern. The payout he receives is calibrated to his actual projected loss.

This is the gap every other solution in this space ignores.

\---

## Who We're Building For

**Persona: Zomato / Swiggy Food Delivery Partners in Chennai**

Chennai is not a generic Indian city for this problem. It has:

* The most rain-disrupted delivery ecosystem in South India (northeast monsoon, Oct–Dec)
* Dense urban zones where hyperlocal disruption is the norm — it can flood in Velachery while T Nagar is completely dry
* A large base of full-time delivery partners who depend entirely on weekly earnings

Meet our three core personas:

**Muthu, 28 — Full-timer, Adyar zone**
Works evenings and weekends. 5 days a week, 5–6 hours/day. Lost 3 full evenings last October to rain. Estimated loss: ₹2,100 with zero compensation.

**Priya, 34 — Single earner, Anna Nagar zone**
Works the full day shift. Her family depends entirely on her weekly payout. A disruption isn't inconvenient — it's a crisis. She needs an immediate payout, not a claim process.

**Karthik, 22 — Part-timer, OMR corridor**
Works lunch and dinner rush only. His loss window is narrow — 2 hours of disruption during his peak slot matters more than 6 hours at off-peak.

> TRIGR treats these three differently. Same product, different intelligence.

\---

## What Makes TRIGR Different: The Behavioral Engine

Most parametric systems work like this:

```
IF rainfall > threshold THEN pay flat amount
```

TRIGR works like this:

```
IF rainfall > threshold in worker's active zone
AND worker was in active coverage window
THEN payout = f(worker's projected earnings for this slot,
                disruption severity,
                historical zone loss data,
                current week's coverage tier)
```

### The Behavioral Profile — Built Over Time

At onboarding, we collect:

* Preferred working hours and days
* Primary operating zones (pin code level)
* Declared weekly earnings band

After week 1, the AI begins learning:

* Actual earning patterns vs declared (establishes fraud baseline)
* Which time slots generate peak income for this specific worker
* Zone-level disruption exposure score (some Chennai zones flood at 30mm rainfall; others need 80mm)

After week 4:

* Fully personalized risk profile is active
* Dynamic weekly premium reflects the worker's actual risk exposure
* Payout is calibrated to *when* in the worker's shift the disruption occurred

**A disruption at 7:30 PM for a dinner-rush worker hits harder than the same disruption at 2 PM. TRIGR knows the difference.**

\---

## Weekly Premium Model

We price weekly because gig workers earn weekly. No exceptions. No monthly lock-in.

### Coverage Tiers

|Tier|Weekly Premium|Max Weekly Payout|Best For|
|-|-|-|-|
|Flex Shield|₹35/week|₹700|Part-timers and low-hour workers|
|Core Shield|₹59/week|₹1,400|Regular full-shift workers|
|Full Shield|₹89/week|₹2,500|Full-time primary earners|

### How the Behavioral Engine Adjusts the Premium

```
Final Weekly Premium = Base Tier Rate
                       × Zone Risk Multiplier (0.8 – 1.3)
                       × Season Factor (1.0 – 1.4 during monsoon)
                       × Behavioral Loyalty Discount (0.85 – 1.0)
```

* **Zone Risk Multiplier**: Velachery = 1.3 (notorious flooding). Porur = 1.1. OMR elevated stretch = 0.85.
* **Season Factor**: Oct–Dec northeast monsoon period carries a 1.35 premium adjustment
* **Behavioral Loyalty Discount**: Workers with 8+ weeks of clean history receive progressive discounts

Premium is collected via UPI AutoPay every Monday at 9 AM — aligned with the worker's weekly earnings cycle.

\---

## Parametric Triggers

No manual claims. Ever. TRIGR monitors continuously and fires automatically.

|Trigger ID|Event|Data Source|Threshold|Coverage Window|
|-|-|-|-|-|
|T-01|Heavy Rainfall|OpenWeatherMap API|> 45mm / 3hrs in worker's pin code|Active shift hours only|
|T-02|Cyclone / Storm Alert|IMD RSS Feed|Official red/orange alert for Chennai district|Full day|
|T-03|Severe Pollution|OpenAQ API|AQI > 350 in city zone|Active shift hours|
|T-04|Extreme Heat|OpenWeatherMap|Temp > 43°C between 11 AM – 4 PM|Afternoon shift only|
|T-05|Social Disruption|Mock Alert API|Curfew or bandh in operative pin codes|Declared disruption hours|

### The Chennai-Specific Trigger Logic

Generic platforms apply city-level triggers. TRIGR applies **pin-code-level triggers.**

In Chennai, Velachery can have standing water while Nungambakkam is completely passable. A city-level trigger would either over-pay workers in unaffected zones or under-compensate those hit hardest. TRIGR resolves this by:

* Mapping each worker's **active delivery zone** (top 3 pin codes by order history)
* Applying the trigger only if the disruption intersects the worker's specific zone
* Weighting the payout by the zone-disruption overlap percentage

\---

## AI/ML Architecture

### Module 1 — Behavioral Profiling Engine

* **Algorithm:** K-Means clustering for worker segmentation → Random Forest for individual earnings prediction
* **Input Features:** Hour of day, day of week, operating zone, historical earnings, platform tenure
* **Output:** Projected earnings per time slot per worker — used directly in payout calculation
* **Retraining:** Every Monday before the premium deduction cycle runs

### Module 2 — Dynamic Premium Calculator

* **Algorithm:** XGBoost Regressor
* **Input Features:** Zone risk score, season, coverage tier, historical claim frequency, loyalty weeks
* **Output:** Personalized weekly premium, always clipped within the declared tier range — no silent upgrades

### Module 3 — Fraud Detection Engine

* **Algorithm:** Isolation Forest (anomaly detection)
* **Signals Monitored:**

  * GPS zone mismatch at time of trigger (worker claims Chennai North disruption, last ping was Tambaram)
  * Coverage purchased less than 6 hours before a weather event already in the public forecast
  * Claim pattern significantly above the worker's own behavioral baseline
  * Statistically improbable cluster of claims from the same pin code for a single event
* **Output:** Fraud risk score from 0–100. Score above 70 goes to manual review. Score above 90 is auto-rejected with an appeal option available to the worker.

### Module 4 — Zone Intelligence Layer

* **Type:** Geospatial analytics
* **Data:** Historical IMD rainfall records for Chennai (2015–2024), GCC flood zone maps
* **Output:** Per-pin-code risk score updated quarterly
* **Used In:** Premium zone multiplier and trigger threshold calibration per zone

\---

## Platform: Mobile-First PWA

**Why PWA over a native app:**

Delivery partners switch phones frequently and avoid downloading unfamiliar apps. A PWA that opens via a WhatsApp-shared link has zero adoption friction — open the link, onboard in 3 minutes, covered by Monday morning.

**Core Screens:**

1. **Onboard** — Aadhaar-lite verification (mocked), working hours declaration, zone selection, tier choice
2. **Weekly Dashboard** — This week's coverage status, earnings protected so far, next premium date
3. **Trigger Feed** — Live disruption alerts active in the worker's operating zone
4. **Payout History** — Every automated payout with the triggering event linked and timestamped
5. **Profile \& Settings** — Update working zones, change coverage tier, pause coverage

\---

## Tech Stack

|Layer|Technology|Reason|
|-|-|-|
|Frontend|React.js PWA|Mobile-first, installable on low-end Android|
|Styling|Tailwind CSS|Fast responsive build|
|Backend|Python FastAPI|Async, lightweight, ML-native|
|Task Queue|Celery + Redis|Background trigger monitoring every 15 minutes|
|Database|PostgreSQL|Relational data for policies, claims, payouts|
|ML|scikit-learn + XGBoost|Proven, free-tier deployable|
|Weather|OpenWeatherMap (free tier)|Reliable pin-code level queries|
|Pollution|OpenAQ (free, open source)|City-level AQI data|
|Storm Alerts|IMD RSS Feed|Official cyclone and red-alert data|
|Payments|Razorpay Test Mode|UPI payout simulation|
|Hosting|Render (backend) + Vercel (frontend)|Free tier, sufficient for demo|
|CI/CD|GitHub Actions|Auto-deploy on push to main|

\---

## Development Roadmap

### Phase 1 — Now (Ideation \& Foundation) ✅

* \[x] Chennai-specific persona research completed
* \[x] Behavioral AI architecture designed
* \[x] Weekly premium model defined
* \[x] Zone-level trigger logic designed
* \[x] Tech stack finalized
* \[ ] Low-fidelity wireframes
* \[ ] Repository structure initialized

### Phase 2 — Weeks 3–4 (Build Core)

* \[ ] Worker onboarding flow (3-minute registration)
* \[ ] Behavioral profiling engine v1 (clustering + earnings prediction)
* \[ ] Weekly premium calculator with zone risk multiplier
* \[ ] Trigger monitoring engine (Celery jobs, 15-min polling)
* \[ ] Automated payout flow via Razorpay sandbox
* \[ ] Basic fraud scoring (GPS mismatch + coverage timing checks)
* \[ ] Worker dashboard (coverage status, payout history)

### Phase 3 — Weeks 5–6 (Scale \& Polish)

* \[ ] Full Isolation Forest fraud detection deployed
* \[ ] Zone intelligence layer with Chennai historical rainfall data
* \[ ] Admin dashboard (loss ratios, zone heatmaps, fraud alert queue)
* \[ ] Simulated disruption demo — trigger a fake storm, watch the auto-payout fire
* \[ ] Final pitch deck

\---

## Financial Viability

|Metric|Estimate|
|-|-|
|Chennai active Zomato/Swiggy partners|\~85,000|
|Target Year 1 adoption|8,000 workers|
|Average weekly premium|₹59|
|Weekly premium revenue at target|₹4.72 Lakhs|
|Annual revenue run rate|₹2.45 Crore|
|Estimated claims payout ratio|38% of premiums|
|Gross margin estimate|\~45%|

The behavioral engine reduces over-payout to workers in unaffected zones by an estimated 28% compared to city-level parametric systems — directly improving the loss ratio and making the business sustainable.

\---

## What TRIGR is NOT

We want to be explicit about scope boundaries:

* ❌ Not health insurance
* ❌ Not accident or injury coverage
* ❌ Not vehicle repair or maintenance payouts
* ❌ Not life insurance
* ✅ Only income lost during verified, trigger-based external disruption events

\---

## Team

> \\\\\\\\\\\\\\\[WEB WEAVERS]
> \\\\\\\\\\\\\\\[SAMANT KUMAR MISHRA] · \\\\\\\\\\\\\\\[ABHINAV SINGH BHADURIA] · \\\\\\\\\\\\\\\[KRISHAN KUMAR] · \\\\\\\\\\\\\\\[ALPHA SOLOMON]
> \\\\\\\\\\\\\\\[SRM INSTITUTE OF SCIENCE AND TECHNOLOGY, KTR], Chennai

\---

## Demo Video

> \\\\\\\\\\\\\\\[2-minute video link — YouTube unlisted / Google Drive]

\---

*Guidewire DEVTrails 2026 — Unicorn Chase
Built in Chennai. For Chennai. For every delivery partner waiting under a shop awning.*

