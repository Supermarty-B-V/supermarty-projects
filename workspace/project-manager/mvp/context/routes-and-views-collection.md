# 📚 Collection of Routes & Views: SuperMarty Application

> This document contains a collection of all planned routes and views for the SuperMarty MVP. The purpose is to create a centralized map of the application's structure for developers, defining the scope of frontend navigation and API routing.

**Purpose of this Collection:** To serve as a single source of truth for all navigational paths within the user-facing application and the internal admin panel. This ensures alignment between frontend routing and backend API endpoint design.

---

## User-Facing App Routes (Flutter)

These routes represent the screens a user will interact with in the iOS, Android, and Web applications.

| Route Path                  | View / Screen Name            | Description / Key Features                                                                                             |
| :-------------------------- | :---------------------------- | :--------------------------------------------------------------------------------------------------------------------- |
| **Authentication**          |                               |                                                                                                                        |
| `/welcome`                  | Welcome Screen                | Initial screen for new users, presenting options to sign up or log in.                                                 |
| `/login`                    | Login Screen                  | Form for existing users to enter their credentials.                                                                    |
| `/signup`                   | Sign Up Screen                | Form for new users to create an account.                                                                               |
| `/forgot-password`          | Forgot Password Screen        | Form for users to request a password reset link.                                                                       |
| **Core Shopping**           |                               |                                                                                                                        |
| `/home`                     | Home Screen                   | Main dashboard. Displays featured content like recipes, meal plans, and special offers. Includes a prominent search bar. |
| `/search`                   | Search Results Screen         | Displays results from a global search. Includes filters for categories, price, etc.                                    |
| `/products/{id}`            | Product Detail Screen         | Shows all details for a single "shadow product," including description, images, nutritional info, and price comparison.  |
| `/categories`               | Categories Screen             | A list or grid of all top-level product categories for browsing.                                                       |
| `/categories/{id}`          | Category Products Screen      | Displays all products within a selected category.                                                                      |
| `/bag`                      | Shopping Bag Screen           | Lists all items added to the user's cart, with options to adjust quantity or remove items.                               |
| `/checkout`                 | Checkout & Compare Screen     | Displays the final price comparison for the entire shopping bag across different supermarkets. Provides redirect links.  |
| **Content & Discovery**     |                               |                                                                                                                        |
| `/recipes`                  | Recipe Discovery Screen       | Browse and search for all available recipes.                                                                           |
| `/recipes/{id}`             | Recipe Detail Screen          | Shows recipe instructions, ingredients, and prep time. Includes an "Add all to bag" button.                              |
| `/meal-plans`               | Meal Plan Discovery Screen    | Browse and search for all available meal plans (e.g., "Weekly Vegan Plan").                                            |
| `/meal-plans/{id}`          | Meal Plan Detail Screen       | Shows the collection of recipes for a meal plan. Includes an "Add all to bag" button.                                    |
| **User Profile**            |                               |                                                                                                                        |
| `/profile`                  | Profile Screen                | Main user account hub. Links to favorites, health profile, and settings.                                               |
| `/profile/favorites`        | Favorites Screen              | A list of all products, recipes, and meal plans the user has saved.                                                    |
| `/profile/health`           | Health Profile Screen         | Allows the user to view and manage their stored health data (allergies, intolerances, dietary goals).                  |
| `/onboarding/health`        | Health Onboarding Flow        | A one-time, guided flow to collect user health preferences and obtain explicit GDPR consent.                             |
| **AI Assistant**            |                               |                                                                                                                        |
| `/ai-assistant`             | AI Assistant Chat Screen      | The main natural language chat interface for interacting with "Super Marty" for personalized suggestions.                |
| `/ai-assistant/onboarding`  | Guided Assistant Flow         | The initial, clickable Q&A flow for generating a meal plan based on structured inputs (budget, preferences, etc.).     |

---

## Internal Admin Panel Routes (Retool)

These routes are for the internal admin dashboard used for data management and operations.

| Route Path            | View / Screen Name         | Description / Key Features                                                                 |
| :-------------------- | :------------------------- | :----------------------------------------------------------------------------------------- |
| `/`                   | Admin Dashboard            | Main landing page with key metrics and links to management sections.                       |
| `/product-matches`    | Product Matching Queue     | Interface for admins to review, approve, or reject automated product matches.              |
| `/products`           | Product Management         | CRUD interface for managing "shadow products" and viewing linked supermarket products.     |
| `/categories`         | Category Management        | CRUD interface for product categories.                                                     |
| `/recipes`            | Recipe Management          | CRUD interface for creating and editing recipes and their ingredients.                     |
| `/meal-plans`         | Meal Plan Management       | CRUD interface for creating and editing meal plans.                                        |
| `/users`              | User Management            | View and manage user accounts (for support purposes, non-sensitive data only).             |

---

### Notes

*   **User-Facing App:** The primary application is built with Flutter to target Web, iOS, and Android. The routing will be handled by a Flutter navigation package.
*   **Admin Panel:** The admin panel will be built using Retool, a low-code platform. The "routes" represent different pages or views within the Retool application.