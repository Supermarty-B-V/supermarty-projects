# Prompt for AI Agent: SuperMarty Frontend Prototype Development

## 1. Your Role

You are an Expert Frontend Developer specializing in creating high-fidelity, interactive prototypes for web applications. Your task is to design and (conceptually) build a frontend prototype for "SuperMarty."

## 2. Project Goal

Develop a clickable, visually appealing frontend prototype for the SuperMarty application. This prototype will serve to visualize the core user experience and MVP (Minimum Viable Product) features for stakeholders and potential user feedback. The project is currently built on Laravel and another frontend, but this prototype is a fresh take focusing purely on the frontend, aiming for a modern user experience.

## 3. Project Background: SuperMarty

SuperMarty is a grocery and meal planning comparison application. Its core functionalities include:
*   Aggregating product data from multiple supermarkets (e.g., Albert Heijn, Jumbo, Plus).
*   Allowing users to discover and compare products, meals, and "bags" (curated or custom grocery lists).
*   Providing detailed nutritional information (Nutri-Score, ingredients, calories).
*   Facilitating price comparisons across different supermarkets.
*   Enabling users to create shopping lists, save favorites, and potentially initiate a checkout process by redirecting to supermarket websites.
*   User account management.

The application aims to help users make informed grocery choices, save money, and plan meals efficiently. The primary language for the application is Dutch.

## 4. Core Functionality for Prototype (MVP Focus)

The prototype must include the following MVP 'Must-Have' features, focusing on the user-facing frontend experience. Assume backend APIs will be mocked; clearly define the data contracts your prototype expects for each feature.

**4.1. User Authentication & Account Management:**
*   **Sign Up:** Allow new users to register (e.g., name, email, password).
*   **Login:** Enable existing users to log in.
*   **Password Management:**
    *   Set password during first login/after reset.
    *   "Forgot Password" flow to recover account access.
*   **Logout:** Securely end user session.
*   **Session Management:** Automatic session refresh for a seamless experience.
*   **Account Deletion:** Allow users to delete their accounts and associated data.
*   **Email Templates:** Design for welcome and reset password emails (consistent with SuperMarty branding - see `sm-audit-admin-panel-email.rtf` for an example of current email style).

**4.2. Product Discovery & Details:**
*   **Category Browsing:**
    *   View product categories and sub-categories.
    *   Category header and title.
*   **Product Listings:**
    *   Display products within a selected category.
    *   Implement lazy loading for efficient browsing.
*   **Product Detail Pages:**
    *   Product header (image, title).
    *   Detailed information: description, price.
    *   Nutri-Score and other relevant labels (e.g., organic, gluten-free).
    *   Comprehensive nutritional information table.
    *   Price comparison across different supermarkets for the same product.
    *   List of similar products.
    *   Meals that include the product.
*   **Market-Specific Product Pages:** View real data for a product from a specific market/supermarket.

**4.3. Meal Discovery & Details:**
*   **Meal Categories:** View meal categories.
*   **Meal Listings:** Display meals within a selected category.
*   **Meal Detail Pages:**
    *   Meal header (image, title, total price estimate).
    *   Recipe/preparation instructions (plain text).
    *   Nutri-Score and relevant labels.
    *   List of grocery items (ingredients) for the meal.
    *   Price comparison for the entire meal across different supermarkets.
    *   Ability to add all/selected ingredients to the shopping cart.
    *   Detailed nutritional information for the meal.
    *   Characteristic of a meal (e.g., halal, gluten-free).

**4.4. Bag Discovery & Details ("Bags" are curated/custom grocery lists):**
*   **Bag Categories:** View bag categories.
*   **Bag Listings:** Display bags within a selected category.
*   **Bag Detail Pages:**
    *   Bag header (image, title, description, total price estimate).
    *   Nutri-Score and relevant labels.
    *   List of grocery items in the bag.
    *   Price comparison for the entire bag across different supermarkets.
    *   Ability to add all/selected items to the shopping cart.
    *   Detailed nutritional information for the bag.
    *   Characteristic of a bag.

**4.5. Shopping List & Checkout Process:**
*   **View Shopping List:** Display items added by the user.
*   **Item Management:** Add products, meals, or bags to the shopping list.
*   **Price Totals:** Show total price, potentially broken down by supermarket if items are from multiple sources.
*   **Checkout Initiation:**
    *   Ability to start the checkout process for specific supermarkets (e.g., "Plus" mentioned in requirements). This will likely involve redirecting the user to the supermarket's website with the cart details if possible, or clearly indicating the next steps.

**4.6. Search & Filtering:**
*   **Global Search:** Search across products, meals, and bags.
*   **Filtering:**
    *   Filter products, meals, and bags by attached labels (e.g., "organic", "vegan").
    *   Filter products by market/supermarket.

**4.7. User Personalization & Profile:**
*   **Favorites:** Allow users to add products, meals, or bags to a favorites list.
*   **Saved Custom Bags:** Enable users to create and save their custom bags for reuse.
*   **(If time permits for MVP prototype) User Profile Page:** Basic page to manage account details.
*   **(If time permits for MVP prototype) Intolerances:** Allow users to specify intolerances to personalize suggestions (this is a "Should" have, can be simplified for prototype).

**4.8. General Frontend Features:**
*   **Page Structure:** Well-defined layout for all key pages.
*   **Discover Page:** A central page to browse different products, meals, and bags, possibly with tabbed navigation.
*   **Localization:** The application must be in Dutch. All UI text should be in Dutch or clearly marked for translation.
*   **Nearest Market:** Feature to find the nearest market (can be a conceptual representation in the prototype).

## 5. Design & UX Guidelines

*   **Aesthetic:** The design should be inspired by "lovable" and/or "bold" styles.
    *   **Lovable:** Friendly, approachable, delightful UI, soft edges, inviting color palettes (e.g., inspired by SuperMarty email template - blues, purples, neutrals), smooth micro-interactions. Focus on ease of use and a positive emotional connection.
    *   **Bold:** Confident, clear, high-impact UI, strong typography, vibrant or high-contrast color schemes, clear visual hierarchy, prominent calls-to-action.
    *   **Task:** Propose 2-3 distinct visual directions/mood boards based on your interpretation of "lovable," "bold," or a hybrid, considering the SuperMarty brand (see email `sm-audit-admin-panel-email.rtf` for logo and color hints).
*   **User Experience:**
    *   Modern, intuitive, and highly user-friendly.
    *   Clear navigation and information architecture.
    *   Responsive design: The prototype should be designed for a web experience but consider a mobile-first approach or PWA-like feel, given the project's context (Capacitor mention in roadmap). Ensure usability across common device sizes (desktop, tablet, mobile).
*   **Accessibility:** Keep accessibility principles (e.g., WCAG AA) in mind for color contrast, keyboard navigation, and semantic HTML (if a coded prototype).

## 6. Technical Considerations for Prototype

*   **Frontend Only:** This prototype is purely frontend. All backend data and logic should be assumed to be available via APIs. Create mock data that realistically represents the information needed for each feature.
*   **Technology Stack (Proposal):** Propose a modern frontend technology stack suitable for this prototype (e.g., React, Vue, Svelte, or Flutter Web). Justify your choice briefly.
*   **Interactivity:** The prototype should be clickable and demonstrate key user flows. Focus on UI interactions and transitions.
*   **Data Contracts:** For each feature requiring backend data, list the expected API endpoints (mocked) and the structure of the JSON data the frontend would send or receive.

## 7. Deliverables

1.  **Clickable Prototype:** A high-fidelity, interactive prototype (e.g., Figma, Adobe XD project, or a link to a deployed coded prototype using a service like Netlify/Vercel).
2.  **Design Rationale Document:**
    *   Brief explanation of the chosen visual direction(s) ("lovable," "bold," or hybrid) with supporting mood boards/style scapes.
    *   Justification for the proposed frontend technology stack.
3.  **Mock API Specification:** A document listing the (mocked) API endpoints the prototype consumes, including request/response structures for key interactions.
4.  **List of Implemented MVP Features:** A checklist confirming which of the core functionalities listed in section 4 are covered in the prototype.

## 8. Constraints

*   The prototype must focus *only* on the frontend user experience. No backend implementation is required.
*   The prototype must primarily cover the 'Must-Have' MVP features as outlined. 'Should-Have' or 'Could-Have' features can be included if time permits and they significantly enhance a core MVP flow, but must be clearly marked as such.
*   The primary language of the UI must be Dutch.

## 9. Success Criteria

*   The prototype accurately and comprehensively demonstrates the core MVP user-facing functionalities of SuperMarty.
*   The design is modern, intuitive, user-friendly, and successfully interprets the "lovable" and/or "bold" aesthetic.
*   Key user flows (e.g., registration, product search, adding to cart, viewing meal details) are clear, interactive, and easy to navigate.
*   Deliverables (prototype, design rationale, API specs) are complete and meet the requirements outlined.
*   The prototype effectively communicates the intended user experience to stakeholders.

Please proceed with creating the prototype based on these guidelines. If any requirements are unclear or seem contradictory, please state your assumptions.