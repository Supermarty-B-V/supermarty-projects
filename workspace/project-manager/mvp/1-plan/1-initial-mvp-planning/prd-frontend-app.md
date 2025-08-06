# ⚙️ Requirements: Frontend Application (Flutter)

---
# 🧩 Actors & Components (Who or what)
*   **End User:** The primary user of the application.
*   **Web Prototype (MVP 0):** A high-fidelity, interactive web application built with a tool like v0.dev, using mock data.
*   **Application (Flutter):** The main cross-platform application for Web, iOS, and Android.
*   **Screens**
    *   `[Authentication Screen]` (Login / Sign Up)
    *   `[Product Catalog Screen]` (Browse & Search)
    *   `[Product Detail Screen]`
    *   `[Shopping Bag Screen]`
    *   `[Price Comparison Screen]`
    *   `[Meal Plan Screen]` (MVP 2)
    *   `[Recipe Detail Screen]` (MVP 2)
    *   `[Health Profile Onboarding Screen]` (MVP 3)
    *   `[AI Assistant Chat Screen]` (MVP 3)
*   **UI Components**
    *   `[Product Card]`
    *   `[Meal Plan Card]` (MVP 2)
    *   `[Recipe Card]` (MVP 2)
    *   `[Search Bar]`
    *   `[Supermarket Selector]`
    *   `[Price Comparison Table]`
    *   `[Checkout Button]`
    *   `[Chat Input Field]` (MVP 3)
    *   `[Chat Message Bubble]` (MVP 3)
*   **Backend API (Supabase):** The external system providing all data.
*   **Mock Data Source (MVP 0):** A set of static JSON files simulating the backend API.

---
# 🎬 Activities (Who or what does what?)
*   **End User**
    *   [Interact with the web prototype to click through the entire user journey] (MVP 0)
    *   [Provide feedback on the prototype's UI/UX] (MVP 0)
    *   [Sign up for a new account using email and password]
    *   [Log in to an existing account]
    *   [Search for products by name]
    *   [Browse products by category]
    *   [View detailed information about a product]
    *   [Add a product to the shopping bag]
    *   [Remove a product from the shopping bag]
    *   [Adjust the quantity of a product in the shopping bag]
    *   [View the shopping bag with all items]
    *   [Navigate to the price comparison screen]
    *   [View a comparison of the total bag price across different supermarkets]
    *   [Initiate checkout, which redirects to the selected supermarket's website]
    *   [Browse curated meal plans] (MVP 2)
    *   [View the details of a recipe, including ingredients and instructions] (MVP 2)
    *   [Add all ingredients from a recipe to the shopping bag with one click] (MVP 2)
    *   [Complete the health profile onboarding flow] (MVP 3)
    *   [Provide explicit consent for health data processing] (MVP 3)
    *   [Open the AI Assistant chat interface] (MVP 3)
    *   [Send natural language requests to the AI assistant] (MVP 3)
    *   [Receive personalized meal or product suggestions from the AI] (MVP 3)

---
## 🌊 Activity Flows & Scenarios (What in which order?)
*   **[Prototype Validation (MVP 0)]**
    *   **Happy Flow:**
        *   GIVEN a stakeholder receives a URL to the web prototype
        *   WHEN they open the URL
        *   THEN they can click through all screens of the application, from login to checkout
        *   AND all interactive elements respond, powered by mock data.
*   **[Full Shopping Journey (MVP 1)]**
    *   **Happy Flow:**
        *   GIVEN a logged-in user is on the `Product Catalog Screen`
        *   WHEN the user searches for "Milk" and adds "Organic Milk 1L" to their bag
        *   AND navigates to the `Price Comparison Screen`
        *   THEN the screen displays the total price for the bag at Albert Heijn and Jumbo
        *   WHEN the user selects "Albert Heijn" and taps "Checkout"
        *   THEN the app opens a browser and redirects the user to the Albert Heijn website.
*   **[Meal Plan to Shopping Bag (MVP 2)]**
    *   **Happy Flow:**
        *   GIVEN a user is on the `Meal Plan Screen`
        *   WHEN the user taps on a "Weekly Keto Plan"
        *   AND on the `Recipe Detail Screen` for a specific recipe, taps "Add All Ingredients to Bag"
        *   THEN all required products for that recipe are added to the `Shopping Bag`.
*   **[AI-Driven Shopping (MVP 3)]**
    *   **Happy Flow:**
        *   GIVEN a user has completed their health profile
        *   WHEN the user opens the `AI Assistant Chat Screen` and types "Suggest a healthy, low-budget meal for tonight"
        *   THEN the AI responds with a recipe suggestion card
        *   WHEN the user taps "Add to Bag" on the suggestion card
        *   THEN the recipe's ingredients are added to the `Shopping Bag`.
    *   **Mermaid Diagram (Combined Flow):**
        ```mermaid
        graph TD
            subgraph MVP 0
                P[Web Prototype] -->|Click-through| Q[Gather Feedback];
            end
            subgraph MVP 1
                A[Catalog] -->|Add Product| B[Shopping Bag];
                B --> C[Price Comparison];
                C --> D[Redirect to Supermarket];
            end
            subgraph MVP 2
                E[Meal Plans] -->|Select Recipe| F[Recipe Details];
                F -->|Add Ingredients| B;
            end
            subgraph MVP 3
                G[AI Assistant] -->|Get Suggestion| H[AI Recipe Card];
                H -->|Add to Bag| B;
            end
        ```

---
# 📝 Properties (Which values?)
*   **ProductCard Component**
    *   `product_name : string`
    *   `image_url : string`
    *   `best_price : float`
*   **ShoppingBag State**
    *   `items : List<ShoppingBagItem>`
*   **Recipe** (MVP 2)
    *   `name : string`
    *   `instructions : string`
    *   `ingredients : List<{product_id, quantity}>`
*   **HealthProfile** (MVP 3)
    *   `goals : List<string>`
    *   `intolerances : List<string>`
    *   `weight_kg : float`
    *   `height_cm : float`

---
# 🛠️ Behaviours (How does it act when.. in terms of.. ?)
*   **Performance**
    *   [The app must maintain a smooth 60fps scroll performance on all list screens.]
    *   [Product search results should appear in under 500ms.]
*   **State Management**
    *   [The shopping bag state must persist across app sessions.]
*   **Responsiveness**
    *   [All screens must adapt gracefully to different screen sizes, from mobile phones to web desktops.]
*   **Offline Support**
    *   [The app should cache product catalog and recipe data to allow for browsing when offline.]
*   **GDPR Compliance (MVP 3)**
    *   [The app must obtain explicit, granular consent before allowing a user to enter any health data.]
    *   [It must be as easy for a user to withdraw consent as it was to give it.]

---
# 💡 Ideas & 🪵 Backlog
*   [Implement a "Favorites" feature for users to save products and recipes.]
*   [Add a dark mode theme.]
*   [Allow users to share meal plans and shopping lists with others.]

---
# ❓ Questions
*   What should happen if the affiliate link for a checkout redirection is broken? (Assumption: We will show an error message and redirect to the supermarket's homepage as a fallback).
*   Are there specific UI designs or a design system to follow for all MVP phases? (Assumption: A basic, clean UI will be created and evolved).

---
# 🎯 Roles, 📝 Tasks & 🎓 Suggested Approach
*   **🎨 UI/UX Designer**
    *   [MVP 0]
        *   [ ] Provide high-fidelity designs for all user-facing screens to guide the prototype development.
    *   [ ] Create wireframes and high-fidelity mockups for all screens across MVP1, MVP2, and MVP3.
    *   [ ] Design the consent flow for health data collection (MVP 3).
    *   [ ] Define a comprehensive design system.
*   **🖥️ Frontend Developer**
    *   [MVP 0]
        *   [ ] Build a complete, interactive web prototype using a tool like v0.dev, powered by mock JSON data.
        *   [ ] Deploy the prototype to a public URL for feedback.
    *   [MVP 1]
        *   [ ] Implement the core shopping journey: Auth, Catalog, Bag, Price Comparison, Checkout.
    *   [MVP 2]
        *   [ ] Build screens for browsing Meal Plans and Recipes.
        *   [ ] Implement "Add all ingredients to bag" logic.
    *   [MVP 3]
        *   [ ] Build the Health Profile onboarding and management screens.
        *   [ ] Implement the AI Assistant chat interface.
        *   [ ] Ensure all GDPR consent mechanisms are implemented correctly on the frontend.
*   **📌 Project Manager**
    *   [ ] Break down features for all three MVPs into user stories.
    *   [ ] Coordinate with the backend team on API contracts for all phases.