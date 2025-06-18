Understood. I’ll conduct an in-depth analysis of integration feasibility for transferring a shopping bag from SuperMarty to Albert Heijn, Jumbo, and Plus in the Netherlands.

This will include examining available APIs, shared cart URLs, affiliate or partner programs, and any other technical routes including reverse engineering for understanding—not recommendation. I’ll also evaluate technical limitations like product identifiers, login requirements, and maximum cart sizes. Finally, I’ll suggest a phased integration roadmap for each supermarket.

I’ll share the full report with you as soon as it’s ready.


# Integration Feasibility for Albert Heijn, Jumbo, and PLUS

## Albert Heijn

**Shared Cart URLs:** Albert Heijn supports creating a “Mijn lijst” shopping list via URL. For example, visiting `https://www.ah.nl/mijnlijst/add-multiple?p=230720:1&p=448504:2` will attempt to add 1 unit of product 230720 and 2 of product 448504 to the user’s list. These numeric IDs come from the product page URLs (e.g. `/producten/product/wi230720`). In practice, this only creates a list (not a fully-checked-out cart) – the user still must click “Add to cart” on the site. This link requires the user to be signed in (since it acts on the user’s personal “Mijn lijst”).

**Official APIs:** AH does not publish a public cart API. However, its mobile app uses private REST endpoints (requiring OAuth tokens) for product search, lists, and carts. For example, one must obtain a bearer token via the AH auth API and include it in requests. We see that the app’s internal “add to list” call is a PATCH to `/mobile-services/shoppinglist/v2/items` with JSON payloads like `{"items":[{"originCode":"PRD","productId":450534,"quantity":1,"type":"SHOPPABLE"}]}`. All payloads use AH’s internal numeric product IDs. These APIs require a valid login and are undocumented for third parties, so deep integration would need an official partner agreement.

**Affiliate Program:** AH runs its own affiliate program (previously on networks like Partnerize/Performance Horizon). Affiliates can link to AH product pages, but there is no special affiliate URL that preloads a cart or list. In one report, the AH “Zet op je lijst” feature on a blog triggered a Partnerize affiliate redirect, indicating that affiliate links can wrap list-adding actions, but details are proprietary. In summary, the AH affiliate program exists for tracking but does not natively enable multi-item cart injection.

**Reverse Engineering:** Technically, one could simulate AH’s web or mobile behavior (e.g. by automating the app’s HTTP API or scripting the website) to build a cart. For example, the mobile API uses predictable calls and numeric IDs. However, AH’s servers employ rate limits and may block automated requests; as one insider noted, “the APIs are not public, and scraping is only allowed up to a certain number of requests, after which your IP is blocked”. Attempting this violates AH’s terms of use and carries legal risk.

| **Method**          | **Format / Support**                                                            | **Limitations / Requirements**                                                                                                                            | **Product IDs**                                          |
| ------------------- | ------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------- | -------------------------------------------------------- |
| Shared Cart URLs    | `https://www.ah.nl/mijnlijst/add-multiple?p=ID:qty&…`                           | Adds items to *shopping list* (not full cart); requires user login; browser still shows a “Add to cart” button for each item.                             | AH’s internal numeric IDs (from URLs)                    |
| Official API        | No public API. Private mobile-app REST (OAuth) exists                           | Requires authentication (access\_token); undocumented and subject to change. Only usable by integration partners or via unsupported hack.                 | Same AH numeric product IDs (used in API)                |
| Affiliate Program   | Yes – in-house affiliate (Performance Horizon / Partnerize)                     | Provides tracked links to product pages; no official cart-list integration. Affiliates can use deep links but cannot programmatically set multiple items. | Product URLs (embed AH ID); affiliate tags (as required) |
| Reverse Engineering | Possible (web/mobile scraping); e.g. use Selenium or intercept mobile API calls | Likely violates ToS; subject to IP blocking and captchas. Requires maintaining a full AH login/session.                                                   | N/A (requires above IDs)                                 |

**Implementation Roadmap (AH):**

1. *Phase 1 (MVP)*: Generate a simple redirect or list of affiliate product links (e.g. using AH’s affiliate or search pages). This gets users to the AH site with products pre-selected.
2. *Phase 2*: Implement the `mijnlijst/add-multiple` link format to preload a shopping list of SuperMarty items (using numeric AH IDs). This improves UX by populating the AH list in one click. Users still confirm and check out manually.
3. *Phase 3*: Pursue deep integration via AH’s partner program – e.g. become an authorized affiliate or API partner. This could allow direct cart injection or checkout API access (subject to AH’s policies).

## Jumbo

**Shared Cart URLs:** Jumbo has no publicly documented URL scheme for creating carts or lists. Its online store doesn’t support adding multiple products via a query string in the same way AH does. We found no evidence of any `add-multiple` or list-generation URL on jumbo.com.

**Official APIs:** Jumbo does not offer a public developer API. Internally, the Jumbo mobile app/back-end does use REST endpoints for orders and baskets – as evidenced by community projects. For example, the Python “jumbo-api” library pulls basket and order data from the app’s endpoints. However, this is **unofficial**: it requires the user’s Jumbo credentials, and reverse-engineered endpoints. No documentation or partner program exists for external API access.

**Affiliate Program:** Jumbo.com runs an affiliate program via TradeTracker (4% commission). This supports standard deep-links (i.e. affiliates can link to any jumbo.com product page or category). However, there is no special affiliate parameter to batch-add items. Thus, any carting integration would still rely on the user manually adding items after arriving.

**Reverse Engineering:** In principle, one could try to simulate Jumbo’s app or web flow (e.g. by posting to their mobile API or automating the site). Community reports advise caution: “the APIs are not public, and scraping is only allowed up to a certain number of requests, after which your IP is blocked”. In practice, one could retrieve product lists or basket details from the app’s JSON endpoints (as done by Home Assistant integrations), but attempting to automate adding to cart risks tripping Jumbo’s anti-bot measures and is not officially permitted.

| **Method**          | **Format / Support**                                                             | **Limitations / Requirements**                                                                                                                | **Product IDs**                                       |
| ------------------- | -------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- | ----------------------------------------------------- |
| Shared Cart URLs    | **Not supported.** No known URL scheme for multi-item cart or list on jumbo.com. | N/A (cannot auto-create list via link).                                                                                                       | N/A                                                   |
| Official API        | No public API. Unofficial mobile app endpoints exist.                            | Endpoints require login/auth (Jumbo account); not documented; could change without notice. Integration must be unofficial or via partnership. | Likely internal SKUs or EANs (used in app/data feeds) |
| Affiliate Program   | Yes – Jumbo.com on TradeTracker (4% commission).                                 | Only provides referral links to product pages. No support for passing multiple items.                                                         | Uses Jumbo product page IDs (embedded in URLs)        |
| Reverse Engineering | Possible (web scraping or using mobile API).                                     | Likely violates ToS; Jumbo actively blocks excessive scraping. Requires full Jumbo login/session.                                             | N/A (would need SKU/EAN resolution)                   |

**Implementation Roadmap (Jumbo):**

1. *Phase 1 (MVP)*: Provide simple links to Jumbo’s website or affiliate product pages (one link per item). This directs users to Jumbo with items ready to add, albeit not automatically placed in a basket.
2. *Phase 2:* (No direct analogue to AH’s shared list; could skip or try to simulate a consolidated link using an intermediate landing page or affiliate deep-link tool if available.)
3. *Phase 3:* Explore official partnership with Jumbo (e.g. via TradeTracker or direct B2B channel). If Jumbo ever offers a checkout API (currently there is none), integrate that. Otherwise, consider lightweight automation for power users, with full disclosure of risks.

## PLUS

**Shared Cart URLs:** PLUS.nl does not support a multi-item cart via URL. Its product pages (e.g. `https://www.plus.nl/product/...-908409`) have “Toevoegen” and “Bewaar in je lijstje” buttons, but no query-string interface for batch adds. We found no documented way to encode multiple Plus items in a single URL.

**Official APIs:** PLUS offers no public cart or checkout API. The website appears to be a standard e-commerce front end without a developer interface. (Internally, Plus is part of Ahold Delhaize but has its own systems; it does not publish any partner API for cart creation.) Therefore, the only programmatic access is web scraping or reverse-engineered calls, which is unsupported.

**Affiliate Program:** PLUS runs an affiliate program via Awin. Affiliates can generate tracked links to Plus.nl (for example, to individual product pages). Like Jumbo, this yields standard referral links; there is no affiliate URL format for injecting an entire list. Affiliates earn commissions on purchases after redirection, but integration is limited to product or category pages.

**Reverse Engineering:** One could try to automate interactions with the Plus site (e.g. by posting to its internal AJAX endpoints or scripting the browser). However, this again risks breaching Plus’s terms and triggering defenses. As with other retailers, automated scraping is generally frowned upon; Plus does not provide a public API for this. Any deep integration would be ad hoc and legally uncertain.

| **Method**          | **Format / Support**                                 | **Limitations / Requirements**                                                                                       | **Product IDs**                                  |
| ------------------- | ---------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------ |
| Shared Cart URLs    | **Not supported.** No bulk-add URL.                  | N/A (each item must be added via UI).                                                                                | N/A                                              |
| Official API        | None. No public API or partner checkout integration. | Any integration would require unsupported web scraping or a custom solution; no guarantees of stability or legality. | N/A                                              |
| Affiliate Program   | Yes – PLUS NL on Awin (FamilyBlend).                 | Only provides affiliate links to pages; no multi-item linking.                                                       | Uses Plus internal product IDs (numeric in URLs) |
| Reverse Engineering | Possible via web or mobile traffic inspection.       | Violates website terms; risk of blocks. Requires maintaining session and potentially solving captchas.               | N/A                                              |

**Implementation Roadmap (PLUS):**

1. *Phase 1 (MVP)*: Offer Plus product links (using Awin affiliate links if possible) so users can click through to each item in their basket. This is equivalent to manual selection on Plus.nl.
2. *Phase 2:* (No bulk URL is available, so Phase 2 may focus on usability: e.g., compiling all items on an intermediate page with one-click navigation to each product on Plus.)
3. *Phase 3:* Investigate any partner opportunities with Plus/Ahold Delhaize. If Plus ever provides a B2B API (currently none is public), integrate it; otherwise, consider offering an assisted shopping mode (e.g. prefilled lists that the user applies in their Plus account).

**Sources:** We drew on community research and documentation for these findings. Each supermarket’s affiliate network (TradeTracker or Awin) confirms the existence of merchant programs. Note that the absence of official APIs means all URL schemes and scraping methods are unofficial and may change without notice.
