
# **Supermarket Checkout Integration: A Technical Feasibility Report**

## **I. Executive Summary & Consolidated Strategic Roadmap**

### **A. Introduction & Primary Objective**

This report presents a comprehensive technical feasibility analysis for integrating the SuperMarty shopping bag with the online checkout processes of three leading Dutch supermarkets: Albert Heijn, Jumbo, and Plus. The primary objective is to investigate and define viable technical pathways that would allow a user to compile a shopping list within the SuperMarty application and seamlessly transfer that list to their chosen supermarket's e-commerce platform to complete the purchase. The analysis covers a spectrum of integration methods, from simple Minimum Viable Product (MVP) solutions to deep, partnership-based integrations, providing a clear, actionable roadmap for progressive implementation.

### **B. Key Findings & Overarching Analysis**

The investigation into the technical landscapes of Albert Heijn, Jumbo, and Plus reveals several critical patterns that shape the strategic options for integration.

First, the available integration pathways present a fundamental strategic choice between long-term stability and short-term functional perfection. For Albert Heijn and Jumbo, there is a clear divergence between a legitimate, stable, but potentially less seamless "Partnership" route via official affiliate networks, and a highly functional but unstable and legally perilous "Piracy" route via the reverse-engineering of private mobile APIs. The research shows a consistent lack of public, documented APIs for creating shopping carts.1 However, there is also strong evidence of functional but unofficial APIs that power the supermarkets' own applications.3 This creates a distinct fork in the road. The official affiliate programs offer a sanctioned "front door" to partnership.7 Conversely, relying on the unofficial "back door" introduces significant business risks, including the potential for IP address blocking and unannounced API changes that would break the integration, making it an untenable strategy for a reliable commercial product.10 This reality pushes the affiliate partnership route to the forefront, despite its potential user experience limitations.

Second, the three target supermarkets exhibit vastly different levels of architectural maturity and openness, which directly impacts the potential for deep integration. PLUS Supermarkets, built on the modern, API-first Commercetools platform, is architecturally primed for the type of "composable commerce" integration SuperMarty aims to achieve.12 Albert Heijn also possesses a sophisticated, modern technology stack, including a private GraphQL API, but maintains a proprietary, closed ecosystem.1 Jumbo similarly utilizes a modern GraphQL API but appears less focused on publicizing its technology platform.5 A platform like Commercetools is designed specifically for the kind of integration being explored, meaning a formal partnership with PLUS could likely yield a true API-based cart transfer with relative ease. In contrast, persuading Albert Heijn or Jumbo to grant access to their private, business-critical APIs would require a much more significant strategic effort. This technical landscape suggests that the "Deep Integration" phase of the roadmap should prioritize a partnership with PLUS.

Third, leveraging official affiliate programs to create "deep links" to specific products emerges as the universal MVP. This approach is the most reliable, lowest-risk, and immediately applicable starting point for all three supermarkets. Albert Heijn (Partnerize), Jumbo (Tradetracker), and PLUS (Awin) all maintain active affiliate programs on major networks.7 These networks provide the tools necessary to generate tracked links that direct a user to a specific product page.14 While this method does not automatically populate a multi-item shopping cart in a single step, it represents a significant improvement over a simple redirect to the supermarket's homepage. It is a legitimate, stable, and potentially revenue-generating (via commission) first step that serves to establish a formal business relationship with each supermarket.

### **C. Consolidated Implementation Roadmap**

The following table provides a high-level, consolidated roadmap for a phased integration approach, summarizing the recommended strategy for each supermarket. This overview is designed to aid in strategic planning and resource allocation.

| Phase | Albert Heijn | Jumbo | PLUS |
| :---- | :---- | :---- | :---- |
| **Phase 1 (MVP)** | **Affiliate Deep Linking:** Join the Partnerize program. Implement deep links from SuperMarty products to corresponding product pages on ah.nl. | **Affiliate Deep Linking:** Join the Tradetracker program. Implement deep links from SuperMarty products to corresponding product pages on jumbo.com. | **Shared Cart URL / Affiliate Deep Linking:** Join the Awin program. Test and implement a hypothesized shared cart URL. If not possible, use Awin deep linking as the primary MVP. |
| **Phase 2 (Enhancement)** | **"Buy Button" Integration:** Leverage the Partnerize affiliate program's "buy button" functionality to allow users to add single items to their AH cart directly. | **Partnership Escalation:** Engage with the Tradetracker account manager to explore options for a pre-filled cart link, which may be an unadvertised feature for key partners. | **Optimize Cart Transfer:** If the shared cart URL is functional, this phase involves optimization. If not, work with the affiliate partner (FamilyBlend) to enable this functionality. |
| **Phase 3 (Deep Integration)** | **API Partnership:** Leverage the affiliate relationship to pursue a formal partnership with AH Technology, aiming for access to their private GraphQL API for direct, multi-item cart creation. | **API Partnership:** Build on the affiliate relationship to propose a technical partnership with Jumbo, with the goal of gaining documented access to their private GraphQL API. | **Direct API Integration:** Prioritize a formal technical partnership to gain access to the Commercetools backend APIs for a fully seamless, server-to-server cart transfer. |

---

## **II. Albert Heijn: Integration Deep Dive**

### **A. Technical Ecosystem Overview**

Albert Heijn (AH) operates as a technologically advanced retailer with a significant in-house division, "AH Technology," dedicated to making it the "\#1 food & tech retailer".1 Their strategy focuses on leveraging data and technology to enhance the entire shopping experience, from personalized advice to simplifying online ordering.1 The company's e-commerce and mobile platforms are built upon a sophisticated microservices architecture hosted on Microsoft Azure and utilizing MongoDB Atlas for its data layer.18 Critically, client-facing applications like the "Appie" app interact with a private GraphQL API, signaling a modern but intentionally closed technical ecosystem.13

### **B. Analysis of Integration Pathways**

#### **1\. Shared Cart URLs**

* **Finding:** There is no evidence of a standardized, public method for creating a pre-filled shopping cart using URL query parameters.
* **Analysis:** Product pages on ah.nl use a path-based internal identifier (e.g., .../product/wi230720/...) for navigation to a single product page.6 This structure is not designed for populating a cart with multiple items or quantities. Direct interaction with the website confirms that adding items to the cart is a dynamic process handled by client-side scripts, with no corresponding changes to the URL.20 This method is  
  **not viable** for the desired user flow.

#### **2\. Official APIs**

* **Finding:** Albert Heijn does not offer a public or documented partner API for third-party e-commerce integration, such as cart creation or checkout.
* **Analysis:** The "Product Data Portal" (pdp.ah.nl) is a restricted B2B portal for suppliers to manage product data, not a developer portal for application integration.21 The public AH Technology GitHub organization hosts repositories related to internal infrastructure (e.g., Kubernetes, Azure), analytics, and mobile development utilities, but contains no projects related to e-commerce transactions, product catalogs, or cart management.1 Access to their core commerce APIs is therefore not possible without a direct, high-level strategic partnership.

#### **3\. Affiliate Programs**

* **Finding:** Albert Heijn manages an official affiliate program through the **Partnerize** network.9
* **Analysis:** This represents the most promising and legitimate pathway for integration. The Partnerize platform provides robust tools for deep linking and mobile app tracking, which are essential for directing users and attributing sales.15 Most importantly, discussions within developer communities and media reports indicate that Albert Heijn provides a "widget to add items to the shopping cart" or a  
  **"buy button"** to external partners, likely through this affiliate program.6 This suggests a mechanism more advanced than a simple deep link, one that could potentially pass product and quantity information to add an item directly to the user's cart. This "buy button" is the key to achieving a significantly improved user experience in an early phase. The immediate next step is to join the Partnerize program to gain access to these tools and analyze their technical implementation.

#### **4\. Reverse Engineering (High Risk)**

* **Finding:** It is technically feasible to interact with Albert Heijn's private mobile and web APIs by reverse-engineering the calls made by their official "Appie" app.
* **Analysis:** Multiple independent developers and open-source projects have successfully documented and interacted with the private AH API. This process involves obtaining an anonymous OAuth bearer token from their authentication endpoint (POST https://api.ah.nl/mobile-auth/v1/auth/token/anonymous) and using it to access services like product search.3 The backend has evolved to use a modern  
  **GraphQL API**, which, while powerful, remains undocumented and subject to unannounced changes.10 Relying on this method for a commercial product is fraught with risk. AH could change endpoints, authentication methods, or data structures at any time, instantly breaking the integration. Furthermore, they may actively monitor for and block unauthorized API traffic.11 Due to these stability and legal risks, this method is  
  **not recommended** for a production system.

### **C. Technical Limitations & Requirements**

* **Product Identifiers:** The primary product identifier used by Albert Heijn is an internal, web-specific ID, often prefixed with wi (e.g., wi230720) found in the product URL.6 A foundational requirement for any integration is a service that can map universal EAN codes to these specific AH identifiers by scraping product pages.
* **Authentication:** The recommended affiliate route relies on Partnerize's click-tracking and cookie-based attribution. The high-risk reverse-engineered route would necessitate managing and refreshing OAuth bearer tokens.
* **Limitations:** The precise capabilities and limitations of the affiliate "buy button" (e.g., maximum number of items, whether it can handle quantity, user login requirements) are currently unknown. These must be determined by joining the Partnerize program and examining the provided tools.

### **D. Recommended Phased Approach for Albert Heijn**

* **Phase 1 (MVP):** Join the Partnerize affiliate program. Build the essential product ID mapping service (EAN to AH wi... ID). Utilize Partnerize's standard deep-linking tools to connect each product in a SuperMarty list to its corresponding page on ah.nl.
* **Phase 2 (Enhancement):** Once approved for the affiliate program, access and implement the "buy button" functionality.6 This will allow for a one-click action to add a specific product (and potentially quantity) to the user's cart on the AH website, significantly streamlining the user journey.
* **Phase 3 (Deep Integration):** With a successful affiliate partnership established, leverage this relationship to open a strategic dialogue with AH Technology. The goal is to negotiate a formal API partnership, seeking documented access to their private GraphQL API for direct, multi-item cart creation.

### **Table: Albert Heijn Integration Methods \- Feasibility vs. Risk Analysis**

| Integration Method | Technical Feasibility | Stability & Legal Risk | Recommendation |
| :---- | :---- | :---- | :---- |
| Shared Cart URL | Low | Low | Not Recommended |
| Official API | Low (without partnership) | Low | Pursue via Partnership (Phase 3\) |
| Affiliate Program (Partnerize) | High | Low | **Recommended (Phases 1 & 2\)** |
| Reverse Engineering | High | High | Not Recommended |

---

## **III. Jumbo: Integration Deep Dive**

### **A. Technical Ecosystem Overview**

Jumbo Supermarkten is a major player in the Dutch market, extending its customer-centric "7 Zekerheden" (7 Certainties) promise to its online shopping experience.26 From a technical standpoint, Jumbo's mobile services are powered by a modern

**GraphQL API**, a fact confirmed by independent developers who have interacted with it.6 The open-source

SupermarktConnector project successfully utilizes this mobile API to retrieve detailed product data, demonstrating its functionality.5 However, Jumbo's developer portal (

idp-static.dev.cloud.jumbo.com) is explicitly labeled as "Internal" and is secured with Okta authentication, making it clear that their infrastructure is not intended for public or third-party developer access.2

### **B. Analysis of Integration Pathways**

#### **1\. Shared Cart URLs**

* **Finding:** There is no evidence of a shared cart URL functionality for Jumbo's e-commerce platform.
* **Analysis:** Manual inspection of the jumbo.com website and its network traffic during the shopping process shows that adding items to the cart is handled dynamically via API calls made by frontend JavaScript. The browser URL does not change to reflect the cart's contents with product IDs or quantities.27 This method is  
  **not viable**.

#### **2\. Official APIs**

* **Finding:** Jumbo does not provide a public or partner-facing API for e-commerce integration.
* **Analysis:** The developer portal is strictly internal.2 Public searches for a "Jumbo API" yield numerous results for unaffiliated companies with similar names (e.g., Jumio identity verification, Jumbonline travel API), but nothing related to the supermarket chain.28 This path is a  
  **dead end** without securing a direct, formal partnership.

#### **3\. Affiliate Programs**

* **Finding:** Jumbo operates an official affiliate program in the Netherlands through the **Tradetracker** affiliate network.7
* **Analysis:** This stands out as the only viable and legitimate pathway for an initial integration. The program details a 4% commission on sales with a 7-day cookie duration, providing a clear business model.7 The Tradetracker platform provides essential tools for partners, including  
  **deep linking**, which allows SuperMarty to generate tracked URLs that send users directly to specific product pages on jumbo.com.14 While Tradetracker offers an API, its documentation suggests it is primarily for reporting and campaign management, not for direct e-commerce actions like cart manipulation.14 This makes the affiliate program a solid foundation for an MVP.

#### **4\. Reverse Engineering (High Risk)**

* **Finding:** It is technically possible to interact with Jumbo's private GraphQL API.
* **Analysis:** The success of the SupermarktConnector project in retrieving product data confirms the existence and functionality of the private API.5 Developer forums corroborate that it is a GraphQL API that can be explored using a network inspector.6 However, this approach carries an explicit and significant risk. A user claiming to have inside knowledge from Jumbo's hosting provider stated unequivocally that the APIs are not public and that unauthorized scraping or API usage will result in the user's IP address being blocked.11 This direct warning makes the reverse-engineering route  
  **unacceptably risky and unreliable** for a commercial application.

### **C. Technical Limitations & Requirements**

* **Product Identifiers:** The SupermarktConnector project reveals that Jumbo uses an internal alphanumeric product ID (e.g., "70942PAK") for its items.5 A mapping service to translate EANs to these Jumbo-specific IDs is a critical prerequisite.
* **Authentication:** The affiliate route will use Tradetracker's standard linking and tracking mechanisms. The high-risk reverse-engineered path would require intercepting and managing authentication tokens from the mobile app's private login flow.
* **Limitations:** The Tradetracker affiliate program appears limited to deep linking and does not offer a more advanced "buy button" or multi-item cart creation tool out of the box. The most significant limitation of the alternative path is the high probability of being actively blocked by Jumbo's security measures.11

### **D. Recommended Phased Approach for Jumbo**

* **Phase 1 (MVP):** Join the Tradetracker affiliate program for Jumbo. Build the necessary product ID mapping service. Implement Tradetracker's deep linking tools to send users from a product in SuperMarty to the corresponding product page on jumbo.com.
* **Phase 2 (Enhancement):** Leverage the formal affiliate partnership to engage with the assigned Tradetracker account manager. Inquire about more advanced integration options, such as the possibility of a pre-filled cart link, which may be an unadvertised feature available to key partners.
* **Phase 3 (Deep Integration):** After demonstrating value through the affiliate program, propose a formal technical partnership directly with Jumbo. The goal is to gain documented, sanctioned access to their GraphQL API to enable a seamless, multi-item cart transfer.

### **Table: Jumbo Integration Methods \- Feasibility vs. Risk Analysis**

| Integration Method | Technical Feasibility | Stability & Legal Risk | Recommendation |
| :---- | :---- | :---- | :---- |
| Shared Cart URL | Low | Low | Not Recommended |
| Official API | Low (without partnership) | Low | Pursue via Partnership (Phase 3\) |
| Affiliate Program (Tradetracker) | High | Low | **Recommended (Phases 1 & 2\)** |
| Reverse Engineering | High | Very High | Not Recommended |

---

## **IV. Plus Supermarkets: Integration Deep Dive**

### **A. Technical Ecosystem Overview**

Of the three supermarkets analyzed, PLUS presents the most modern and integration-friendly technical architecture. Their entire online e-commerce platform is built using **Commercetools**, a leading "composable commerce" provider known for its headless, API-first approach.12 A case study on the implementation explicitly highlights the platform's "outstanding API response time" for crucial e-commerce functions, including

**"adding products to the basket, applying discounts and calculating the total order amount in real-time"**.12 This is a direct confirmation that robust, high-performance APIs for cart management are not just an add-on but are the core foundation of their digital infrastructure.

### **B. Analysis of Integration Pathways**

#### **1\. Shared Cart URLs (Hypothesized)**

* **Finding:** While no specific shared cart URL format for PLUS is documented in the research, modern e-commerce platforms that share architectural principles with Commercetools, such as Shopify, offer this functionality as a standard feature.
* **Analysis:** Platforms like Shopify commonly use a URL structure like .../cart/{variant\_id}:{quantity},{variant\_id\_2}:{quantity\_2} to allow for the creation of pre-filled shopping carts via a single link.34 Given that PLUS is built on an API-first platform, it is highly probable that it supports a similar URL-based cart creation method. This is a strong hypothesis that should be the first avenue of technical exploration, as it could provide a superior user experience from the outset. This method is considered  
  **potentially highly viable**.

#### **2\. Official APIs**

* **Finding:** The core of the PLUS e-commerce operation is built on the Commercetools API.12
* **Analysis:** This is the most significant finding for any of the targets. Unlike Albert Heijn and Jumbo, whose APIs are private and proprietary, the core functionality of the PLUS website is *designed* to be driven by an API. While gaining access to this API would still require a formal partnership and credentials, the technical foundation is not only present but is the central pillar of their system. This makes a deep, reliable, and fully seamless integration **technically very feasible** and the ultimate strategic goal for this partnership.

#### **3\. Affiliate Programs**

* **Finding:** PLUS operates an official affiliate program, which is managed by the agency **FamilyBlend** and runs on the **Awin** affiliate network.8
* **Analysis:** This provides a clear, legitimate, and professional "front door" for establishing a partnership. The Awin network offers a standard suite of tools, including deep link builders, product-level commission capabilities, and robust tracking and reporting.16 This serves as an excellent starting point for an MVP and, crucially, establishes a formal line of communication with PLUS's digital marketing partners at FamilyBlend.

#### **4\. Reverse Engineering (High Risk)**

* **Finding:** While technically possible, it is strategically unnecessary and counterproductive.
* **Analysis:** Given the modern, API-first architecture of the Commercetools backend and the existence of an official, professionally managed affiliate program, there is no strategic incentive to pursue a high-risk, unstable reverse-engineering path. The legitimate channels for partnership and integration are far more promising and align with a long-term, stable business relationship. This method is **not recommended**.

### **C. Technical Limitations & Requirements**

* **Product Identifiers:** The specific product ID format used by PLUS within their Commercetools instance is not detailed in the research. It is likely to be an internal SKU or a unique ID generated by the platform. Standard industry codes like EAN for packaged goods and PLU for fresh produce will also be relevant.38 A product ID mapping service is a critical prerequisite for any integration.
* **Authentication:** The affiliate route will use Awin's standard tracking mechanisms. A direct API integration would use an OAuth or similar token-based authentication system provided by PLUS under a formal partnership agreement.
* **Limitations:** The primary limitation is access. The first step is to contact FamilyBlend to join the Awin affiliate program.8 The success of a deep integration (Phase 3\) is entirely dependent on securing a technical partnership that grants API credentials for their Commercetools instance.

### **D. Recommended Phased Approach for PLUS**

* **Phase 1 (MVP):** Immediately contact FamilyBlend to begin the process of joining the Awin affiliate program for PLUS. In parallel, dedicate technical resources to testing the hypothesis of a shared cart URL format (e.g., plus.nl/cart/PRODUCT\_ID:QUANTITY). If the URL method is successful, implement it as the MVP, as it provides a superior user experience. If not, use Awin's standard deep linking as the fallback MVP.
* **Phase 2 (Enhancement):** If the MVP was limited to deep-linking, the enhancement goal is to work with FamilyBlend and PLUS to enable a shared cart URL. If the shared cart URL was functional from the start, this phase should focus on optimizing the process and using the affiliate partnership data to build the business case for a deeper API integration.
* **Phase 3 (Deep Integration):** This is the primary strategic goal for the PLUS partnership. Leverage the affiliate relationship and performance data to engage in discussions about a direct API integration with their Commercetools backend. The objective is to obtain API keys to use their cart and checkout APIs for a truly seamless, multi-item, server-to-server transfer.

### **Table: PLUS Integration Methods \- Feasibility vs. Risk Analysis**

| Integration Method | Technical Feasibility | Stability & Legal Risk | Recommendation |
| :---- | :---- | :---- | :---- |
| Shared Cart URL (Hypothesized) | High | Low | **Recommended (Test for Phase 1\)** |
| Official API (Commercetools) | High (with partnership) | Low | **Recommended (Phase 3 Goal)** |
| Affiliate Program (Awin) | High | Low | **Recommended (Phase 1 Entry)** |
| Reverse Engineering | Medium | High | Not Recommended |

---

## **V. Strategic Recommendations & Detailed Next Steps**

### **A. Cross-Platform Technical Prerequisites**

Successful integration with any of the target supermarkets hinges on two foundational technical components that must be developed internally.

* **Product Identifier Mapping Service:** This is the most critical prerequisite. A robust internal service must be built to map universal product identifiers, such as EANs, to the proprietary internal product IDs used by Albert Heijn (wi...), Jumbo (...PAK), and PLUS. This will likely require scraping product pages to extract these IDs and storing the mappings in a database. This service is the foundational block upon which all other integration work depends.
* **Affiliate Link Generation Module:** A centralized software module is required to construct correctly formatted and tracked affiliate links for each of the three different networks: Partnerize (for AH), Tradetracker (for Jumbo), and Awin (for PLUS). This module must handle the unique URL structures and tracking parameters of each network.

### **B. Detailed Phased Implementation Plan**

#### **Phase 1 (MVP \- Universal Deep Linking)**

* **Actions:**
    1. Initiate the application process for all three affiliate programs: Albert Heijn via Partnerize, Jumbo via Tradetracker, and PLUS via Awin/FamilyBlend.
    2. Begin development and deployment of the core Product Identifier Mapping Service.
    3. Develop and integrate the Affiliate Link Generation Module.
    4. For PLUS, concurrently test the hypothesized shared cart URL.
* **User Experience:** The user compiles a shopping bag in SuperMarty. Upon clicking "Checkout at," they are presented with a list of their chosen items. Each item in this list is a tracked deep link. Clicking an item opens the corresponding product page on the supermarket's website in a new tab. The user must then manually add each item to the supermarket's cart. This provides basic functionality and establishes the partnership.

#### **Phase 2 (Enhancement \- Pre-filled Carts)**

* **Actions:**
    1. **Albert Heijn:** Upon acceptance into the Partnerize program, investigate and implement the "buy button" functionality to enable one-click adding of items to the AH cart.6
    2. **PLUS:** If the shared cart URL test in Phase 1 was successful, this phase is complete. If not, work through the Awin/FamilyBlend partnership to request or discover a method for creating a pre-filled cart.
    3. **Jumbo:** Engage the assigned Tradetracker account manager to explore possibilities for a pre-filled cart link. This may be an unadvertised feature available to high-value partners.
* **User Experience:** A significant improvement. The user compiles their bag in SuperMarty and clicks "Checkout at." They are redirected to the supermarket's website or app with their entire shopping cart pre-filled and ready for the final checkout steps.

#### **Phase 3 (Deep Integration \- API Access)**

* **Actions:**
    1. **PLUS:** Prioritize a formal partnership pitch to PLUS and their agency, FamilyBlend. The goal is to gain documented API access to their Commercetools platform for direct, server-to-server cart creation. The pitch should be supported by affiliate sales data gathered in previous phases.
    2. **Albert Heijn & Jumbo:** After establishing successful affiliate relationships, initiate high-level partnership discussions with their respective e-commerce, business development, or technology departments. The goal is to make a compelling business case for gaining access to their private GraphQL APIs.
* **User Experience:** The ultimate seamless flow. The user clicks "Checkout at" in the SuperMarty app. SuperMarty makes a direct, server-to-server API call to the supermarket's backend, creating the shopping cart. The user is then redirected straight to the final checkout page, with their cart filled and ready for payment.

### **C. Actionable Next Steps**

* **Immediate (Week 1):**
    * Assign engineering resources to begin architecture and development of the Product Identifier Mapping Service.
    * Designate a business development lead to begin the application process for the Partnerize, Tradetracker, and Awin affiliate programs. Draft initial outreach communications to the relevant contacts.
* **Next (Weeks 2-4):**
    * As access to each affiliate network is granted, begin technical investigation of their respective platforms, focusing on their link generation tools, APIs for deep linking, and any available documentation.
    * Begin prototyping the Affiliate Link Generation Module.
* **Contingency Planning:**
    * In the event that affiliate program applications are rejected, the backup strategy is to re-evaluate the risks and rewards of a limited, non-production Proof of Concept (PoC) using the reverse-engineered API paths. This PoC would not be for public release but could serve as a powerful demonstration tool to use as leverage in renewed partnership discussions.

---

## **VI. Appendix**

### **A. Summary of Unofficial API Endpoints (For Informational Purposes Only)**

The following table summarizes API endpoints discovered through analysis of open-source projects and community discussions. These are private, undocumented APIs. **Use of these endpoints in a production environment is not recommended due to high instability and legal risks.**

| Supermarket | Endpoint & Method | Description | Required Headers / Body | Source |
| :---- | :---- | :---- | :---- | :---- |
| Albert Heijn | POST https://api.ah.nl/mobile-auth/v1/auth/token/anonymous | Obtains an anonymous bearer token for guest sessions. | Content-Type: application/json, Body: { "clientId": "appie" } | 4 |
| Albert Heijn | GET https://api.ah.nl/mobile-services/product/search/v2 | Searches for products using a query string. | Authorization: Bearer \<token\>, User-Agent: Appie/8.22.3 | 4 |
| Albert Heijn | GraphQL Endpoint | The albert-heijn-wrapper library indicates the new API is GraphQL. Specific queries (e.g., for adding to cart) are not documented. | Authorization: Bearer \<token\> | 13 |
| Jumbo | GraphQL Endpoint | Mobile app uses a GraphQL API. Specific queries must be discovered via network inspection. | Requires authentication token. | 6 |

### **B. Comparative Table of Affiliate Programs**

| Supermarket | Affiliate Network | Management/Contact | Commission Rate | Cookie Duration | Key Features | Source |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| **Albert Heijn** | Partnerize | Direct / Partnerize | Not Publicly Listed | Not Publicly Listed | Deep Linking, Mobile Tracking, "Buy Button" (reported) | 6 |
| **Jumbo** | Tradetracker | Tradetracker | 4.00% | 7 days | Deep Linking, Product Feeds, Reporting API | 7 |
| **PLUS** | Awin | FamilyBlend (Agency) | Not Publicly Listed | Not Publicly Listed | Deep Linking, Product-level Commissioning, QR Codes | 8 |

#### **Works cited**

1. AH Technology · GitHub, accessed June 17, 2025, [https://github.com/albert-heijn-technology](https://github.com/albert-heijn-technology)
2. Jumbo Internal Developer Portal, accessed June 17, 2025, [https://idp-static.dev.cloud.jumbo.com/](https://idp-static.dev.cloud.jumbo.com/)
3. Albert Heijn Plugin (alternative for OpenFoodFacts) \- grocy \- Reddit, accessed June 17, 2025, [https://www.reddit.com/r/grocy/comments/1jc2yn2/albert\_heijn\_plugin\_alternative\_for\_openfoodfacts/](https://www.reddit.com/r/grocy/comments/1jc2yn2/albert_heijn_plugin_alternative_for_openfoodfacts/)
4. Interact with the Albert Heijn mobile app API to retrieve receipt data, and other things, accessed June 17, 2025, [https://gist.github.com/jabbink/8bfa44bdfc535d696b340c46d228fdd1](https://gist.github.com/jabbink/8bfa44bdfc535d696b340c46d228fdd1)
5. bartmachielsen/SupermarktConnector: Collecting product ... \- GitHub, accessed June 17, 2025, [https://github.com/bartmachielsen/SupermarktConnector](https://github.com/bartmachielsen/SupermarktConnector)
6. Albert Heijn Winkelmand API : r/appiememes \- Reddit, accessed June 17, 2025, [https://www.reddit.com/r/appiememes/comments/18wlhdt/albert\_heijn\_winkelmand\_api/](https://www.reddit.com/r/appiememes/comments/18wlhdt/albert_heijn_winkelmand_api/)
7. affiliate-net.nl, accessed June 17, 2025, [https://affiliate-net.nl/programmas/jumbo/\#:\~:text=Jumbo.com%20heeft%20een%20affiliate,Tradetracker%20zijn%20hieronder%20te%20vinden.](https://affiliate-net.nl/programmas/jumbo/#:~:text=Jumbo.com%20heeft%20een%20affiliate,Tradetracker%20zijn%20hieronder%20te%20vinden.)
8. Affiliate programma \- PLUS.nl, accessed June 17, 2025, [https://www.plus.nl/organisatie/affiliate](https://www.plus.nl/organisatie/affiliate)
9. Cookiebeleid | Albert Heijn, accessed June 17, 2025, [https://www.ah.nl/cookiebeleid](https://www.ah.nl/cookiebeleid)
10. Tweaker maakt 'Dash'-knop om wasmiddel op digitale boodschappenlijst te zetten \- IT Pro, accessed June 17, 2025, [https://tweakers.net/geek/107913/tweaker-maakt-dash-knop-om-wasmiddel-op-digitale-boodschappenlijst-te-zetten.html](https://tweakers.net/geek/107913/tweaker-maakt-dash-knop-om-wasmiddel-op-digitale-boodschappenlijst-te-zetten.html)
11. supermarkt API's gebruiken, is het legaal : r/appiememes \- Reddit, accessed June 17, 2025, [https://www.reddit.com/r/appiememes/comments/1fwnlmb/supermarkt\_apis\_gebruiken\_is\_het\_legaal/](https://www.reddit.com/r/appiememes/comments/1fwnlmb/supermarkt_apis_gebruiken_is_het_legaal/)
12. PLUS Supermarkets Customer Story \- Commercetools, accessed June 17, 2025, [https://commercetools.com/customer-stories/plus-supermarkets](https://commercetools.com/customer-stories/plus-supermarkets)
13. albert-heijn-wrapper | Yarn, accessed June 17, 2025, [https://classic.yarnpkg.com/en/package/albert-heijn-wrapper](https://classic.yarnpkg.com/en/package/albert-heijn-wrapper)
14. Publisher | Affiliate Marketing \- TradeTracker.com, accessed June 17, 2025, [https://tradetracker.com/gb/publishers/](https://tradetracker.com/gb/publishers/)
15. For Affiliates \- Partnerize, accessed June 17, 2025, [https://partnerize.com/partners/affiliates](https://partnerize.com/partners/affiliates)
16. How can I use Link Builder to create deep links? \- Partner Success Center \- Awin, accessed June 17, 2025, [https://success.awin.com/s/article/How-can-I-use-Link-Builder-to-create-Deep-Links](https://success.awin.com/s/article/How-can-I-use-Link-Builder-to-create-Deep-Links)
17. Senior Backend Developer (Kotlin, Microservices, Kafka) | Ahold Delhaize, accessed June 17, 2025, [https://careers.aholddelhaize.com/vacancy/2318/senior-backend-developer-kotlin-microservices-kafka](https://careers.aholddelhaize.com/vacancy/2318/senior-backend-developer-kotlin-microservices-kafka)
18. Albert Heijn & MongoDB: Making Digital Receipts A Reality, accessed June 17, 2025, [https://www.mongodb.com/solutions/customer-case-studies/albert-heijn](https://www.mongodb.com/solutions/customer-case-studies/albert-heijn)
19. €30 worth of groceries from Albert Heijn : r/Netherlands \- Reddit, accessed June 17, 2025, [https://www.reddit.com/r/Netherlands/comments/16rvaxb/30\_worth\_of\_groceries\_from\_albert\_heijn/](https://www.reddit.com/r/Netherlands/comments/16rvaxb/30_worth_of_groceries_from_albert_heijn/)
20. Albert Heijn: boodschappen doen bij de grootste supermarkt, accessed June 17, 2025, [https://www.ah.nl/](https://www.ah.nl/)
21. Log In, accessed June 17, 2025, [https://pdp.ah.nl/](https://pdp.ah.nl/)
22. Affiliate marketing: 8 manieren om er geld mee te verdienen \- Bloggen en loggen, accessed June 17, 2025, [https://www.bloggenenloggen.nl/affiliate-marketing/](https://www.bloggenenloggen.nl/affiliate-marketing/)
23. Announcing Our Enhanced App Tracking Capabilities For Partner Marketing, accessed June 17, 2025, [https://partnerize.com/resources/blog/announcing-our-enhanced-app-tracking-capabilities-for-partner-marketing](https://partnerize.com/resources/blog/announcing-our-enhanced-app-tracking-capabilities-for-partner-marketing)
24. Omnichannel Best Practice at Scale: Across 1000 Stores and Online \- Brand Experts, accessed June 17, 2025, [https://www.brand-experts.com/best-practices/omnichannel-best-practice-at-scale/](https://www.brand-experts.com/best-practices/omnichannel-best-practice-at-scale/)
25. Interact with the Albert Heijn mobile app API to retrieve receipt data, and other things, accessed June 17, 2025, [https://gist.github.com/jabbink/8bfa44bdfc535d696b340c46d228fdd1?permalink\_comment\_id=5106051](https://gist.github.com/jabbink/8bfa44bdfc535d696b340c46d228fdd1?permalink_comment_id=5106051)
26. Jumbo.com affiliate programma, accessed June 17, 2025, [https://affiliate-net.nl/programmas/jumbo/](https://affiliate-net.nl/programmas/jumbo/)
27. Jumbo: Altijd lage prijzen op je dagelijkse boodschappen, accessed June 17, 2025, [https://www.jumbo.com/](https://www.jumbo.com/)
28. Jumio: Leading AI-Powered Identity Verification Platform, accessed June 17, 2025, [https://www.jumio.com/](https://www.jumio.com/)
29. JUMBO | Postman API Network, accessed June 17, 2025, [https://www.postman.com/telecoms-specialist-23383689/jumbo/overview](https://www.postman.com/telecoms-specialist-23383689/jumbo/overview)
30. Jumbonline.com, accessed June 17, 2025, [https://www.jumbonline.com/](https://www.jumbonline.com/)
31. Jumbo.com Affiliate programma \- LinkPizza, accessed June 17, 2025, [https://linkpizza.com/nl/app/affiliate-program/jumbo.com](https://linkpizza.com/nl/app/affiliate-program/jumbo.com)
32. Advertisers | Affiliate Marketing \- TradeTracker.com, accessed June 17, 2025, [https://tradetracker.com/us/advertisers/](https://tradetracker.com/us/advertisers/)
33. TradeTracker Merchant API Reference \- CData Virtuality Documentation, accessed June 17, 2025, [https://docs.datavirtuality.com/connectors/tradetracker-merchant-api-reference](https://docs.datavirtuality.com/connectors/tradetracker-merchant-api-reference)
34. Cart permalinks \- Shopify Help Center, accessed June 17, 2025, [https://help.shopify.com/en/manual/checkout-settings/cart-permalink](https://help.shopify.com/en/manual/checkout-settings/cart-permalink)
35. Shopify Pre-filled Cart Guide: Strategies & Permalinks \- Checkout Links, accessed June 17, 2025, [https://checkoutlinks.com/blog/shopify-pre-filled-cart-guide-strategies-and-permalinks/](https://checkoutlinks.com/blog/shopify-pre-filled-cart-guide-strategies-and-permalinks/)
36. Create cart permalinks \- Shopify.dev, accessed June 17, 2025, [https://shopify.dev/docs/apps/build/checkout/create-cart-permalinks](https://shopify.dev/docs/apps/build/checkout/create-cart-permalinks)
37. The Affiliate Marketing Platform For Advertisers \- Awin, accessed June 17, 2025, [https://www.awin.com/us/advertisers](https://www.awin.com/us/advertisers)
38. Price look-up code \- Wikipedia, accessed June 17, 2025, [https://en.wikipedia.org/wiki/Price\_look-up\_code](https://en.wikipedia.org/wiki/Price_look-up_code)
39. Tips for Marketing Fresh Produce to Retail Grocers: Using PLU and UPC Codes, accessed June 17, 2025, [https://www.cefs.ncsu.edu/ncgt/NCGT-Tips-for-Producers-on-PLU-and-UPC-Codes-Nov-2013.pdf](https://www.cefs.ncsu.edu/ncgt/NCGT-Tips-for-Producers-on-PLU-and-UPC-Codes-Nov-2013.pdf)
