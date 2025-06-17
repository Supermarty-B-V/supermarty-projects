# ⚙️ Requirements: SuperMarty Backend (MVP)

# 🧩 Actors & Components (Who or what)
*   **System:** The overall backend application.
*   **API:** The interface for the frontend application and admin panel to communicate with the backend.
*   **Database:** Stores all application data (e.g., PostgreSQL).
*   **Admin:** A user with privileges to manage the system's content and users.
*   **Scraping Service:** A Python-based service responsible for data aggregation.
    *   **AlbertHeijn Scraper:** Scrapes product data from Albert Heijn.
    *   **Jumbo Scraper:** Scrapes product data from Jumbo.
    *   **Plus Scraper:** Scrapes product data from Plus.
*   **Supermarket APIs/Websites:** External sources of product data for AH, Jumbo, and Plus.
*   **Scheduled Task Runner (Cron):** Executes periodic tasks, specifically the daily scraping jobs.
*   **Authentication Service:** Manages user and admin authentication (JWT, sessions).
*   **Email Service:** Third-party service (Mailgun) for sending transactional emails (welcome, password reset).

---
# 🎬 Activities (Who or what does what?)
*   **Scraping Service**
    *   [Fetch product data from supermarket sources (AH, Jumbo, Plus)]
    *   [Normalize scraped product data into a standard format]
    *   [Automatically group equivalent products from different supermarkets into a single system product]
*   **Database**
    *   [Store user accounts (admins and end-users)]
    *   [Store system products and their linked market-specific products]
    *   [Store categories (with hierarchy), labels, meals, and bags]
    *   [Store user preferences (e.g., intolerances) and favorite items]
    *   [Store user-created shopping lists]
*   **API**
    *   [Provide endpoints for Admin authentication (login, password reset)]
    *   [Provide endpoints for End-User authentication (signup, login, password reset)]
    *   [Provide CRUD endpoints for System Products]
    *   [Provide endpoints for manually linking/unlinking market products]
    *   [Provide CRUD endpoints for Categories, including managing hierarchy and order]
    *   [Provide CRUD endpoints for Labels, including inline creation]
    *   [Provide CRUD endpoints for Meals (Recipes), including duplication]
    *   [Provide CRUD endpoints for Shopping Bags]
    *   [Provide CRUD endpoints for Admin user management]
    *   [Provide endpoints for End-User shopping list management]
    *   [Provide search and filter capabilities across products, meals, and bags]
*   **Admin**
    *   [Log in to the admin panel]
    *   [Perform CRUD operations on products, categories, labels, meals, and bags]
    *   [Manually override/correct automated product groupings]
    *   [Duplicate existing meals to create new ones quickly]
    *   [Manage other admin users]
*   **System**
    *   [Run scraping jobs on a daily schedule]
    *   [Handle database migrations for schema changes]
    *   [Generate and manage JWT for authentication]
    *   [Send welcome and password reset emails via Mailgun]

---
## 🌊 Activity Flows & Scenarios (What in which order?)
*   **[Automated Product Grouping]**
    *   **Happy Flow:**
        *   GIVEN the scraping service has fetched new products from all supermarkets
        *   WHEN the normalization and grouping process is triggered
        *   AND it identifies two products (e.g., "AH Basic Milk" and "Jumbo Halfvolle Melk") as equivalent based on matching logic
        *   THEN it links both market products to a single system product (e.g., "Halfvolle Melk")
        *   AND the system logs the successful grouping.
    *   **Scenario (Manual Override):**
        *   GIVEN an admin is viewing a system product with incorrectly matched market products
        *   WHEN the admin unlinks an incorrect market product
        *   AND searches for and links the correct market product
        *   THEN the system product's grouping is updated
        *   AND this manual override is preserved during subsequent automated runs.
    *   **Mermaid Diagram:**
        ```mermaid
        graph TD
            A[Start Grouping] --> B{Find Equivalent Products};
            B -->|Match Found| C[Link Market Products to System Product];
            B -->|No Match| D[Create New System Product];
            C --> E[Admin Reviews Grouping];
            E -->|Correct| F[No Action];
            E -->|Incorrect| G[Admin Manually Adjusts Links];
        ```

---
# 📝 Properties (Which values?)
*   **SystemProduct**
    *   `system_product_id : UUID`
    *   `name : string`
    *   `description : text`
    *   `thumbnail_url : string` (For vertical rectangle thumbnail)
    *   `is_published : boolean`
    *   `category_id : UUID`
    *   `labels : array[UUID]`
    *   `nutritional_info : JSONB` (Aggregated or representative)
*   **MarketProduct (linking SystemProduct to a Supermarket)**
    *   `market_product_id : UUID`
    *   `system_product_id : UUID`
    *   `supermarket_name : string` (e.g., 'AlbertHeijn', 'Jumbo', 'Plus')
    *   `market_specific_id : string`
    *   `market_specific_name : string`
    *   `price : decimal`
    *   `unit_of_measure : string`
    *   `url : string`
    *   `image_url : string`
    *   `nutritional_info : JSONB`
*   **User (End-User)**
    *   `user_id : UUID`
    *   `email : string`
    *   `password_hash : string`
    *   `first_name : string`
    *   `last_name : string`
    *   `preferences : JSONB` (e.g., `{ "intolerances": ["gluten", "lactose"] }`)
*   **Admin**
    *   `admin_id : UUID`
    *   `email : string`
    *   `password_hash : string`
    *   `role : string` (Default: 'admin')
*   **Meal**
    *   `meal_id : UUID`
    *   `name : string`
    *   `description : text`
    *   `preparation_instructions : text`
    *   `products : array[system_product_id]`
    *   `total_calories : integer`
*   **Bag**
    *   `bag_id : UUID`
    *   `name : string`
    *   `description : text`
    *   `products : array[system_product_id]`
    *   `total_calories : integer`

---
# 🛠️ Behaviours (How does it act when.. in terms of.. ?)
*   **API**
    *   [Should enforce JWT authentication for all protected endpoints.]
    *   [Should validate all incoming data and return consistent error responses.]
    *   [Should support pagination for all list endpoints to ensure performance.]
*   **Scraping Service**
    *   [Should run automatically on a daily schedule via a cron job.]
    *   [Should respect `robots.txt` and implement reasonable delays to avoid being blocked.]
    *   [Should log errors for failed scrapes and send an alert to an administrator.]
*   **Database**
    *   [Should use foreign key constraints to ensure data integrity.]
    *   [Should have a regular backup and monitoring policy configured.]

---
# 💡 Ideas & 🪵 Backlog
*   [Integrate with Picnic supermarket API.]
*   [Implement automated scraping for recipes from supermarket websites.]
*   [Develop an AI Food Assistant for personalized recommendations (post-MVP).]
*   [Epic 9: Develop a "Data Broker" service for trend analysis.]
*   [Implement advanced user roles and permissions for end-users (e.g., trainer/client hierarchy).]
*   [Implement a caching layer (e.g., Redis) to improve API performance.]

---
# ❓ Questions
*   What is the exact logic for the initial automated product matching? Is it based on name similarity, EAN/barcode, or a combination?
*   For nutritional values on products sold by piece (e.g., avocado), what is the standard weight to use for calculation?
*   What are the specific requirements for the "low-code" admin panel? Does this imply a specific technology (e.g., Retool, Appsmith) or just a goal for rapid development?
*   What are the non-functional requirements regarding performance (e.g., response times, concurrent users) for the MVP?

---
# 🎯 Roles, 📝 Tasks & 🎓 Suggested Approach
*   **🔧 Backend Developer**
    *   [Database]
        *   [ ] Design and implement the database schema for all MVP models.
        *   [ ] Set up database migrations.
    *   [Scraping Service]
        *   [ ] Implement scrapers for Albert Heijn, Jumbo, and Plus.
        *   [ ] Implement the data normalization and automated product grouping logic.
    *   [API]
        *   [ ] Develop authentication endpoints for admins and end-users (email/password).
        *   [ ] Develop all CRUD API endpoints for products, categories, labels, meals, and bags.
        *   [ ] Implement API for manual product matching override.
        *   [ ] Implement search, filtering, and pagination.
        *   [ ] Integrate with Mailgun for sending transactional emails.
*   **🚀 DevOps Engineer**
    *   [Infrastructure]
        *   [ ] Set up and configure a Virtual Machine (VM) for production.
        *   [ ] Configure CI/CD pipelines for automated deployment.
        *   [ ] Configure cron jobs for the daily scraping service.
        *   [ ] Implement monitoring, logging, and alerting.
        *   [ ] Configure database backups (100GB storage).
        *   [ ] Configure Mailgun service and SSL certificate (Comodo).
*   **📌 Project Manager**
    *   [Planning]
        *   [ ] Refine user stories and acceptance criteria for all backend tasks.
        *   [ ] Coordinate with the frontend team on API contracts.
        *   [ ] Manage project timeline and priorities for backend development.