# 🚀 SuperMarty: Initial MVP Project Brief

**Document Version:** 1.0
**Date:** 2024-07-16
**Author:** Project Manager (AI Assistant)

---

## 1. Executive Summary

This document outlines the revised project plan and initial requirements for the SuperMarty application. We are pivoting to a new technology stack and a phased MVP approach to accelerate development and focus on core user value. The new stack will consist of a **Flutter** frontend (for Web, iOS, and Android), a **Supabase** backend, and a dedicated **Scraping Service** for product data aggregation.

The project will be delivered in four distinct MVP phases:
1.  **Frontend Prototyping:** Rapidly build a high-fidelity, interactive web prototype to validate the user experience.
2.  **Core Shopping & Price Comparison:** Allow users to build a shopping bag and compare prices across supermarkets.
3.  **Meal Plans & Recipes:** Introduce curated meal plans and recipes to enhance the user experience.
4.  **Health & AI Assistant:** Integrate personalization through user health profiles and an AI-powered assistant, "Super Marty."

This brief defines the scope, technology, and key research areas for the successful delivery of the first MVP.

---

## 2. Vision & Goals

### Vision
To become the leading intelligent grocery shopping assistant in the EU, helping users save money, eat healthier, and simplify their meal planning process through a seamless, AI-driven experience.

### Project Goals
*   **Goal 1 (MVP1):** Launch a functional cross-platform application that allows users to select products and accurately compare the total cost of their shopping bag across multiple major supermarkets.
*   **Goal 2 (Post-MVP1):** Increase user engagement by introducing meal plans and recipes that can be added to the shopping bag with a single tap.
*   **Goal 3 (Long-term):** Establish SuperMarty as a personalized health partner by leveraging user data and AI to provide tailored dietary suggestions and meal plans.
*   **Goal 4 (Technical):** Validate the core architecture (Flutter, Supabase, Scraping Service) and establish a robust, scalable foundation for future features.

---

## 3. Target Audience

*   **Primary:** Health-conscious individuals seeking to simplify meal planning and align their grocery shopping with their dietary goals (e.g., fitness enthusiasts, users with specific dietary needs).
*   **Secondary:** Budget-conscious individuals and families in the EU who want to find the cheapest prices for their weekly groceries.

---

## 4. Phased MVP Scope

Our strategy is to deliver value incrementally through four distinct phases, starting with a frontend prototype to validate the user experience before full-scale development.

### MVP 0: Frontend Prototyping (Timeline: 1 Month)
*   **Focus:** Rapidly build a high-fidelity, interactive web prototype of the complete user-facing application using a UI generation tool (e.g., v0.dev, Lovable).
*   **Goal:** Validate the end-to-end user flow, gather early stakeholder feedback, and finalize the UI/UX design before committing to backend development.
*   **Key Characteristics:**
    *   **Frontend Only:** This phase involves no backend development.
    *   **Mock Data:** The prototype will be powered entirely by static, mock JSON data that simulates the final API responses.
    *   **Web-First:** The prototype will be a web application to allow for easy sharing and feedback via a URL.

### MVP 1: Core Shopping & Price Comparison (Timeline: 2 Months, Post-MVP0)

This foundational release validates the core business model by delivering an essential price comparison tool.

*   **User-Facing App (Flutter):**
    *   **Core Journey:** Users can sign up, browse a unified product catalog, add items to a shopping bag, and see a clear price comparison across major Dutch supermarkets.
    *   **Checkout v1:** The initial checkout experience will be a simple, reliable redirection to the chosen supermarket's website via affiliate links, allowing users to complete their purchase manually.
*   **Backend & Services:**
    *   **Data Pipeline:** A robust on-demand scraping service (Python) will populate a Supabase database with product data from Albert Heijn, Jumbo, and Plus.
    *   **Product Matching v1:** An EAN-based matching algorithm will link identical products, with a manual override capability in the admin panel.
    *   **Admin Panel v1 (Retool):** An internal dashboard for the core task of reviewing and correcting product matches to ensure data accuracy.

### MVP 2: Meal Plans & Recipes (Timeline: 1 Month, Post-MVP1)

This phase focuses on increasing user engagement and retention by adding content and utility beyond simple price comparison.

*   **User-Facing App (Flutter):**
    *   **Content Discovery:** Users can browse a curated library of meal plans and individual recipes.
    *   **One-Click Shopping:** Users can add all ingredients from a recipe or an entire meal plan to their shopping bag with a single tap, seamlessly integrating content with the core shopping journey.
*   **Backend & Services:**
    *   **New Data Models:** The database will be extended to support `MealPlan` and `Recipe` entities, including ingredients and instructions.
    *   **API Expansion:** New API endpoints will be created to serve meal and recipe content to the app.
    *   **Admin Panel v2 (Retool):** The admin panel will be expanded with full CRUD functionality for managing meal plans and recipes.

### MVP 3: Health Profile & AI Assistant (Timeline: 1 Month, Post-MVP2)

This phase introduces deep personalization, transforming the app from a utility into an intelligent assistant and delivering on our primary "health-first" value proposition.

*   **User-Facing App (Flutter):**
    *   **Health Onboarding:** Users will be invited to complete a health profile, providing data on goals, intolerances, and biometrics. Data entry will be a mix of required and optional fields to respect user privacy while enabling personalization.
    *   **AI Assistant ("Super Marty"):** A chat interface will allow users to make natural language requests for meal plans and product suggestions (e.g., "Suggest a low-carb, high-protein weekly meal plan for two people").
*   **Backend & Services:**
    *   **Secure Health Data Storage:** The backend will be enhanced to securely store and process sensitive health data, in full compliance with GDPR.
    *   **AI Service Integration:** The backend will integrate with an AI service to process user requests, query the user's health profile and product database, and generate personalized recommendations.
    *   **Admin Panel v3 (Retool):** The admin panel may include a restricted-access dashboard for monitoring anonymized AI interaction metrics and user feedback to improve the service.

---

## 5. Technology Stack

*   **Prototyping (MVP 0):** UI Generation tools like **v0.dev, Lovable, or bolt.new** for rapid web prototype development.
*   **Frontend (Client):** Flutter (for Web, iOS, and Android from a single codebase).
*   **Backend-as-a-Service (BaaS):** Supabase (for database, authentication, and serverless functions).
*   **Data Aggregation:** **Firecrawl**. The scraping service will be built behind an abstraction layer to ensure it can be easily replaced with a custom solution or alternative service if costs become prohibitive.
*   **Admin Panel:** Retool (for internal CRUD operations and data management).

---

## 6. Key Research & Discovery Areas (Risks & Unknowns)

The following areas require dedicated research and technical spikes before or during MVP1 development.

1.  **Modular Scraping Service Architecture:**
    *   **Objective:** Design and implement a scraping service that uses Firecrawl as its initial engine but is architected behind a modular interface (an abstraction layer). This design must allow for a seamless switch to an alternative service or a custom-built solution in the future to mitigate cost and dependency risks.
    *   **Question:** What is the optimal design for a "Scraping Adapter" interface? How can we ensure that the core application logic remains decoupled from the specific implementation details of Firecrawl?

2.  **Product Matching Algorithm:**
    *   **Objective:** Design and validate a strategy for accurately and automatically linking equivalent products from different supermarkets to a single "shadow product" in our database.
    *   **Question:** Should this be based on EAN codes, product name similarity (NLP), image recognition, or a hybrid model? How will we handle mismatches and allow for manual admin correction?

3.  **EU Health Data Compliance (GDPR):**
    *   **Objective:** Understand all legal requirements under GDPR for collecting, storing, and processing personal health data to provide dietary suggestions.
    *   **Question:** What specific consent is required? How must the data be secured? What are the rules around automated decision-making based on health profiles? This requires legal consultation.

4.  **Supermarket Checkout Integration:**
    *   **Objective:** Investigate the technical feasibility of progressively enhancing the checkout experience for each target supermarket.
    *   **Question:** Which supermarkets offer shared cart URLs? Which have affiliate programs or APIs for deeper integration? What are the technical limitations of each?

---

## 7. Next Steps

1.  **[ ] Research & Discovery:** Initiate technical spikes for the four key areas identified above.
2.  **[ ] Legal Consultation:** Engage a legal expert to provide guidance on GDPR compliance for health data.
3.  **[ ] Detailed Requirements:** Begin drafting detailed requirements and user stories for MVP 1 features based on this brief.
4.  **[ ] Architecture Design:** Create a high-level architecture document for the Flutter/Supabase/Scraping stack.