# 📚 Collection of UI Components: SuperMarty (shadcn/ui)

> This document contains a collection of all UI components required to build the SuperMarty application, specifically tailored for a React implementation using the **shadcn/ui** component library.

**Purpose of this Collection:** To serve as a detailed blueprint for frontend development. It maps application features to specific shadcn/ui components (or custom composites) to ensure consistency and accelerate development.

---

## Core Components (Reusable)

These are the foundational building blocks of the application's UI, based on `shadcn/ui`.

| shadcn/ui Component | Our Component Name | Description & Key Properties |
| :--- | :--- | :--- |
| `Button` | Button | Standard interactive element. `variant` ('default', 'destructive', 'outline', 'secondary', 'ghost', 'link'), `size`, `asChild`. Can contain an icon. |
| `Input` + `Label` | InputField | For user text input. Often combined with `Label` for accessibility. `type`, `placeholder`, `disabled`, `error` state via styling. |
| `Card` | Card | Container for grouping content. Composed of `CardHeader`, `CardTitle`, `CardDescription`, `CardContent`, `CardFooter`. |
| (Tailwind CSS) | Typography | Text element. No specific component; uses utility classes like `text-h1`, `text-body-1`, etc. (custom-defined in `globals.css`). |
| `Avatar` | Avatar | Circular element for user profile pictures. Composed of `AvatarImage` and `AvatarFallback`. |
| `Checkbox` | Checkbox | A control that allows a user to select one or more options. Often used with `Label`. |
| `Badge` | Tag/Chip | For displaying statuses, filters, or attributes. `variant` ('default', 'secondary', 'destructive', 'outline'). |
| `Accordion` | Accordion / Expandable | A vertically stacked set of interactive headings that each reveal a section of content. |
| `Carousel` | Carousel | A slideshow component for cycling through images or other content. |
| `Table` | Table | Component for displaying tabular data. Composed of `TableHeader`, `TableRow`, `TableHead`, `TableBody`, `TableCell`. |
| `Dropdown Menu` | DropdownMenu | Displays a menu to the user — such as a list of actions or functions — triggered by a button. |
| `Progress` | ProgressBar | Displays an indicator showing the completion progress of a task. |
| `Scroll Area` | ScrollArea | Augments native scroll functionality for custom, cross-browser styling. |
| `Toggle Group` | ToggleGroup | A set of two-state buttons that can be toggled on or off. Useful for multi-select filters. |
| `Collapsible` | Collapsible | An interactive component which expands/collapses a content section. |
| `lucide-react` | Icon | Icon library recommended for use with shadcn/ui. |
| (Custom) | Spinner / Loader | Typically the `Loader2` icon from `lucide-react` with a spinning animation class. |
| (Custom) | SearchBar | Composite component made of `Input` and a `Button` with a search `Icon`. |
| (Custom) | AppBar / NavigationBar | Custom layout components built with `div`s and flexbox, containing other core components. |

---

## Welcome Screen (`/welcome`)

| Component | shadcn/ui Component(s) | Description / Purpose |
| :--- | :--- | :--- |
| **ScreenLayout** | `div` (Tailwind) | A full-screen container that vertically and horizontally centers its content. |
| **AppLogo** | `<img>` / `next/image` | The official SuperMarty logo. |
| **Headline** | `h1` (Tailwind) | A large, welcoming message (e.g., "Welcome to SuperMarty"). |
| **SubHeadline** | `p` (Tailwind) | A short pitch explaining the app's value proposition. |
| **SignUpButton** | `Button` | `variant: 'default'`. The main call-to-action to navigate to the Sign Up screen. |
| **LoginButton** | `Button` | `variant: 'secondary'`. The secondary action to navigate to the Log In screen. |

---

## Login Screen (`/login`)

| Component | shadcn/ui Component(s) | Description / Purpose |
| :--- | :--- | :--- |
| **ScreenLayout** | `div` (Tailwind) | A standard screen layout with a form. |
| **TopBar** | Custom (`div`) | Contains a leading 'Back' `Button` (`variant: 'ghost'`) and a `h2` title. |
| **EmailField** | `Input` + `Label` | `type: 'email'`. For the user to enter their email address. |
| **PasswordField** | `Input` + `Label` | `type: 'password'`. For the user to enter their password. |
| **LoginButton** | `Button` | `variant: 'default'`. Submits the login form. Shows a `Spinner` when in a `loading` state. |
| **ForgotPasswordLink** | `Button` | `variant: 'link'`. Navigates to the Forgot Password screen. |
| **SignUpPrompt** | `p` (Tailwind) | A text element with an inline link: "Don't have an account? **Sign Up**". |

---

## Sign Up Screen (`/signup`)

| Component | shadcn/ui Component(s) | Description / Purpose |
| :--- | :--- | :--- |
| **ScreenLayout** | `div` (Tailwind) | A standard screen layout with a form. |
| **TopBar** | Custom (`div`) | Contains a leading 'Back' `Button` (`variant: 'ghost'`) and a `h2` title. |
| **EmailField** | `Input` + `Label` | `type: 'email'`. For the user's email address. |
| **PasswordField** | `Input` + `Label` | `type: 'password'`. For creating a password. |
| **ConfirmPasswordField**| `Input` + `Label` | `type: 'password'`. For confirming the password. Includes validation logic. |
| **SignUpButton** | `Button` | `variant: 'default'`. Submits the registration form. |
| **LoginPrompt** | `p` (Tailwind) | A text element with an inline link: "Already have an account? **Log In**". |

---

## Home Screen (`/home`)

| Component | shadcn/ui Component(s) | Description / Purpose |
| :--- | :--- | :--- |
| **ScreenLayout** | `ScrollArea` | A vertically scrollable layout that houses different content sections. |
| **TopBar** | Custom (`div`) | Contains a user `Avatar` on the left and notification `Icon` on the right. No title. |
| **MainSearchBar** | Custom (`Input` + `Button`) | A prominent search bar near the top to encourage product discovery. |
| **SectionHeader** | `div` + `h2` + `Button` | A heading for a content section (e.g., "Featured Recipes"), with a "See All" `Button` (`variant: 'link'`). |
| **HorizontalList** | `ScrollArea` | A horizontally scrolling container for displaying cards. |
| **RecipeCard** | `Card` | A preview card for a recipe. Contains an `Image`, recipe name, and prep time. |
| **MealPlanCard** | `Card` | A preview card for a meal plan. Contains an `Image`, plan name, and a short description. |
| **BottomNav** | Custom (`div`) | The primary app navigation bar, fixed to the bottom of the screen. |

---

## Search Results Screen (`/search`)

| Component | shadcn/ui Component(s) | Description / Purpose |
| :--- | :--- | :--- |
| **ScreenLayout** | `div` (Tailwind) | A layout containing filter options and a list of results. |
| **TopBar** | Custom (`div`) | The `SearchBar` is embedded directly into the AppBar. |
| **FilterBar** | `div` + `Badge` | A horizontal row of `Badge` components for filtering results (e.g., "Products", "Recipes"). |
| **SortControl** | `DropdownMenu` | A `Button` that opens a `DropdownMenu` for sorting options (e.g., "Price: Low to High"). |
| **ResultsList** | `ScrollArea` | A vertically scrolling list that displays result items. |
| **ProductListItem** | `Card` | A row in the list for a product. Contains `Image`, name, and price. |
| **EmptyState** | `div` (Tailwind) | A view shown when no results are found. Contains an `Icon` and message. |

---

## Product Detail Screen (`/products/{id}`)

| Component | shadcn/ui Component(s) | Description / Purpose |
| :--- | :--- | :--- |
| **ScreenLayout** | `ScrollArea` | A view that displays all information about a single product. |
| **TopBar** | Custom (`div`) | Contains a 'Back' `Button` and a 'Favorite' `Button` (both `variant: 'ghost'`). |
| **ProductImageCarousel**| `Carousel` | A swipeable carousel of product images. |
| **ProductHeader** | `div` (Tailwind) | Contains the product name (`h1`) and description (`p`). |
| **PriceComparisonTable**| `Table` | A table showing a `SupermarketLogo` (`Image`), name, and price per store. |
| **NutritionalInfo** | `Accordion` | An expandable section that reveals a `Table` of nutritional data. |
| **AddToBagControls** | Custom (`div`) | A sticky footer or section with a quantity stepper (`Button`s and `Input`) and an "Add to Bag" `Button`. |

---

## Shopping Bag Screen (`/bag`)

| Component | shadcn/ui Component(s) | Description / Purpose |
| :--- | :--- | :--- |
| **ScreenLayout** | `div` (Tailwind) | A view with a list of items and a summary footer. |
| **TopBar** | Custom (`div`) | Title: "Shopping Bag". Optional "Clear All" `Button` (`variant: 'link'`). |
| **ItemList** | `ScrollArea` | A list of `ShoppingBagItem` components. |
| **ShoppingBagItem** | `Card` | A row item containing product `Image`, name, price, a `QuantityStepper`, and a 'Remove' `Button`. |
| **EmptyBagView** | `div` (Tailwind) | A view shown when the bag is empty, with an `Icon` and a "Start Shopping" `Button`. |
| **SummaryFooter** | `Card` | A sticky footer `Card` displaying the subtotal and a "Compare Prices" `Button`. |

---

## Checkout & Compare Screen (`/checkout`)

| Component | shadcn/ui Component(s) | Description / Purpose |
| :--- | :--- | :--- |
| **ScreenLayout** | `div` (Tailwind) | A view for comparing the total bag price across different supermarkets. |
| **TopBar** | Custom (`div`) | Title: "Compare & Checkout". |
| **ComparisonList** | `ScrollArea` | A list of `SupermarketComparisonCard`s, sortable by price. |
| **SupermarketComparisonCard** | `Card` | Displays `SupermarketLogo`, total cost, item availability info, and a "Go to Checkout" `Button`. |
| **UnavailableItems** | `Collapsible` | An expandable section within a card that lists items not available at that supermarket. |

---

## Recipe Detail Screen (`/recipes/{id}`)

| Component | shadcn/ui Component(s) | Description / Purpose |
| :--- | :--- | :--- |
| **ScreenLayout** | `ScrollArea` | A view showing a single recipe's details. |
| **TopBar** | Custom (`div`) | Contains a 'Back' `Button` and a 'Favorite' `Button`. |
| **RecipeHeader** | `div` (Tailwind) | Contains a large `Image`, the recipe name (`h1`), and a row of `Badge`s (e.g., "30 Mins", "Vegan"). |
| **IngredientsSection** | `div` (Tailwind) | A section with a header and a list of ingredient strings. |
| **InstructionsSection**| `div` (Tailwind) | A section with a header and a numbered list of instruction steps. |
| **AddToBagFAB** | `Button` | A floating action button (FAB) with an icon and label: "Add Ingredients to Bag". Styled with fixed position. |

---

## Profile Screen (`/profile`)

| Component | shadcn/ui Component(s) | Description / Purpose |
| :--- | :--- | :--- |
| **ScreenLayout** | `div` (Tailwind) | A view for account management. |
| **TopBar** | Custom (`div`) | Title: "Profile". |
| **ProfileHeader** | `div` (Tailwind) | Contains the user's `Avatar`, name (`h2`), and email (`p`). |
| **NavigationList** | `div` (Tailwind) | A list of `NavigationRow` components. |
| **NavigationRow** | `Button` | A clickable row (`variant: 'ghost'`), full-width, with a leading `Icon`, a `label`, and a trailing chevron `Icon`. |
| **LogoutButton** | `Button` | `variant: 'destructive'`. Logs the user out. |

---

## Health Onboarding Flow (`/onboarding/health`)

| Component | shadcn/ui Component(s) | Description / Purpose |
| :--- | :--- | :--- |
| **ScreenLayout** | Custom (`div`) | A multi-step wizard layout that the user swipes or taps through. |
| **ProgressBar** | `Progress` | A bar at the top showing the user's progress through the steps. |
| **StepView** | `div` (Tailwind) | Each step contains a question (`h2`) and interactive controls. |
| **MultiSelectChips** | `ToggleGroup` | A group of `ToggleGroupItem`s that the user can select/deselect (e.g., for allergies). |
| **GoalCheckboxes** | `div` + `Checkbox` | A list of `Checkbox` components with `Label`s for selecting dietary goals. |
| **ConsentStep** | `div` (Tailwind) | A special step with detailed text explaining data usage and a non-pre-ticked `Checkbox` for explicit consent. |
| **NavigationFooter** | `div` (Tailwind) | A footer with "Back" and "Next" / "Finish" `Button`s. |

---

## AI Assistant Chat Screen (`/ai-assistant`)

| Component | shadcn/ui Component(s) | Description / Purpose |
| :--- | :--- | :--- |
| **ScreenLayout** | `div` (Tailwind) | A classic chat interface layout with a sticky footer. |
| **TopBar** | Custom (`div`) | Title: "Super Marty". |
| **MessageList** | `ScrollArea` | A vertically scrolling list that contains `ChatMessage` bubbles. It should auto-scroll to the bottom on new messages. |
| **ChatMessage** | `div` (Tailwind) | A chat bubble component. Styled differently for 'user' or 'bot'. Can contain text or complex components like a `Card`. |
| **ChatInputBar** | `div` (Tailwind) | A sticky footer with a text `Input` and a 'Send' `Button` (`variant: 'ghost'`). |
| **SuggestedPrompts** | `ScrollArea` | A horizontally scrolling list of `Badge`s or `Button`s (`variant: 'outline'`) with suggested questions. |