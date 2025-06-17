# SuperMarty 5-Month Phased MVP Roadmap
**Timeline:** June 17, 2025 - November 17, 2025

This roadmap outlines the key epics and features to be delivered across four MVP phases, executed in ten 2-week sprints.

---

### **Phase 0: MVP 0 - Frontend Prototyping (Month 1)**

| Sprint | Dates | Key Goals & Deliverables |
| :--- | :--- | :--- |
| **Sprint 1** | Jun 17 - Jun 30 | **Prototype Scaffolding & Core UI.** <br/> - [ ] Setup prototyping project (v0.dev, etc.). <br/> - [ ] Define mock data structures/JSON files for products, meals, users. <br/> - [ ] Build main app shell, navigation, and screens for Auth, Product Catalog, and Shopping Bag using mock data. |
| **Sprint 2** | Jul 1 - Jul 14 | **Complete Prototype & Feedback.** <br/> - [ ] Build out all remaining screens (Price Comparison, Meal Plans, AI Chat) using mock data. <br/> - [ ] Connect all screens into a seamless, clickable user flow. <br/> - [ ] Deploy prototype to a public URL for stakeholder review. <br/> - [ ] Gather initial feedback to inform MVP1 development. |

---

### **Phase 1: MVP 1 - Core Shopping & Price Comparison (Months 2-3)**

| Sprint | Dates | Key Goals & Deliverables |
| :--- | :--- | :--- |
| **Sprint 3** | Jul 15 - Jul 28 | **Backend Foundation & Data Aggregation.** <br/> - [x] Finalize PRDs. <br/> - [ ] Setup project repositories (Flutter, Python Service Wrapper). <br/> - [ ] Provision Supabase project, define schema for MVP1, configure auth. <br/> - [ ] Integrate Firecrawl API via a modular scraping service for AH, Jumbo, and Plus. <br/> - [ ] Implement Product Matching Service v1 (EAN-first logic). |
| **Sprint 4** | Jul 29 - Aug 11 | **API & Initial Frontend.** <br/> - [ ] Develop core Supabase API endpoints for products. <br/> - [ ] Build initial Retool dashboard for viewing products and manual match queue. <br/> - [ ] Setup Flutter project for Web, iOS, and Android. <br/> - [ ] Implement User Authentication flow (Sign up, Login). <br/> - [ ] Build Product Catalog and Search screens. |
| **Sprint 5** | Aug 12 - Aug 25 | **End-to-End User Journey.** <br/> - [ ] Implement Shopping Bag state management and UI. <br/> - [ ] Implement Price Comparison screen, fetching data from the backend. <br/> - [ ] Implement checkout redirection using affiliate deep links. <br/> - [ ] Begin full end-to-end testing of the user journey. |
| **Sprint 6** | Aug 26 - Sep 8 | **MVP 1 Launch Prep.** <br/> - [ ] Enhance Retool Admin Panel with side-by-side match review interface. <br/> - [ ] Address all critical bugs from testing phase. <br/> - [ ] UI/UX polishing and performance tuning. <br/> - [ ] Prepare app store listings and web deployment. <br/> - **Goal: Launch MVP 1 by Sep 8, 2025.** |

---

### **Phase 2: MVP 2 - Meal Plans & Recipes (Month 4)**

| Sprint | Dates | Key Goals & Deliverables |
| :--- | :--- | :--- |
| **Sprint 7** | Sep 9 - Sep 22 | **Content Backend & Admin.** <br/> - [ ] Extend DB schema for Meal Plans and Recipes. <br/> - [ ] Develop backend APIs for CRUD operations on meals/recipes. <br/> - [ ] Enhance Retool Admin Panel to allow creation and management of meal plans and recipes. |
| **Sprint 8** | Sep 23 - Oct 6 | **Frontend Content Discovery.** <br/> - [ ] Build Frontend screens for browsing Meal Plans and Recipes. <br/> - [ ] Implement "Add all ingredients to bag" functionality. <br/> - [ ] Test end-to-end content discovery and shopping bag integration. <br/> - **Goal: Launch MVP 2 by Oct 6, 2025.** |

---

### **Phase 3: MVP 3 - Health Profile & AI Assistant (Month 5)**

| Sprint | Dates | Key Goals & Deliverables |
| :--- | :--- | :--- |
| **Sprint 9** | Oct 7 - Oct 20 | **Health Profile & GDPR.** <br/> - [ ] Finalize GDPR compliance strategy and DPIA. <br/> - [ ] Extend DB schema for secure storage of user health data. <br/> - [ ] Build Frontend screens for Health Profile onboarding and management. <br/> - [ ] Implement backend logic to store and retrieve health data securely. |
| **Sprint 10**| Oct 21 - Nov 3 | **AI Assistant Integration & Launch.** <br/> - [ ] Integrate with AI service for personalized recommendations. <br/> - [ ] Build AI Assistant chat interface in the Flutter app. <br/> - [ ] End-to-end testing of AI-driven suggestions. <br/> - [ ] Final polish and documentation. <br/> - **Goal: Launch MVP 3 by Nov 3, 2025.** |