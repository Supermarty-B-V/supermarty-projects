# ⚙️ Requirements: Backend Services (Supabase & Python)

---
# 🧩 Actors & Components (Who or what)
*   **System:** The overall backend infrastructure.
*   **Supabase:** The core BaaS platform.
    *   **PostgreSQL Database:** The primary data store.
    *   **Supabase Auth:** Manages user and admin authentication.
    *   **Edge Functions:** Serverless functions for API logic.
*   **Scraping Service:** A modular service responsible for data aggregation.
    *   **Scraping Adapter:** An internal interface that abstracts the scraping logic.
    *   **Firecrawl Client:** The initial implementation of the adapter, which calls the Firecrawl API.
*   **Product Matching Service:** AI/ML service for linking products.
    *   **EAN Matcher:** Tier 1 matcher.
    *   **NLP Matcher (SBERT):** Tier 2 matcher.
*   **AI Assistant Service (MVP 3):** Service that integrates with a third-party AI (e.g., OpenAI) to generate recommendations.
*   **Cache Layer (Redis):** Caches scraper responses and API queries.
*   **Admin Panel (Retool):** External actor for admin tasks.
*   **Frontend App (Flutter):** External actor consuming the API.

---
# 🎬 Activities (Who or what does what?)
*   **Scraping Service**
    *   [Fetch product data on-demand from supermarket sources]
    *   [Normalize and cache scraped data]
*   **Product Matching Service**
    *   [Receive a new product and link it to a shadow product or flag for review]
*   **Supabase (API & DB)**
    *   [Provide endpoints for User and Admin authentication]
    *   [Provide CRUD endpoints for Shadow Products, Market Products, Categories, and Labels]
    *   [Provide CRUD endpoints for Meal Plans and Recipes] (MVP 2)
    *   [Provide secure endpoints to create, read, and update a User's Health Profile] (MVP 3)
    *   [Provide an endpoint for the AI Assistant to query user/product data] (MVP 3)
    *   [Store all application data, including sensitive health data, securely in PostgreSQL]

---
## 🌊 Activity Flows & Scenarios (What in which order?)
*   **[On-Demand Product Data Fetch & Match (MVP 1)]**
    *   **Happy Flow:**
        *   GIVEN a user requests a product not in the cache
        *   WHEN the API receives the request
        *   THEN it calls the modular `Scraping Service` (which uses Firecrawl) to fetch the product data
        *   AND the matching service links the new product via its EAN
        *   THEN the updated data is stored and returned to the user.
*   **[AI-Powered Meal Suggestion (MVP 3)]**
    *   **Happy Flow:**
        *   GIVEN a user sends a message "Suggest a low-carb meal" to the AI Assistant endpoint
        *   WHEN the backend receives the request
        *   THEN it securely retrieves the user's health profile (e.g., intolerances)
        *   AND passes the user's request and profile data to the AI Assistant Service
        *   AND the AI service queries the product/recipe database for suitable options
        *   AND generates a recipe suggestion
        *   THEN the suggestion is returned to the user via the API.
    *   **Mermaid Diagram:**
        ```mermaid
        graph TD
            A[User Request via Flutter App] --> B[Supabase Edge Function];
            B --> C{Retrieve User Health Profile};
            C --> D[Pass Request + Profile to AI Service];
            D --> E{AI Service Queries DB for Recipes};
            E --> F[AI Generates Suggestion];
            F --> G[Return Suggestion to User];
        ```

---
# 📝 Properties (Which values?)
*   **ShadowProduct**
    *   `id : UUID`, `name : text`, `category_id : UUID`
*   **MarketProduct**
    *   `id : UUID`, `shadow_product_id : UUID`, `supermarket : text`, `price : numeric`, `ean : text`
*   **Recipe (MVP 2)**
    *   `id : UUID` (Primary Key)
    *   `name : text`
    *   `description : text`
    *   `instructions : text`
    *   `ingredients : jsonb` (e.g., `[{"product_id": "...", "quantity": "200g"}]`)
*   **MealPlan (MVP 2)**
    *   `id : UUID` (Primary Key)
    *   `name : text`
    *   `description : text`
    *   `recipes : array[UUID]` (Foreign Keys to Recipe)
*   **UserHealthProfile (MVP 3)**
    *   `user_id : UUID` (Primary Key, Foreign Key to `auth.users`)
    *   `goals : array[text]`
    *   `intolerances : array[text]`
    *   `weight_kg : float`
    *   `height_cm : float`
    *   `activity_level : text`

---
# 🛠️ Behaviours (How does it act when.. in terms of.. ?)
*   **Security (MVP 3)**
    *   [All health data must be encrypted at rest and in transit.]
    *   [Row-Level Security (RLS) policies must be implemented in Supabase to ensure a user can only access their own health profile.]
    *   [The AI Assistant endpoint must be strictly protected and must not expose raw health data to any third-party AI without explicit, auditable consent.]
*   **Performance**
    *   [API response times for fetching cached product data should be < 200ms.]
    *   [The product matching service must process a new product in < 5 seconds.]

---
# 💡 Ideas & 🪵 Backlog
*   [Build a historical price tracking system for products.]
*   [Explore using Supabase Vector for NLP similarity searches directly in the database.]
*   [Create a system to learn from user feedback on AI suggestions.]

---
# ❓ Questions
*   What third-party AI service will be used for the assistant? (e.g., OpenAI, Google Gemini). This will determine the integration specifics.
*   What is the definitive source of truth if nutritional information differs between two matched products?

---
# 🎯 Roles, 📝 Tasks & 🎓 Suggested Approach
*   **🔧 Backend Developer**
    *   [MVP 0]
        *   [ ] Define and document the mock data API contract (JSON files) to be used by the frontend prototype.
    *   [MVP 1]
        *   [ ] Implement database schema for core product and user tables.
        *   [ ] Develop a modular scraping service that integrates with the Firecrawl API.
        *   [ ] Develop the EAN-based matching service.
        *   [ ] Build APIs for the core shopping journey.
    *   [MVP 2]
        *   [ ] Extend schema and build APIs for Meal Plans and Recipes.
    *   [MVP 3]
        *   [ ] Implement secure schema for User Health Profiles with RLS.
        *   [ ] Build the AI Assistant integration service, ensuring data privacy.
        *   [ ] Develop secure endpoints for managing health data.
*   **🚀 DevOps Engineer**
    *   [ ] Configure Supabase project, including backups and security settings.
    *   [ ] Set up hosting and deployment for the Python services.
*   **📌 Project Manager**
    *   [ ] Define detailed user stories for all backend features across all MVPs.
    *   [ ] Coordinate with the frontend team on the evolving API contract.