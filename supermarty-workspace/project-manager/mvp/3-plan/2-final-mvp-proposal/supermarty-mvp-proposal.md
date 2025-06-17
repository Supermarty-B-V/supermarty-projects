# SuperMarty: Full MVP Proposal & Roadmap

**Document Version:** 3.0
**Date:** 2025-06-17
**Author:** Proposal Expert (AI Assistant)

---

## 1. Executive Summary

### 1.1. Vision
To become the leading intelligent grocery shopping assistant in the EU, helping users save money, eat healthier, and simplify their meal planning through a seamless, AI-driven experience.

### 1.2. Proposal Overview
This document outlines a comprehensive, 5-month phased development plan and budget to bring the SuperMarty vision to market. The plan is broken down into four distinct epics, beginning with a rapid prototyping phase (MVP 0) to validate the user experience, followed by three subsequent MVP releases that incrementally deliver core functionality.

Based on extensive research, we recommend a strategic **"build" approach** for our core data acquisition and product matching systems. While this requires a greater upfront investment, it will create a powerful, proprietary data asset that serves as a long-term competitive advantage.

This proposal provides a detailed breakdown of features, required resources, timeline, and estimated costs to deliver the full MVP scope, totaling **1,520 hours** at an estimated cost of **€152,000**.

---

## 2. Strategic Approach & Recommendations

### 2.1. Phased MVP Rollout
To manage risk and deliver value quickly, the project will be executed in four distinct epics:

*   **Epic 0: Project Setup & Prototyping (1 Month):** Build a high-fidelity, interactive web prototype using mock data to validate the complete user flow and finalize UI/UX designs before committing to full-stack development.
*   **Epic 1: Core Platform & Shopping Experience (2 Months):** Launch a functional cross-platform app allowing users to build a shopping bag and compare prices across Albert Heijn, Jumbo, and Plus. This includes building the core data acquisition and product matching services.
*   **Epic 2: Content & Engagement Features (1 Month):** Increase user engagement by introducing a library of curated meal plans and recipes that can be added to the shopping bag with one click.
*   **Epic 3: Personalization & AI (1 Month):** Deliver deep personalization by launching the "Super Marty" AI assistant, which provides tailored dietary suggestions based on user health profiles, while ensuring full GDPR compliance.

### 2.2. Technology Stack
*   **Frontend:** **Flutter** for a single codebase across Web, iOS, and Android.
*   **Backend:** **Supabase** for its integrated database, authentication, and serverless functions.
*   **Admin Panel:** **Retool** for rapid development of internal data management dashboards.
*   **Data Acquisition:** A custom **Python** service using a modular adapter for **Firecrawl**, with a fallback to a custom Scrapy/Playwright framework.
*   **AI & Matching:** Python services using **Sentence-BERT** for NLP matching and integrating with a third-party LLM for the AI assistant.

---

## 3. Project Epics & High-Level Roadmap

**Total Timeline:** 5 Months (June 17, 2025 - November 17, 2025)

| Phase     | Epic                                         | Sprints | Dates                 | Key Goals & Deliverables                                                                               |
| :-------- | :------------------------------------------- | :------ | :-------------------- | :------------------------------------------------------------------------------------------------------ |
| **Phase 0** | **Epic 0:** Project Setup & Prototyping      | 1-2     | Jun 17 - Jul 14       | Validate UI/UX with a high-fidelity, clickable web prototype using mock data. Finalize design direction. |
| **Phase 1** | **Epic 1:** Core Platform & Shopping         | 3-6     | Jul 15 - Sep 8        | Build and launch the core price comparison engine, data backend, and user-facing Flutter app for MVP 1. |
| **Phase 2** | **Epic 2:** Content & Engagement             | 7-8     | Sep 9 - Oct 6         | Enhance user value by adding browsable meal plans and recipes that integrate with the shopping bag.      |
| **Phase 3** | **Epic 3:** Personalization & AI             | 9-10    | Oct 7 - Nov 3         | Implement health profiles and the "Super Marty" AI assistant. Ensure full GDPR compliance.               |

---

## 4. Detailed Feature Breakdown & Estimations

### Epic 0: Project Setup & Prototyping (Total: 178 hours)
| Feature / Task               | Description                                                                 | PM (h) | Backend (h) | Frontend (h) | UI/UX (h) | Total (h) |
| :--------------------------- | :-------------------------------------------------------------------------- | :----- | :---------- | :----------- | :-------- | :-------- |
| Project & Team Onboarding    | Setup repositories, PM tools, communication channels.                       | 10     | 4           | 4            | 0         | 18        |
| Define Mock API Contract     | Specify the JSON structure for all data models to be used by the prototype. | 0      | 16          | 8            | 0         | 24        |
| UI/UX Design for Prototype    | Create high-fidelity mockups for all screens in the user journey.            | 0      | 0           | 0            | 40        | 40        |
| Build Interactive Prototype  | Develop a clickable web prototype using v0.dev or similar, powered by mock JSON. | 0      | 0           | 80           | 0         | 80        |
| Stakeholder Review & Feedback | Conduct review sessions and consolidate feedback to inform MVP 1.           | 16     | 0           | 0            | 0         | 16        |
| **Epic 0 Totals**            |                                                                             | **26** | **20**      | **92**       | **40**    | **178**   |

### Epic 1: Core Platform & Shopping Experience (Total: 760 hours)
| Feature / Task                     | Description                                                                 | PM (h) | Backend (h) | Frontend (h) | UI/UX (h) | Total (h) |
| :--------------------------------- | :-------------------------------------------------------------------------- | :----- | :---------- | :----------- | :-------- | :-------- |
| Backend Setup                      | Provision Supabase, define DB schema for MVP 1, configure Auth.             | 0      | 40          | 0            | 0         | 40        |
| Scraping Service v1                | Build modular service with Firecrawl adapter for AH, Jumbo, Plus.          | 0      | 80          | 0            | 0         | 80        |
| Product Matching Service v1        | Implement EAN-based matching and a baseline NLP model.                     | 0      | 80          | 0            | 0         | 80        |
| Core Backend APIs                  | Develop APIs for users, products, and shopping bags.                       | 0      | 120         | 0            | 0         | 120       |
| Admin Panel v1 (Retool)            | Setup Retool dashboards for product and match review.                      | 0      | 56          | 0            | 0         | 56        |
| Frontend Setup (Flutter)           | Initialize cross-platform project, connect to Supabase.                    | 0      | 0           | 40           | 0         | 40        |
| Frontend Auth Flow                 | Implement screens and logic for Sign Up and Login.                         | 0      | 0           | 40           | 0         | 40        |
| Product Catalog & Search           | Build screens for browsing categories and searching for products.          | 0      | 0           | 80           | 0         | 80        |
| Shopping Bag & Price Comparison    | Implement bag state management and the price comparison UI.               | 0      | 0           | 80           | 0         | 80        |
| Checkout v1 (Redirect)             | Implement affiliate deep linking for checkout redirection.                | 0      | 0           | 40           | 0         | 40        |
| UI/UX Design for MVP 1             | Finalize designs for all MVP 1 features.                                   | 0      | 0           | 0            | 40        | 40        |
| Project Management                 | Sprints planning, coordination, reviews.                                   | 64     | 0           | 0            | 0         | 64        |
| **Epic 1 Totals**                  |                                                                             | **64** | **376**     | **280**      | **40**    | **760**   |

### Epic 2: Content & Engagement Features (Total: 228 hours)
| Feature / Task                | Description                                                                | PM (h) | Backend (h) | Frontend (h) | UI/UX (h) | Total (h) |
| :---------------------------- | :------------------------------------------------------------------------- | :----- | :---------- | :----------- | :-------- | :-------- |
| Backend for Meals/Recipes     | Extend DB schema and build CRUD APIs for content.                         | 0      | 64          | 0            | 0         | 64        |
| Admin Panel v2 (Retool)       | Add dashboards for managing meal plans and recipes.                       | 0      | 32          | 0            | 0         | 32        |
| Frontend Content Screens      | Build UI for browsing and viewing meal plans and recipes.                | 0      | 0           | 60           | 0         | 60        |
| "Add to Bag" from Recipe      | Implement logic to add all recipe ingredients to the shopping bag.         | 0      | 0           | 20           | 0         | 20        |
| UI/UX Design for MVP 2        | Design all content-related screens and user flows.                       | 0      | 0           | 0            | 20        | 20        |
| Project Management            | Sprints planning, coordination, reviews.                                 | 32     | 0           | 0            | 0         | 32        |
| **Epic 2 Totals**             |                                                                            | **32** | **96**      | **80**       | **20**    | **228**   |

### Epic 3: Personalization & AI (Total: 354 hours)
| Feature / Task                  | Description                                                                 | PM (h) | Backend (h) | Frontend (h) | UI/UX (h) | Total (h) |
| :------------------------------ | :-------------------------------------------------------------------------- | :----- | :---------- | :----------- | :-------- | :-------- |
| Secure Health Backend           | DB schema with RLS for health data, secure APIs.                           | 0      | 72          | 0            | 0         | 72        |
| AI Assistant Integration        | Integrate with a third-party LLM for generating suggestions.               | 0      | 60          | 0            | 0         | 60        |
| Admin Panel v3 (Retool)         | Build restricted dashboards for support and AI analytics.                  | 0      | 40          | 0            | 0         | 40        |
| Health Onboarding Frontend      | Build screens for health profile creation and GDPR consent.               | 0      | 0           | 60           | 0         | 60        |
| AI Assistant Chat UI            | Implement the chat interface in the Flutter app.                          | 0      | 0           | 60           | 0         | 60        |
| UI/UX Design for MVP 3          | Design the health profile and AI chat experience.                          | 0      | 0           | 0            | 30        | 30        |
| Project Management              | Sprints planning, GDPR compliance oversight.                               | 32     | 0           | 0            | 0         | 32        |
| **Epic 3 Totals**               |                                                                            | **32** | **172**     | **120**      | **30**    | **354**   |

---

## 5. Team Composition & Resource Allocation

The successful delivery of this project requires a dedicated team with the following roles and estimated effort over the 5-month timeline.

| Role                 | Total Estimated Hours |
| :------------------- | :-------------------- |
| Project Manager      | 154                   |
| Backend Developer(s) | 664                   |
| Frontend Developer(s)| 572                   |
| UI/UX Designer       | 130                   |
| **Grand Total**      | **1,520**             |

---

## 6. Budget Estimation

The total estimated budget is based on the total project hours and a blended hourly rate, which is standard for a project team with this mix of roles and expertise.

*   **Total Estimated Hours:** 1,520 hours
*   **Assumed Blended Hourly Rate:** €100.00
*   **Total Estimated Project Cost:** **€152,000**

| Phase  | Epic                             | Estimated Hours | Estimated Cost |
| :----- | :--------------------------------| :-------------- | :------------- |
| Phase 0 | Epic 0: Prototyping              | 178             | €17,800        |
| Phase 1 | Epic 1: Core Platform            | 760             | €76,000        |
| Phase 2 | Epic 2: Content                  | 228             | €22,800        |
| Phase 3 | Epic 3: Personalization & AI     | 354             | €35,400        |
| **Total** |                                 | **1,520**       | **€152,000**   |

---

## 7. Key Architectural Decisions

*   **Data Acquisition:** We will build a proprietary, hybrid data acquisition service. This provides long-term flexibility and avoids vendor lock-in. The service will prioritize stable mobile APIs and use a robust web scraping framework (Scrapy/Playwright) as a fallback.
*   **Product Matching:** A multi-modal matching pipeline is essential for accuracy. EANs provide a high-precision first pass. A fine-tuned Sentence-BERT model will handle the semantic complexities of product titles. Image similarity will act as a final verifier.
*   **Backend Infrastructure:** Supabase provides a powerful, scalable foundation. This will be augmented by custom Python services for data-intensive tasks like scraping and matching, deployed in a containerized environment.
*   **Checkout Integration:** The initial reliance on affiliate deep links is a low-risk, legitimate entry point that establishes a formal relationship with each supermarket, providing a foundation for negotiating deeper integrations.

---

## 8. Legal, Compliance & Risk Management

*   **GDPR Compliance (MVP 3):** This is the highest compliance risk. All user-provided health information will be treated as **"special category data"** under GDPR Article 9. The only viable legal basis is **"explicit consent,"** which will be implemented via a granular, unbundled consent flow. A mandatory **Data Protection Impact Assessment (DPIA)** will be completed before the launch of MVP 3.
*   **Scraping Legality:** We acknowledge that web scraping may violate supermarket Terms of Service. We will mitigate this risk by prioritizing mobile APIs and adhering to ethical scraping best practices (e.g., identifying our bot, respecting `robots.txt`).
*   **Technical Risks:**
    * **API Changes:** Supermarkets may change their private APIs without notice. **Mitigation:** A robust monitoring and alerting system, and the web scraping fallback system.
    * **Model Drift:** The accuracy of the matching model may degrade over time. **Mitigation:** The HITL feedback loop and regular model retraining.

---

## 9. Next Steps

1.  **Formal Approval:** Seek stakeholder approval for this proposal, timeline, and budget.
2.  **Initiate Epic 0:** Begin development of the high-fidelity web prototype immediately.
3.  **Establish Partnerships:** Begin the application process for the affiliate programs with Partnerize (Albert Heijn), Tradetracker (Jumbo), and Awin (PLUS).
4.  **Begin Compliance Work:** Start the formal Data Protection Impact Assessment (DPIA) process for the MVP 3 features.
5.  **Resource Allocation:** Formally allocate the project team resources as outlined in this proposal.