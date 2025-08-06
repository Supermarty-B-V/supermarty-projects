# SuperMarty: Phased MVP Proposal & Roadmap

**Document Version:** 4.0
**Date:** 2025-06-17
**Author:** Project Manager

---

## 1. Executive Summary

### 1.1. Vision
To become the leading intelligent grocery shopping assistant in the EU, helping users save money, eat healthier, and simplify their meal planning through a seamless, AI-driven experience.

### 1.2. Proposal Overview
This document outlines a revised, comprehensive 7-month phased development plan to bring the SuperMarty vision to market. The previous plan has been updated to a more granular, de-risked 5-phase MVP approach that prioritizes rapid validation and incremental replacement of the existing technical landscape.

This new strategy begins with a prototyping phase (MVP-0) to validate the user experience, followed by a Flutter app release that leverages the existing backend (MVP-1). Subsequent phases will systematically replace the backend with a modern Supabase and custom scraping solution (MVP-2), replace the admin dashboard with Retool (MVP-3), and finally integrate the core SuperMarty AI features (MVP-4).

This proposal provides a detailed breakdown of features for each MVP phase, required resources, timeline, and estimated costs to deliver the full MVP scope, totaling **1,520 hours** at an estimated cost of **€152,000**.

---

## 2. Strategic Approach & Recommendations

### 2.1. Phased MVP Rollout
To manage risk, accelerate time-to-market, and deliver value incrementally, the project will be executed in five distinct MVP phases:

* **MVP-0: Full Prototype with Mock Data:** A rapid, low-cost phase to build a high-fidelity, interactive prototype. This allows for early user testing and UI/UX validation before committing to full-stack development.
* **MVP-1: Flutter App with Existing Backend:** Develop the full Flutter application connecting to the existing backend provided by the other party. This de-couples frontend and backend development, allowing for parallel progress and getting a native app into users' hands quickly.
* **MVP-2: Supabase Backend & Scraping Solution:** A strategic replacement of the other party's backend with our own scalable Supabase infrastructure and proprietary scraping solution. This gives us full control over our data, performance, and feature development velocity.
* **MVP-3: Retool Dashboard:** Replace the existing Laravel dashboard with a more flexible and rapidly developed Retool dashboard for internal data management and operations.
* **MVP-4: SuperMarty AI Integration:** Integrate the core AI-powered personalization features, delivering on the primary "health-first" value proposition.

### 2.2. Technology Stack
* **Frontend:** Flutter for a single codebase across Web, iOS, and Android.
* **Backend:** Supabase for its integrated database, authentication, and serverless functions, augmented by a custom Python service for scraping and matching.
* **Admin Panel:** Retool for rapid development of internal data management dashboards.
* **AI & Matching:** Python services using Sentence-BERT for NLP matching and integrating with a third-party LLM for the AI assistant.

---

## 3. MVP Phases & High-Level Roadmap

**Total Timeline:** 7 Months

| Phase    | MVP Phase                                    | Duration    | Key Goals & Deliverables                                                                                                         |
| :------- | :------------------------------------------- | :---------- | :------------------------------------------------------------------------------------------------------------------------------- |
| **MVP-0**| **MVP Phase 0:** Prototyping & Validation    | 1 Month     | Validate UI/UX with a high-fidelity, clickable web prototype using mock data. Finalize design direction.                          |
| **MVP-1**| **MVP Phase 1:** Flutter App on Existing Backend  | 1.5 Months  | Launch a functional cross-platform app using the current backend. Validate user-facing experience with real data.               |
| **MVP-2**| **MVP Phase 2:** Backend Replacement          | 2.5 Months  | Replace the third-party backend with our proprietary Supabase and scraping solution. Achieve technical independence.             |
| **MVP-3**| **MVP Phase 3:** Admin Dashboard Replacement  | 0.5 Months  | Replace the Laravel dashboard with a flexible Retool application for internal teams.                                              |
| **MVP-4**| **MVP Phase 4:** AI & Personalization         | 1.5 Months  | Implement health profiles and the SuperMarty AI assistant. Ensure full GDPR compliance.                                          |

---

## 4. Detailed Feature Breakdown & Estimations

### MVP Phase 0: Prototyping & Validation (Total: 178 hours)
| Feature / Task                | Description                                                                  | PM (h) | Backend (h) | Frontend (h) | UI/UX (h) | Total (h) |
| :---------------------------- | :--------------------------------------------------------------------------- | :----- | :---------- | :----------- | :-------- | :-------- |
| Project & Team Onboarding     | Setup repositories, PM tools, communication channels.                        | 10     | 4           | 4            | 0         | 18        |
| Define Mock API Contract      | Specify the JSON structure for all data models to be used by the prototype.  | 0      | 16          | 8            | 0         | 24        |
| UI/UX Design for Prototype     | Create high-fidelity mockups for all screens in the user journey.             | 0      | 0           | 0            | 40        | 40        |
| Build Interactive Prototype   | Develop a clickable web prototype using a rapid UI tool, powered by mock JSON.| 0      | 0           | 80           | 0         | 80        |
| Stakeholder Review & Feedback | Conduct review sessions and consolidate feedback to inform MVP-1.             | 16     | 0           | 0            | 0         | 16        |
| **MVP Phase 0 Totals**        |                                                                              | **26** | **20**      | **92**       | **40**    | **178**   |

### MVP Phase 1: Flutter App on Existing Backend (Total: 300 hours)
| Feature / Task                     | Description                                                                   | PM (h) | Backend (h) | Frontend (h) | Total (h) |
| :--------------------------------- | :---------------------------------------------------------------------------- | :----- | :---------- | :----------- | :-------- |
| Existing API Discovery & Client    | Analyze and document the current Laravel backend APIs. Build a Flutter client.| 0      | 40          | 0            | 40        |
| Flutter App UI Implementation      | Build all user-facing screens from the prototype using Flutter.              | 0      | 0           | 220          | 220       |
| Project Management & QA            | Sprints planning, coordination, reviews, and testing against the live API.    | 40     | 0           | 0            | 40        |
| **MVP Phase 1 Totals**             |                                                                               | **40** | **40**      | **220**      | **300**   |

### MVP Phase 2: Backend Replacement (Total: 600 hours)
| Feature / Task                      | Description                                                                 | PM (h) | Backend (h) | Frontend (h) | Total (h) |
| :---------------------------------- | :-------------------------------------------------------------------------- | :----- | :---------- | :----------- | :-------- |
| Supabase Backend Build              | Setup Supabase, DB schema, and build all new APIs to replace the old backend.| 0      | 240         | 0            | 240       |
| Scraping & Matching Service         | Build the Python service for data scraping and product matching.            | 0      | 220         | 0            | 220       |
| Flutter App Refactor                | Update the Flutter app's data layer to connect to the new Supabase backend. | 0      | 0           | 80           | 80        |
| Project Management & QA             | Sprints planning, data migration oversight, and full regression testing.     | 60     | 0           | 0            | 60        |
| **MVP Phase 2 Totals**              |                                                                              | **60** | **460**     | **80**       | **600**   |

### MVP Phase 3: Admin Dashboard Replacement (Total: 100 hours)
| Feature / Task                 | Description                                                                | PM (h) | Backend (h) | Frontend (h) | Total (h) |
| :----------------------------- | :------------------------------------------------------------------------- | :----- | :---------- | :----------- | :-------- |
| Retool Dashboard Build         | Build all necessary admin dashboards in Retool for internal operations.    | 0      | 0           | 60           | 60        |
| Backend Support for Retool     | Create specific database views or functions to simplify data fetching.     | 0      | 30          | 0            | 30        |
| Project Management & Training  | Coordinate rollout and train internal admin users.                         | 10     | 0           | 0            | 10        |
| **MVP Phase 3 Totals**         |                                                                            | **10** | **30**      | **60**       | **100**   |

### MVP Phase 4: AI & Personalization (Total: 342 hours)
| Feature / Task                  | Description                                                                 | PM (h) | Backend (h) | Frontend (h) | UI/UX (h) | Total (h) |
| :------------------------------ | :-------------------------------------------------------------------------- | :----- | :---------- | :----------- | :-------- | :-------- |
| Secure Health Backend           | DB schema with RLS for health data, secure APIs.                           | 0      | 72          | 0            | 0         | 72        |
| AI Assistant Integration        | Integrate with a third-party LLM for generating suggestions.               | 0      | 60          | 0            | 0         | 60        |
| Health Onboarding & Chat UI     | Build Flutter screens for health profile creation and the AI chat interface.| 0      | 0           | 120          | 0         | 120       |
| UI/UX Design for AI Features    | Design the health profile and AI chat experience.                          | 0      | 0           | 0            | 50        | 50        |
| Project Management & Compliance | Sprints planning, GDPR compliance oversight, DPIA.                        | 40     | 0           | 0            | 0         | 40        |
| **MVP Phase 4 Totals**          |                                                                            | **40** | **132**     | **120**      | **50**    | **342**   |

---

## 5. Team Composition & Resource Allocation

| Role                   | Total Estimated Hours |
| :--------------------- | :-------------------- |
| Project Manager        | 176                   |
| Backend Developer(s)   | 652                   |
| Frontend Developer(s)  | 552                   |
| UI/UX Designer         | 90                    |
| **Grand Total**        | **1,520**             |

*(Note: Hours for Retool development are allocated to Frontend.)*

---

## 6. Budget Estimation

* **Total Estimated Hours:** 1,520 hours
* **Blended Hourly Rate:** €100.00
* **Total Estimated Project Cost:** **€152,000**

| Phase   | MVP Phase                        | Estimated Hours | Estimated Cost |
| :------ | :--------------------------------| :-------------- | :------------- |
| MVP-0   | MVP Phase 0: Prototyping         | 178             | €17,800        |
| MVP-1   | MVP Phase 1: Flutter App         | 300             | €30,000        |
| MVP-2   | MVP Phase 2: Backend Replacement | 600             | €60,000        |
| MVP-3   | MVP Phase 3: Dashboard Replacement | 100             | €10,000        |
| MVP-4   | MVP Phase 4: AI Integration      | 342             | €34,200        |
| **Total** |                                 | **1,520**       | **€152,000**   |

---

## 7. Key Decisions & Justifications

* **Phased Replacement Strategy:** This approach de-risks the project significantly. By first building the Flutter app against the existing backend (MVP-1), we can make immediate progress on the user-facing product without being blocked by a full backend rebuild. This allows for earlier user testing and feedback, while the complex backend replacement (MVP-2) happens in a subsequent, dedicated phase.
* **Proprietary Data Backend (MVP-2):** While connecting to the existing backend is a good first step, owning our data pipeline is critical for long-term success. Research shows that building a custom, hybrid solution provides the most flexibility and avoids vendor lock-in, making MVP-2 a strategic necessity.
* **Retool for Admin Panel (MVP-3):** Using a low-code platform like Retool for the internal dashboard allows for extremely rapid development and iteration, freeing up core engineering resources to focus on the consumer-facing product and complex backend services.

---

## 8. Risks & Mitigations

* **Risk:** The existing backend API is poorly documented or unstable, delaying MVP-1.
  * **Mitigation:** Allocate specific time for API discovery in MVP-1. Build an anti-corruption layer in the Flutter app to isolate it from the legacy API, easing the transition to Supabase in MVP-2.
* **Risk:** Web scraping proves more difficult or legally challenging than anticipated.
  * **Mitigation:** The scraping service in MVP-2 will be built modularly, prioritizing mobile APIs and using web scraping as a fallback, as recommended by research.
* **Risk:** GDPR compliance for health data (MVP-4) is complex and requires specialized legal knowledge.
  * **Mitigation:** Allocate specific hours for compliance work and legal review. Design the architecture with privacy-by-design principles, including EU-only data residency and encryption from the start.

---

## 9. Next Steps

1. **Formal Approval:** Seek stakeholder approval for this revised 5-phase proposal, timeline, and budget.
2. **Initiate MVP Phase 0:** Begin UI/UX design and prototype development immediately.
3. **Team Allocation:** Formally allocate the project team resources as outlined in this proposal.
4. **Kick-off Meeting:** Schedule a project kick-off to align the team on the goals and timeline for MVP-0.