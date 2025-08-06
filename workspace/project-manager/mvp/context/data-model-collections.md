# 📚 Collection of Data Models: SuperMarty MVP

> This document contains a collection of Data Models relevant to the SuperMarty MVP. The purpose is to centralize the definition of all data structures for easy reference by the project team, ensuring consistency between the frontend, backend, and database schema.

**Purpose of this Collection:** To define the core entities of the SuperMarty application. These models will serve as the single source of truth for API contracts, database design, and application state management.

---

## Collection Items

| Item | Type / Category | Description / Key Attributes |
| :--- |:----------------| :--- |
| **User** | Data Model      | Represents an end-user of the application. Handles authentication and basic identity. <br> ```json { "id": "uuid", "email": "string", "created_at": "timestamp" } ``` |
| **UserProfile** | Data Model      | Stores non-sensitive user information and preferences. Linked one-to-one with User. <br> ```json { "user_id": "uuid", "first_name": "string", "last_name": "string", "avatar_url": "string" } ``` |
| **HealthProfile** | Data Model      | Securely stores sensitive user health data, managed with explicit consent. Linked one-to-one with User. Requires row-level security. <br> ```json { "user_id": "uuid", "allergies": ["string"], "intolerances": ["string"], "dietary_goals": ["string"], "consent_granted": "boolean", "consent_timestamp": "timestamp" } ``` |
| **Supermarket** | Data Model      | Represents a supermarket chain. <br> ```json { "id": "uuid", "name": "string", "logo_url": "string", "website_url": "string" } ``` |
| **Category** | Data Model      | Represents a product category (e.g., "Dairy & Eggs", "Fruits"). Can be hierarchical. <br> ```json { "id": "uuid", "name": "string", "parent_id": "uuid" } ``` |
| **ShadowProduct** | Dlata Model     | The core, abstract product that unifies identical items across different supermarkets. This is what users add to their bag. <br> ```json { "id": "uuid", "name": "string", "description": "text", "image_url": "string", "category_id": "uuid" } ``` |
| **Product** | Data Model      | A specific product instance from a single supermarket, linked to a ShadowProduct. <br> ```json { "id": "uuid", "shadow_product_id": "uuid", "supermarket_id": "uuid", "name_in_store": "string", "ean": "string", "price": "decimal", "unit_of_measure": "string", "url": "string", "image_url_in_store": "string", "is_available": "boolean", "last_scraped_at": "timestamp" } ``` |
| **NutritionalInfo** | Data Model      | Nutritional information for a product. Linked one-to-one with Product. <br> ```json { "product_id": "uuid", "energy_kj": "integer", "energy_kcal": "integer", "fat_g": "decimal", "saturated_fat_g": "decimal", "carbs_g": "decimal", "sugars_g": "decimal", "protein_g": "decimal", "salt_g": "decimal" } ``` |
| **ProductMatch** | Data Model      | Logs an automated or manual match between a supermarket product and a shadow product. Used for admin review. <br> ```json { "id": "uuid", "product_id": "uuid", "shadow_product_id": "uuid", "confidence_score": "float", "status": "enum('pending', 'approved', 'rejected')", "matched_by": "string" } ``` |
| **ShoppingBag** | Data Model      | A user's shopping cart. <br> ```json { "id": "uuid", "user_id": "uuid", "created_at": "timestamp", "updated_at": "timestamp" } ``` |
| **ShoppingBagItem** | Data Model      | An item within a shopping bag. <br> ```json { "id": "uuid", "shopping_bag_id": "uuid", "shadow_product_id": "uuid", "quantity": "integer" } ``` |
| **Recipe** | Data Model      | A recipe with instructions and ingredients. <br> ```json { "id": "uuid", "name": "string", "description": "text", "instructions": "text", "image_url": "string", "prep_time_minutes": "integer", "cook_time_minutes": "integer" } ``` |
| **RecipeIngredient** | Data Model      | Links a recipe to a shadow product, defining the quantity needed. <br> ```json { "id": "uuid", "recipe_id": "uuid", "shadow_product_id": "uuid", "quantity": "decimal", "unit": "string" } ``` |
| **MealPlan** | Data Model      | A curated collection of recipes, e.g., for a week. <br> ```json { "id": "uuid", "name": "string", "description": "text" } ``` |
| **MealPlanRecipe** | Data Model      | Join table linking Meal Plans and Recipes. <br> ```json { "meal_plan_id": "uuid", "recipe_id": "uuid", "day_of_week": "integer" } ``` |
| **Favorite** | Data Model      | A polymorphic link for a user's favorite items. <br> ```json { "user_id": "uuid", "favoritable_id": "uuid", "favoritable_type": "enum('ShadowProduct', 'Recipe', 'MealPlan')" } ``` |
| **CuratedBag** | Data Model      | A pre-defined list of products (e.g., "Weekly Essentials"). Admin-created. <br> ```json { "id": "uuid", "name": "string", "description": "text" } ``` |
| **CuratedBagItem** | Data Model      | Join table linking Curated Bags and Shadow Products. <br> ```json { "curated_bag_id": "uuid", "shadow_product_id": "uuid", "quantity": "integer" } ``` |

---

### Notes

*   **User & Profiles:** A `User` is created via Supabase Auth. `UserProfile` and `HealthProfile` tables extend the `User` with a one-to-one relationship using the `user_id` as a foreign key. `HealthProfile` data must be encrypted at rest and protected by strict Row-Level Security (RLS) policies.
*   **Products & Supermarkets:** The core of the product system is the `ShadowProduct`, which is the abstract item. Each `ShadowProduct` is linked to one or more `Product` entries, where each `Product` represents the item as sold by a specific `Supermarket`. This allows for price comparison.
*   **Recipes & Meal Plans:** `Recipe`s are composed of `RecipeIngredient`s, which point to `ShadowProduct`s. This way, when a user adds a recipe to their bag, the system knows which abstract products to add. `MealPlan`s are collections of `Recipe`s.
*   **Bags:** There are two types of "bags". The `ShoppingBag` is the user's personal, temporary cart. The `CuratedBag` is a pre-made, reusable list of products created by an admin (e.g., for promotions).
*   **Favorites:** The `Favorite` model uses polymorphism (`favoritable_id`, `favoritable_type`) to allow a user to save different types of entities (products, recipes, etc.) in a single table.
