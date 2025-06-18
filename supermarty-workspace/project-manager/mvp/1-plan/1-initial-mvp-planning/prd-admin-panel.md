# ⚙️ Requirements: Admin Panel (Retool)

> **Note:** Admin Panel development begins in **MVP 1**. MVP 0 is focused exclusively on the user-facing frontend prototype.

---
# 🧩 Actors & Components (Who or what)
*   **Admin:** A user with privileges to manage the system's data.
*   **Retool Application:** The web-based internal tool for administration.
*   **Dashboards**
    *   `[Product Management Dashboard]`
    *   `[Match Review Dashboard]`
    *   `[Meal & Recipe Management Dashboard]` (MVP 2)
    *   `[User Health Data Dashboard]` (MVP 3, Read-only, highly restricted access)
*   **UI Components**
    *   `[Table View]`
    *   `[Search/Filter Controls]`
    *   `[Form]` (for editing data)
    *   `[Side-by-Side Match Comparison View]`
*   **Supabase Database:** The external data source.

---
# 🎬 Activities (Who or what does what?)
*   **Admin**
    *   [Log in securely to the Retool application]
    *   [View and manage Shadow Products and their linked Market Products]
    *   [Review, approve, or reject medium-confidence product matches]
    *   [Perform full CRUD operations on Meal Plans and Recipes] (MVP 2)
    *   [Link Recipes to Meal Plans] (MVP 2)
    *   [View a specific user's health data for support purposes, with explicit user consent and full audit logging] (MVP 3)
    *   [View anonymized analytics about AI assistant usage and performance] (MVP 3)

---
## 🌊 Activity Flows & Scenarios (What in which order?)
*   **[Manual Product Match Review (MVP 1)]**
    *   **Happy Flow:**
        *   GIVEN an Admin is on the `Match Review Dashboard`
        *   WHEN the Admin selects a pending match
        *   AND clicks "Approve" in the side-by-side view
        *   THEN the products are linked in the database and removed from the queue.
*   **[Create a Meal Plan (MVP 2)]**
    *   **Happy Flow:**
        *   GIVEN an Admin is on the `Meal & Recipe Management Dashboard`
        *   WHEN the Admin clicks "Create New Meal Plan"
        *   AND fills in the name and description
        *   AND uses a search component to find and add existing recipes to the plan
        *   AND clicks "Save"
        *   THEN a new meal plan is created in the database.
    *   **Mermaid Diagram:**
        ```mermaid
        graph TD
            A[Navigate to Meal Dashboard] --> B[Click "Create Meal Plan"];
            B --> C[Enter Details (Name, Desc)];
            C --> D[Search & Add Recipes];
            D --> E[Save Meal Plan];
            E --> F[Record Created in DB];
        ```
*   **[View User Health Data (MVP 3)]**
    *   **Happy Flow:**
        *   GIVEN an Admin has explicit user consent and navigates to the `User Health Data Dashboard`
        *   WHEN the Admin enters the user's ID or selects from a list
        *   AND clicks "Fetch Data"
        *   THEN the user's health goals, intolerances, and related metrics are displayed—read-only.
*   **[AI Monitoring Overview (MVP 3)]**
    *   **Scenario:**
        *   GIVEN an Admin is on the `AI Monitoring Dashboard`
        *   WHEN the page loads
        *   THEN anonymized analytics about assistant usage and performance are displayed with filters by date and metric.

---
# 📝 Properties (Which values?)
*   **Product Table View**
    *   `columns : [ID, Name, Category, Is Published, Linked Market Products Count]`
*   **Recipe Form (MVP 2)**
    *   `name : text_input`
    *   `description : text_area`
    *   `instructions : rich_text_editor`
    *   `ingredients : multi_select_product_search`
*   **Meal Plan Form (MVP 2)**
    *   `plan_name : text_input`
    *   `plan_description : text_area`
    *   `linked_recipes : multi_select_recipe_search`
*   **User Health Data View (MVP 3)**
    *   `user_id : text` (Read-only)
    *   `goals : tag_list` (Read-only)
    *   `intolerances : tag_list` (Read-only)
    *   `last_updated : timestamp` (Read-only)

---
# 🛠️ Behaviours (How does it act when.. in terms of.. ?)
*   **Security**
    *   [Access to the Retool application must be restricted to authorized admins via Supabase Auth.]
    *   [All write operations must be logged with the admin's ID and a timestamp.]
    *   [Access to the User Health Data Dashboard must be protected by an additional layer of permissions and require a documented reason for access.] (MVP 3)
*   **Performance**
    *   [All data tables must use server-side pagination to ensure fast load times.]
*   **Usability**
    *   [The workflow for reviewing matches must be optimized for speed.]
    *   [The interface for creating recipes and meal plans must be intuitive, with powerful search capabilities for finding products and recipes.] (MVP 2)

---
# 💡 Ideas & 🪵 Backlog
*   [Add a dashboard to visualize key system metrics (e.g., number of products scraped per day, match accuracy rate).]
*   [Implement bulk actions (e.g., approve/reject multiple matches at once).]
*   [Create a full CRUD interface for all database tables (Categories, Labels, etc.).]
*   [Enhance AI Monitoring Dashboard with anomaly detection alerts.] (MVP 3)
*   [Allow exporting meal plans to PDF or CSV.] (MVP 2)

---
# ❓ Questions
*   What specific roles and permissions are needed for the admin panel? (Assumption: MVP1 starts with a single "super admin" role).
*   What are the key metrics to display on the AI assistant monitoring dashboard? (MVP 3).
*   Should meal plans support scheduling or recurring plans? (MVP 2).
*   How to handle large health data payloads to maintain performance? (MVP 3).

---
# 🎯 Roles, 📝 Tasks & 🎓 Suggested Approach
*   **🔧 Backend Developer**
    *   [ ] Ensure Supabase database is accessible to Retool.
    *   [ ] Create specific database views or functions to simplify data fetching for all dashboards.
    *   [ ] Implement robust audit logging for all admin actions, especially for health data access.
*   **🖥️ Frontend Developer (Retool)**
    *   [MVP 1]
        *   [ ] Build the Product Management and Match Review dashboards.
    *   [MVP 2]
        *   [ ] Build the Meal & Recipe Management dashboard with full CRUD capabilities.
    *   [MVP 3]
        *   [ ] Build the restricted-access User Health Data dashboard.
        *   [ ] Build the AI Monitoring dashboard.
*   **📌 Project Manager**
    *   [ ] Onboard and train the admin team on how to use all dashboards.
    *   [ ] Define the access control policy for viewing sensitive user data.
    *   [ ] Monitor rollout of new MVP2 and MVP3 features and gather feedback.