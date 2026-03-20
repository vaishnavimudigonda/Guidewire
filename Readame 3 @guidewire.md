# nexSure — Income Protection for Amazon Delivery Partners

**Guidewire DEVTrails 2026 | University Hackathon**
**Team: nexSure | Phase 1 Submission**

---

## Table of Contents

1. [Problem Statement](#1-problem-statement)
2. [Our Solution](#2-our-solution)
3. [Persona & Scenarios](#3-persona--scenarios)
4. [Application Workflow](#4-application-workflow)
5. [Weekly Premium Model](#5-weekly-premium-model)
6. [Parametric Triggers](#6-parametric-triggers)
7. [Platform Choice — Web App](#7-platform-choice--web-app)
8. [AI/ML Integration Plan](#8-aiml-integration-plan)
9. [Tech Stack](#9-tech-stack)
10. [Development Plan](#10-development-plan)
11. [Team Members](#11-team-members)

---

## 1. Problem Statement

Amazon delivery partners in Hyderabad work hard every single day to make sure packages reach on time. But there are days when things go completely out of their hands — a sudden heavy downpour, unbearable heat, a city-wide bandh, or even the Amazon app going down. On those days, they simply cannot work. And when they can't work, they don't earn.

The problem is that nobody compensates them for this. They lose 20–30% of their weekly income just because the weather was bad or there was a local strike. There's no insurance, no backup, nothing.

Here's what typically hits them in Hyderabad:

| What Happens | How It Affects Them |
|---|---|
| Heavy rain or flooding | Entire zones become inaccessible, deliveries get cancelled |
| Extreme heat above 43°C | Working outdoors for long hours becomes unsafe, slots get reduced |
| High pollution days (AQI 300+) | Cannot ride for extended hours without health risk |
| Curfew or local bandh | Cannot reach pickup or drop locations at all |
| Amazon app or platform outage | No orders get assigned, zero income for the day |

We wanted to fix this. Not with a complicated insurance process that takes weeks and paperwork — but something that just works automatically the moment a disruption happens.

---

## 2. Our Solution

We're building **nexSure** — a parametric income insurance platform built specifically for Amazon delivery partners in Hyderabad.

The core idea is simple: instead of asking the worker to file a claim and wait for approval, we watch for disruptions in real time. When a disruption crosses a defined threshold (say, rainfall hits 50mm in 3 hours), the system automatically detects it, checks if the worker was affected, and sends the payout directly to their UPI — no forms, no waiting, no confusion.

What nexSure does:
- Covers only income loss. We are not touching health, life, accident, or vehicle repairs — those are strictly out of scope.
- Charges a small weekly premium that fits within a gig worker's budget
- Uses AI to dynamically price premiums based on the worker's zone and risk history in Hyderabad
- Detects fraud automatically using GPS checks and anomaly detection
- Sends payouts instantly via Razorpay sandbox / UPI mock

The worker literally does nothing when a disruption hits. nexSure handles it end to end.

---

## 3. Persona & Scenarios

### Who are we building this for?

**Ravi Kumar, 28 years old**

Ravi has been delivering for Amazon in the Kukatpally and KPHB areas of Hyderabad for about 14 months. He earns around ₹700 on a good working day — roughly ₹4,900 a week when he works 6 days. He uses a budget Android phone, has a basic Jio data plan, and manages his finances week to week.

Last July, it rained heavily for two straight days. His zone was flooded. Amazon halted deliveries. Ravi lost ₹1,400 that week with no way to recover it. He had no idea something like income insurance even existed for people like him.

That's exactly the gap we're trying to fill.

---

### Scenario 1 — Heavy Rain in Kukatpally

It's a Tuesday in July. Ravi logs in at 9:30 AM ready to start. By 10 AM, Hyderabad records 65mm of rain within 3 hours. Kukatpally is flooded. Amazon suspends deliveries in the zone.

Without nexSure: Ravi loses his entire day's income of ₹700 with no recourse.

With nexSure:
1. Our weather API (OpenWeatherMap) detects rainfall crossed 50mm in Kukatpally.
2. The system checks Amazon's simulated platform data — deliveries are confirmed halted in that zone.
3. The fraud engine checks Ravi's last GPS location — he was in Kukatpally when the event hit.
4. Claim is automatically initiated. Ravi gets an SMS: "Disruption detected in your zone. ₹700 payout is being processed."
5. Money hits his UPI within minutes.

Ravi didn't file anything. He didn't call anyone. It just happened.

---

### Scenario 2 — Extreme Heat in May

It's mid-May. Hyderabad is at 45°C by noon. Amazon reduces delivery slots by 60% in outdoor zones due to a heat advisory. Ravi manages only 8 deliveries instead of his usual 25.

With nexSure:
1. Temperature API detects it has been above 43°C for more than 3 continuous hours.
2. Platform data (simulated) confirms 60% slot reduction in Ravi's zone.
3. System calculates partial income loss — roughly ₹420 for the day.
4. Proportional payout of ₹420 is processed automatically without Ravi doing anything.

---

### Scenario 3 — Unexpected Bandh

A bandh is announced in Hyderabad at 7 AM covering KPHB and nearby areas. Amazon suspends all operations for the day in those zones.

With nexSure:
1. A simulated government alert API picks up the bandh announcement.
2. Platform API confirms zero orders assigned in Ravi's zone.
3. Full day payout of ₹700 is automatically triggered and processed.

---

## 4. Application Workflow

Here is how a delivery partner experiences nexSure from the moment they sign up:

```
STEP 1 — ONBOARDING
Worker signs up using their Amazon Partner ID
Verifies identity via Aadhaar or phone OTP
Links their UPI account for receiving payouts
Selects their primary delivery zones in Hyderabad
        |
        v
STEP 2 — RISK PROFILING
AI engine looks at the worker's selected zones
Analyses historical flood, heat, and strike data for those zones
Assigns a risk score to the worker
Calculates their personalised weekly premium
        |
        v
STEP 3 — POLICY CREATION
Worker sees their weekly premium (₹49 / ₹79 / ₹99)
Selects a coverage tier
Weekly premium is auto-deducted every Monday via UPI
        |
        v
STEP 4 — REAL-TIME MONITORING (background, always on)
System continuously polls weather API, AQI API,
platform status API, and news alert API
Worker's GPS is tracked only during active delivery hours
        |
        v
STEP 5 — AUTOMATIC CLAIM TRIGGER
Disruption threshold is crossed in the worker's zone
System validates: GPS location + platform data + cluster check
Fraud score calculated — if below 70, auto-approved instantly
Worker notified via SMS and dashboard notification
        |
        v
STEP 6 — INSTANT PAYOUT
Income loss amount calculated based on disruption type and severity
Razorpay sandbox / UPI mock transfer initiated
Worker's dashboard updated with claim history and payout status
```

---

## 5. Weekly Premium Model

### Why weekly and not monthly?

Amazon delivery partners get paid every week. They plan expenses weekly. A monthly premium would feel like a big upfront cost for someone earning day to day. Weekly keeps it affordable and aligned with how they already manage money.

We also kept the premium amounts intentionally low — between 1% and 2% of weekly earnings. The worker should feel protected, not burdened.

### Our Three Tiers

| Plan | Weekly Premium | Max Weekly Payout | Who It's For |
|---|---|---|---|
| Basic Shield | ₹49 | ₹1,500 | New partners or workers in lower-risk zones |
| Standard Shield | ₹79 | ₹2,500 | Regular partners in moderate risk areas |
| Full Shield | ₹99 | ₹4,000 | High-earning partners in flood-prone zones like Kukatpally |

### How the AI Adjusts Pricing

The premium is not a flat number. Our AI engine looks at a few factors and adjusts it:

```
Final Weekly Premium = Base Premium
                     × Zone Risk Multiplier
                     × Season Factor
                     × Claim History Factor

Real Example for Ravi:
Base (Standard Shield):          ₹79
Zone multiplier (Kukatpally):    × 1.10   (historically flood-prone)
Season factor (July monsoon):    × 1.15
Claim history (clean record):    × 0.95   (small loyalty discount)

Final Premium this week = ₹79 × 1.10 × 1.15 × 0.95 ≈ ₹95
```

Ravi sees this number clearly before confirming. No surprises, no hidden charges.

Premium is deducted every Monday morning. Worker gets a confirmation SMS with what they're covered for that week.

---

## 6. Parametric Triggers

These are the 5 automated triggers we are building. When any of these conditions are met in the worker's active zone, a claim is initiated automatically — no action needed from the worker.

### Trigger 1 — Heavy Rain / Flooding

| | |
|---|---|
| Data Source | OpenWeatherMap API (free tier) |
| Condition | Rainfall exceeds 50mm within any 3-hour window in the worker's zone |
| Income Loss | 100% of that day's projected earnings |
| Validation | GPS confirms worker was in the zone + platform confirms delivery halt |

### Trigger 2 — Extreme Heat

| | |
|---|---|
| Data Source | OpenWeatherMap API |
| Condition | Temperature stays above 43°C for 3 or more continuous hours |
| Income Loss | Proportional — based on how much the platform reduced order slots |
| Validation | Platform API shows reduced assignment rate in the zone |

### Trigger 3 — Severe Air Pollution

| | |
|---|---|
| Data Source | AQICN API (free tier) |
| Condition | AQI exceeds 300 (Hazardous level) in Hyderabad |
| Income Loss | 100% for the day |
| Validation | Cross-checked with government AQI alert |

### Trigger 4 — Warehouse Closure / Zone Lockdown (Section 144)

| | |
|---|---|
| Data Source | Simulated Amazon warehouse status API + government alert API |
| Condition | Amazon fulfillment center shuts down (power cut, fire, local strike) OR Section 144 imposed in the worker's delivery zone blocking movement |
| Income Loss | 100% for the day — no pickups means no deliveries means zero earnings |
| Validation | Platform API confirms zero orders dispatched from that warehouse + government alert API confirms zone restriction |

This trigger is specific to e-commerce delivery. A food delivery partner can still pick up from a restaurant nearby — but an Amazon delivery partner has no alternative if their assigned fulfillment center is closed or their zone is locked down. There is literally no other pickup point available to them.

### Trigger 5 — Amazon Platform Outage

| | |
|---|---|
| Data Source | Simulated Amazon platform status API |
| Condition | Platform down for more than 2 hours during peak windows (10AM–2PM or 6PM–9PM) |
| Income Loss | Proportional to how much of the peak window was affected |
| Validation | Cluster check — multiple workers in the same zone must report the same issue |

---

## 7. Platform Choice — Web App

We went with a web app for a few straightforward reasons.

Most delivery partners use budget Android phones and may not want to install yet another app. A web app works directly in Chrome — nothing to download, no storage issues, no Play Store submission delay for us.

From a build perspective, a single React codebase is much easier to maintain across the 6-week timeline. We're also building an insurer dashboard alongside the worker view, and dashboards naturally suit web better than mobile.

We are building it as a Progressive Web App (PWA) so it still feels app-like on a phone — workers can add it to their home screen, get push notifications, and use some features offline.

The entire UI is being designed mobile-first for 375px screens since most workers access it on phones.

---

## 8. AI/ML Integration Plan

### Module 1 — Dynamic Premium Engine

This is what calculates how much each worker pays per week. In Phase 1 it's a weighted rule-based scoring system. In Phase 2 and 3 we'll evolve it into a proper trained regression model.

What it takes as inputs:
- Worker's registered delivery zones (Kukatpally, KPHB, Madhapur, etc.)
- Historical weather events in those zones over the last 12 months
- How often bandhs and strikes have hit those areas historically
- What month it is — monsoon season means higher risk
- Worker's past claim history — a clean record gets a small discount

What it outputs: A single personalised weekly premium the worker sees before confirming.

Phase-wise evolution:
- Phase 1: Rule-based weighted scoring (what we're submitting now)
- Phase 2: Train a regression model using synthetic Hyderabad zone-weather-claim data
- Phase 3: Real-time premium adjustment using live weather forecast data

---

### Module 2 — Fraud Detection Engine

We need to make sure workers aren't gaming the system by claiming disruptions that didn't affect them.

Here's what we check on every claim automatically:

| Check | What It Does |
|---|---|
| GPS Zone Match | Worker's last recorded GPS must place them within the disrupted zone when the event hit |
| Platform Cross-check | Amazon's simulated API must confirm deliveries were halted or reduced in that zone |
| Cluster Validation | Trigger only fires if multiple workers in the same zone are affected — one isolated claim raises a flag |
| Pattern Anomaly | If a worker claims every single week without exception, the ML model flags it as statistically suspicious |
| Duplicate Block | One claim per worker per calendar day — hard stop, no exceptions |
| Weather-GPS Mismatch | If GPS shows the worker in a dry zone while they're claiming rain disruption elsewhere, it's auto-flagged |

Every claim gets a fraud score from 0 to 100. Under 70 means auto-approved and paid immediately. Above 70 means it goes to manual insurer review.

---

### Real Fraud Scenarios We Thought About

One genuine concern we discussed while building this — what stops a worker from intentionally taking advantage of a disruption event to get money, even if they weren't actually affected? Since bandhs and weather events are public knowledge, a worker could technically know a trigger is about to fire and try to game it.

Here's how nexSure handles each of these situations:

**Scenario 1 — Worker is not in the affected zone but tries to claim**

Say a bandh is announced in Kukatpally. Ravi was actually working fine in Madhapur that day where there was no disruption. He tries to claim because he knows the trigger fired in Kukatpally.

nexSure catches this because his GPS last recorded him in Madhapur, not Kukatpally. The GPS zone match check fails. Fraud score jumps immediately. Claim is rejected and flagged for review.

**Scenario 2 — Worker actually works during the disruption but still claims**

The bandh is announced but Ravi goes out anyway and completes 15 deliveries. Then at the end of the day he tries to claim full day income loss.

nexSure catches this because the platform API shows active delivery completions against his partner ID during the disruption window. If he was working, there is no income loss. The system calculates his actual loss as zero and no payout is triggered.

**Scenario 3 — Worker claims on every possible disruption every single week**

Ravi claims on every rain day, every hot day, every trigger that fires — even borderline ones. He's trying to treat it like free money.

nexSure catches this through pattern anomaly detection. If 200 workers are in his zone and only Ravi claims on every single disruption without exception, the ML model flags his claim pattern as statistically unusual. His fraud score crosses 70 and every future claim goes to manual review until his pattern normalises.

**Scenario 4 — A group of workers plan together to all claim the same event**

Five friends who deliver in the same zone decide they'll all claim a bandh even though only two of them were genuinely unable to work.

nexSure catches this through cluster validation combined with individual GPS checks. Each claimant's GPS is checked independently. Those whose GPS shows them in a different zone or shows active movement during the disruption window get flagged individually. The system doesn't treat a group claim any differently — every worker's data is verified on its own.

**Why this works — the parametric design itself is the biggest protection**

The most important thing here is that the worker cannot manually file a claim at all. There is no "claim now" button. The only way a payout happens is when all of these are true at the same time:

1. External data (weather API or government alert) confirms the disruption actually happened
2. Worker's GPS confirms they were physically in the affected zone
3. Platform data confirms deliveries were actually halted in that zone
4. Fraud score is below 70

If even one of these four conditions fails, the payout does not happen. The system is designed so that gaming it intentionally is harder than just going to work.

---

### Module 3 — Predictive Risk Dashboard (Phase 3 Plan)

Using 7-day weather forecasts, the system will predict which zones are likely to see disruptions in the coming week. This helps workers in risky zones know to stay covered, and lets the insurer forecast expected payouts ahead of time.

---

## 9. Tech Stack

### Frontend
| Technology | Why We Chose It |
|---|---|
| React.js | Fast to build, component-based, good for both worker and admin views |
| Tailwind CSS | Makes mobile-responsive design quick and clean |
| PWA (Service Workers) | App-like experience on the worker's phone without needing to install anything |
| Recharts | Lightweight and clean charts for the analytics dashboard |

### Backend
| Technology | Why We Chose It |
|---|---|
| Node.js + Express.js | REST APIs for all core platform operations |
| Python + FastAPI | Separate microservice dedicated to AI/ML — premium engine and fraud detection |
| JWT Authentication | Secure login for both workers and the insurer admin |

### Database
| Technology | Why We Chose It |
|---|---|
| PostgreSQL | Main database for workers, policies, claims, and payout records |
| Redis | Caching real-time trigger states and handling session data |

### External APIs
| API | What It Does | Mode |
|---|---|---|
| OpenWeatherMap | Rainfall and temperature data for triggers | Free tier (live) |
| AQICN | Air quality index for pollution trigger | Free tier (live) |
| Amazon Platform API | Order assignment and zone status | Simulated / mocked |
| News Alert API | Curfew and bandh detection | Simulated |
| Razorpay | Payout processing | Test mode / sandbox |
| Google Maps | Zone mapping and GPS validation | Free tier |

### AI/ML Libraries
| Library | Purpose |
|---|---|
| scikit-learn | Premium risk model (Phase 2 onwards) |
| Pandas + NumPy | Data processing for zone-risk calculations |
| Custom rule engine | Phase 1 fraud detection and premium scoring |

### Hosting & DevOps
| Tool | Purpose |
|---|---|
| GitHub | Version control — this same repo used across all 3 phases |
| Vercel | Frontend deployment |
| Render | Backend Node.js and Python services |
| Docker | Containerising backend services for consistent deploys |

---
## 11. Team Members

| Name | Role | Contact |
|---|---|---|
| [Saania] | Full Stack Developer | [saania_shaik@srmap.edu.in] |
| [M.Vaishnavi] | AI/ML Engineer | [vaishnavi_mudigonda@srmap.edu.in] |
| [Anusha] | UI/UX Designer | [anusha_sunaapu@srmap.edu.in] |
| [Poojitha and Rsuhi] | Backend & DevOps | [poojitha_gangula@srmap.edu.in
                                             rushi_mahidhar@srmap.edu.in] |

---

**Coverage Exclusions**

nexSure covers income loss only. We do not cover health insurance, life insurance, accident medical bills, vehicle repairs, or any personal expenses. These are outside the scope of this platform as per the hackathon guidelines.

---

*Built for the people who deliver your packages — rain, heat, or anything else the city throws at them.*
