# ⚙️ Requirements: SuperMarty Frontend (MVP)

# 🧩 Actors & Components (Who or what)
*   **End User:** The primary user of the application.
*   **Admin:** The user managing the system via the Admin Panel.
*   **Application Shell (PWA/Capacitor):** The main container for the user-facing app, primarily in Dutch.
*   **Admin Panel:** A "low-code" web interface for administrators.
*   **UI Components**
    *   `[Button]`
    *   `[Input Field]`
    *   `[Search Bar]`
    *   `[Product Card]` (with vertical thumbnail)
    *   `[Recipe Card]`
    *   `[Shopping Bag Card]`
    *   `[List / Grid View]`
    *   `[Tabs]`
    *   `[Navigation Bar]`
    *   `[Modal / Dialog]`
*   **Screens / Pages**
    *   `[Login Screen]`
    *   `[Sign Up / Onboarding Flow]`
    *   `[Discover Screen]`
    *   `[Search Results Screen]`
    *   `[System Product Detail Screen]`
    *   `[Single Market Product Detail Screen]`
    *   `[Recipe Detail Screen]`
    *   `[Bag Detail Screen]`
    *   `[Category Detail Screen]`
    *   `[Shopping List Screen]`
    *   `[Favorites Screen]`
    *   `[User Profile Screen]` (Could Have)

---
# 🎬 Activities (Who or what does what?)
*   **End User**
    *   [Sign up for a new account using email and password]
    *   [Log in and out of the application]
    *   [Reset password via email]
    *   [Complete the onboarding flow to set preferences (e.g., intolerances)]
    *   [Browse and discover products, recipes, and bags on the Discover page]
    *   [Search for specific items]
    *   [Filter content by categories, labels, and supermarket]
    *   [View detailed information for a system product, meal, or bag]
    *   [View detailed information for a single market's version of a product]
    *   [Add/remove items to/from the shopping list]
    *   [Add/remove items to/from a personal Favorites list]
    *   [Create and save custom shopping bags]
    *   [Share a custom bag with others]
    *   [View the shopping list with aggregated prices per supermarket]
    *   [Select a supermarket and proceed to checkout (redirect)]
    *   [Delete their account and associated data]
*   **Admin**
    *   [Log in to the Admin Panel]
    *   [Perform CRUD operations on products, categories, labels, recipes, and bags]
    *   [Create/edit labels directly from the product/meal/bag creation forms]
    *   [View categories based on their parent/child hierarchy]
    *   [Define the display order for categories]
    *   [Search and filter lists of content]

---
## 🌊 Activity Flows & Scenarios (What in which order?)
*   **[Checkout Flow]**
    *   **Happy Flow:**
        *   GIVEN the user is on the Shopping List screen with items in their list
        *   WHEN the user selects a supermarket (e.g., "Albert Heijn")
        *   AND clicks the "Checkout" button
        *   THEN the system displays a notification: "You will be redirected to Albert Heijn. You may need an account there to complete your purchase."
        *   AND the user is redirected to the Albert Heijn web store with the shopping list items (best effort, e.g., via a shared list URL).
    *   **Scenario (Item Unavailable):**
        *   GIVEN the user's shopping list contains an item not available at the selected supermarket
        *   WHEN the user views the total price for that supermarket
        *   THEN a warning is displayed next to the total, indicating that not all items are available.
    *   **Mermaid Diagram:**
        ```mermaid
        graph TD
            A[View Shopping List] --> B{Select Supermarket};
            B --> C[Click Checkout];
            C --> D[Show Redirect Notification];
            D --> E[Redirect to Supermarket Website];
        ```

---
# 📝 Properties (Which values?)
*   **Product Card**
    *   `product_name : string`
    *   `thumbnail_url : string`
    *   `best_price : decimal`
    *   `nutri_score : char` (A-E)
*   **Shopping List**
    *   `items : array[SystemProduct]`
    *   `total_price_per_supermarket : map[string, decimal]`
    *   `selected_supermarket : string`
*   **Single Market Product Page**
    *   `product_name : string`
    *   `market_specific_name : string`
    *   `image_url : string`
    *   `price : decimal`
    *   `nutritional_info : JSONB`
    *   `market_url : string`

---
# 🛠️ Behaviours (How does it act when.. in terms of.. ?)
*   **Localization**
    *   [The application's primary language must be Dutch, including all UI text, labels, and notifications.]
*   **Discovery**
    *   [If the user has not set any preferences, the Discover page should show bags and meals randomly.]
    *   [If preferences are set, the Discover page should prioritize content matching those preferences (e.g., diet, intolerances) and tags.]
*   **Checkout**
    *   [Before redirecting to a supermarket website, a clear notification must inform the user that they are leaving the app and may need an account on the destination site.]
*   **Admin Panel**
    *   [The interface should be optimized for data entry, with efficient forms and tables.]
    *   [All destructive actions (e.g., delete) must require a confirmation dialog.]

---
# 💡 Ideas & 🪵 Backlog
*   [AI Food Assistant for personalized recipe and product suggestions.]
*   [Gamification: Add elements like badges or points to encourage engagement.]
*   [Social Sharing: Allow users to share their favorite meals on social media.]
*   [Advanced Filtering: Allow users to set min/max price ranges or filter by more complex nutritional data.]
*   [User-Created Content: Allow users to create and share their own public meals.]
*   [User Roles: Implement a hierarchy for end-users (e.g., trainer, normal user).]
*   [Location Services: Filter supermarkets based on user's current location.]
*   [Ratings: Allow users to like, dislike, or rate bags and meals.]

---
# ❓ Questions
*   Are there complete UI/UX designs (e.g., Figma files) available for all MVP screens, including the Dutch translations?
*   What is the desired behavior for the app when the user is offline? What data should be accessible (e.g., last viewed shopping list)?
*   For the checkout redirection, what is the specific mechanism for each supermarket (e.g., shared link, query parameters)? What is the fallback if a direct transfer fails?
*   What are the exact fields to be included in the user onboarding/preference selection?

---
# 🎯 Roles, 📝 Tasks & 🎓 Suggested Approach
*   **🎨 UI/UX Designer**
    *   [Branding & Design System]
        *   [ ] Finalize the design system, ensuring components support Dutch language text.
    *   [Wireframes & Mockups]
        *   [ ] Design high-fidelity mockups for all MVP screens, including the Single Market Product page and Favorites page.
        *   [ ] Provide all UI text in Dutch for implementation.
        *   [ ] Design states for loading, empty, and error scenarios.
*   **🖥️ Frontend Developer**
    *   [Project Setup]
        *   [ ] Set up the PWA project using Capacitor and a modern web framework.
        *   [ ] Implement internationalization (i18n) with Dutch as the default language.
    *   [Screen Implementation]
        *   [ ] Implement the Admin Panel screens and connect them to the API.
        *   [ ] Implement the user authentication and onboarding flow.
        *   [ ] Implement all user-facing screens (Discover, Details, Shopping List, Favorites, etc.).
        *   [ ] Implement the checkout redirection flow for AH, Jumbo, and Plus.
        *   [ ] Implement "add to favorites" and "create custom bag" functionality.
*   **📌 Project Manager**
    *   [Coordination]
        *   [ ] Gather final design assets and Dutch translations.
        *   [ ] Facilitate communication between frontend and backend teams regarding API contracts.
        *   [ ] Plan and coordinate User Acceptance Testing (UAT) for the application.