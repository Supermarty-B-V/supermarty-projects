### MVP Plan: SuperMarty Grocery Assistant

**Overall Objective:** To launch a cross-platform grocery and meal planning assistant that allows users to compare prices across major Dutch supermarkets and receive personalized dietary recommendations.

---

### **Milestones**

#### Milestone 1: Build an Interactive Frontend Prototype in a 'Lovable' Style
**What to do:**
- [ ] **Design Phase:** Propose 2-3 distinct visual directions for a "lovable" style, inspired by the branding and color palette in `sm-audit-admin-panel-email.rtf`.
- [ ] **Data Contracts:** Define mock JSON data contracts for all entities as specified in the `frontend_prototype_prompt.md` (Products, Meals, Bags, Users).
- [ ] **Prototype Build:** Build a complete, clickable web prototype covering all MVP features outlined in `frontend_prototype_prompt.md` and the `sm-audit-roadmap-2024.md`:
    - User Authentication & Account Management (Sign Up, Login, Password Reset).
    - Product, Meal, and Bag Discovery & Details (including price comparisons).
    - Shopping List & Checkout Initiation (redirect flow).
    - Global Search & Filtering.
    - User Personalization (Favorites, Saved Custom Bags).
- [ ] **Localization:** Ensure all UI text is in Dutch, as specified in the requirements.
- [ ] **Deployment:** Deploy the prototype to a staging environment for stakeholder review and feedback.

**Acceptance Criteria:**
- [ ] A user can click through all core user flows defined in `frontend_prototype_prompt.md` using only mock data.
- [ ] The prototype's design successfully interprets the "lovable" aesthetic and aligns with stakeholder feedback on the proposed visual directions.
- [ ] All 'Must-Have' features from the `sm-audit-roadmap-2024.md` that are part of the frontend experience are visually represented.
- [ ] The prototype is deployed and accessible via a URL for review.

---

#### Milestone 2: Foundational Data Pipeline for a Single Supermarket
**What to do:**
- [ ] Set up the core backend infrastructure using Supabase, including the PostgreSQL database.
- [ ] Develop the initial version of the Python scraping service to fetch product data from Albert Heijn, prioritizing its mobile API as the primary data source.
- [ ] Define and implement the database schema for products, categories, and nutritional information based on the roadmap.
- [ ] Implement the logic to ingest and store the scraped data from Albert Heijn into the Supabase database.

**Acceptance Criteria:**
- [ ] Product data (name, price, EAN, nutritional info, image URL) for at least 1,000 products from Albert Heijn is successfully scraped and stored in the database.
- [ ] The scraping process can be triggered manually and completes without critical errors.
- [ ] The database schema is documented and has been reviewed by the development team.

---

#### Milestone 3: Connect Frontend to Live Backend
**What to do:**
- [ ] Refactor the Flutter application to replace mock data services with live API calls to the Supabase backend.
- [ ] Implement API calls to fetch product categories and product lists from the backend.
- [ ] Ensure the product detail page correctly displays live data for a selected product from Albert Heijn.
- [ ] Verify that all frontend components previously built in the prototype now function with real data.

**Acceptance Criteria:**
- [ ] The product catalog in the app is populated with data from the Supabase backend, not mock files.
- [ ] Users can browse categories and view products fetched from the live data pipeline.
- [ ] The product detail page shows real-time information for products from Albert Heijn.
- [ ] The application remains stable and performant when using live data.

---

#### Milestone 4: Price Comparison Engine (Core MVP)
**What to do:**
- [ ] Extend the scraping service to fetch product data from a second supermarket (Jumbo), again prioritizing its mobile API.
- [ ] Implement the v1 product matching algorithm, using EAN codes for high-confidence matches and a basic NLP model (e.g., TF-IDF or pre-trained Sentence-BERT) as a fallback.
- [ ] Set up the initial Admin Panel using Retool for manually reviewing and correcting product matches flagged by the algorithm.
- [ ] Modify the frontend product detail page to display a price comparison table showing the price for the same "shadow product" at both Albert Heijn and Jumbo.

**Acceptance Criteria:**
- [ ] Data from Jumbo is successfully scraped and stored in the database.
- [ ] At least 80% of identical products (with EANs) from AH and Jumbo are correctly matched automatically.
- [ ] An admin can log into the Retool panel, view a queue of medium-confidence matches, and approve or reject them.
- [ ] The product detail page clearly shows the prices from both supermarkets for any matched product.

---

#### Milestone 5: User Accounts & Shopping Bag
**What to do:**
- [ ] Implement user authentication (Sign Up, Login, Logout) using Supabase Auth, as detailed in the roadmap.
- [ ] Create a persistent shopping bag feature for logged-in users.
- [ ] Add UI elements to allow users to add/remove products to/from their shopping bag.
- [ ] Create a dedicated shopping bag screen that lists all added items and shows a total price, broken down by supermarket.
- [ ] Implement the MVP checkout flow: a button that redirects the user to the chosen supermarket's website (using affiliate links where possible).

**Acceptance Criteria:**
- [ ] A new user can create an account, log out, and log back in.
- [ ] A logged-in user can add a product to their shopping bag, and the item appears on the shopping bag screen.
- [ ] The shopping bag screen correctly calculates and displays the total cost for the items if purchased from Albert Heijn vs. Jumbo.
- [ ] The "Checkout at Albert Heijn" button redirects the user to `ah.nl`.
- [ ] The shopping bag's contents persist between sessions for a logged-in user.

---

#### Milestone 6: Content Expansion - Meals & Bags
**What to do:**
- [ ] Extend the backend schema and API to support "Meals" (recipes) and "Bags" (curated lists of products) as per the roadmap.
- [ ] Enhance the Admin Panel to allow admins to create and manage meals and bags by linking existing products.
- [ ] Add new sections to the Flutter app for users to discover and browse meals and bags.
- [ ] Implement an "Add all to shopping bag" button on meal and bag detail pages.

**Acceptance Criteria:**
- [ ] An admin can create a new meal with a recipe and a list of product ingredients.
- [ ] An admin can create a new bag with a curated list of products.
- [ ] A user can browse a list of available meals and bags in the app.
- [ ] A user can view the details of a meal/bag, including its full product list.
- [ ] Clicking "Add all to shopping bag" correctly adds all constituent products to the user's shopping bag.

---

#### Milestone 7: Personalization Foundation - Favorites & User Profile
**What to do:**
- [ ] Implement a "Favorites" feature, allowing users to save products, meals, and bags for later.
- [ ] Create a "Favorites" screen where users can view and manage all their saved items.
- [ ] Create a basic User Profile screen where users can view their account details (e.g., name, email).
- [ ] Implement the backend logic to store and retrieve user favorites.

**Acceptance Criteria:**
- [ ] A logged-in user can tap a "favorite" icon on a product, meal, or bag.
- [ ] The favorited item appears on the user's "Favorites" screen.
- [ ] The user can unfavorite an item from the Favorites screen, and it is removed.
- [ ] The user can navigate to a profile page showing their account information.

---

#### Milestone 8: Advanced Personalization - Health Profiles & AI Assistant
**What to do:**
- [ ] Design and implement the GDPR-compliant workflow for obtaining explicit, granular consent for health data processing.
- [ ] Extend the backend to securely store user health profiles (allergies, intolerances, dietary goals) with row-level security.
- [ ] Create the frontend UI for the health profile onboarding and management.
- [ ] Integrate with a third-party LLM to create the "Super Marty" AI assistant.
- [ ] Build the chat interface in the app.
- [ ] The AI assistant must be able to process natural language requests and suggest meals or products based on the user's health profile and the product database.

**Acceptance Criteria:**
- [ ] The app presents a clear, un-ticked consent screen before collecting any health data.
- [ ] A user can enter their dietary goals, allergies, and intolerances, and this data is saved to their profile.
- [ ] A user can ask the AI assistant "Suggest a gluten-free dinner recipe" and receive a relevant suggestion from the database.
- [ ] A user can ask "What's a good low-carb snack?" and receive a list of suitable products.
- [ ] The AI's suggestions respect the user's stated allergies and intolerances.
- [ ] A Data Protection Impact Assessment (DPIA) for this feature is completed and documented.