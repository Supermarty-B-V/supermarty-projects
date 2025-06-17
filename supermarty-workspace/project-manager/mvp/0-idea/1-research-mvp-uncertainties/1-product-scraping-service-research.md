# 📝 Research Prompt: Product Scraping Service

**Role:** You are a **Data Scraping & Aggregation Expert**.

**Objective:**
Your goal is to research and recommend the optimal solution for scraping product data from major EU supermarket websites, starting with Albert Heijn, Jumbo, and Plus in the Netherlands. The solution must be robust, scalable, and legally compliant.

**Context:**
We are building a grocery shopping assistant app (SuperMarty) using Flutter and Supabase. A core feature is providing users with accurate, up-to-date product information, including prices, offers, and nutritional values. The scraping strategy is to perform an initial bulk scrape and then update data on-demand with a caching layer (refreshing once per day).

**Key Research Questions:**

1.  **Build vs. Buy Analysis:**
    *   **Build (Custom Solution):** What are the pros and cons of building a custom scraping solution using frameworks like Python/Scrapy?
        *   What are the estimated development and maintenance costs?
        *   What technical infrastructure is required (e.g., proxy services, server management)?
        *   How can we handle anti-scraping measures (e.g., CAPTCHAs, IP blocking)?
    *   **Buy (Third-Party API):** What are the leading third-party scraping APIs or data-as-a-service providers for EU supermarket data?
        *   Provide a comparison of the top 3-5 services based on:
            *   **Coverage:** Do they support Albert Heijn, Jumbo, and Plus?
            *   **Data Accuracy & Freshness:** How reliable is their data on prices, offers, and nutritional info?
            *   **Pricing Model:** What are the costs (e.g., per call, monthly subscription)?
            *   **API Quality:** How is the documentation, rate limiting, and support?
            *   **Legal Compliance:** How do they handle the legal aspects of web scraping?

2.  **Technical Architecture Recommendation:**
    *   Based on the analysis, recommend an architecture for an on-demand scraping service with a robust caching layer (e.g., using Redis, Cloudflare, or Supabase's capabilities).
    *   Outline the key components and data flow.

3.  **Legal & Ethical Considerations:**
    *   What are the primary legal risks associated with scraping these specific supermarket websites in the EU (e.g., copyright, database rights, terms of service violations)?
    *   What are the best practices to minimize these risks?

**Deliverable:**
A detailed report summarizing your findings, including a clear recommendation for the best path forward (build, buy, or a hybrid approach) with justifications based on cost, reliability, scalability, and legal risk.

---
**[Please add research results below this line]**

<template>
# 🔍 Research: {topic}

> Systematic research investigation into {topic/question} examining {scope_areas}. Documents findings, analysis, and actionable recommendations to support evidence-based decision making for {purpose/decision}.

🔐 **Research Methodology Supported:** Literature review, prototyping, data analysis, user interviews, surveys, competitive analysis, and expert consultation with clear deliverables and next steps.
## 🎯 1. Research Objective
> 💡 *What is the primary goal of this research? What specific question(s) are we trying to answer, or what problem are we trying to solve through this investigation? Be clear and concise.*

[Clearly state the research objective(s) here.]

## 🤔 2. Background & Context
> 💡 *Why is this research needed now? Provide any relevant background information, links to existing discussions, related tickets, or current system limitations that necessitate this research. What is the current understanding or hypothesis, if any?*

*   **Reason for Research:** [e.g., Exploring feasibility of a new feature, Investigating a recurring technical issue, Choosing a technology for X, Understanding user needs for Y, Planning a major refactor]
*   **Current Situation/Problem:** [Brief description]
*   **Relevant Links/Tickets:**
    *   `[Link to related issue/document 1]`
    *   `[Link to related issue/document 2]`
*   **Initial Hypothesis (if any):**

## 🗺️ 3. Scope of Research
> 💡 *Define the boundaries of this research. What specific areas should be investigated? What is explicitly out of scope?*

### In Scope:
> 💡 *List the key areas, questions, or topics to be covered.*
*   `[Specific question/area 1 to investigate]`
*   `[Specific question/area 2 to investigate]`
*   `[e.g., Comparison of technology A vs. B for use case X]`
*   `[e.g., Analysis of user feedback regarding problem Y]`
*   `[e.g., Identification of best practices for Z]`

### Out of Scope:
> 💡 *List anything that should NOT be part of this research to maintain focus.*
*   `[e.g., Full implementation of a solution (PoC might be in scope, but not production code)]`
*   `[e.g., Research into unrelated topic A]`

## 🛠️ 4. Proposed Research Methodology
> 💡 *How should this research be conducted? Suggest specific methods, tools, or resources to be used. This can be refined by the assignee.*

*   **Methods:** [e.g., Literature review, Competitive analysis, Technical spike/Prototyping, User interviews (specify number/type if known), Survey, Data analysis of existing logs, Expert consultation (internal/external)]
*   **Tools:** [e.g., Specific search engines, Databases, Analytics platforms, Survey tools, Prototyping software]
*   **Key Information Sources:** [e.g., Academic papers, Industry reports, Competitor websites, Internal documentation, Specific experts to consult]

## 📦 5. Expected Deliverables
> 💡 *What tangible outputs are expected from this research? How should the findings be presented?*

*   [ ] **Summary Document:** A written report summarizing findings, analysis, and recommendations.
    *   *Format:* `[e.g., Markdown in this ticket, Google Doc, Confluence page]`
*   [ ] **Presentation:** (Optional) A slide deck for presenting findings to the team.
*   [ ] **Proof of Concept (PoC):** (If applicable) Code for a small prototype demonstrating feasibility.
    *   *Repository/Branch:* `[Link]`
*   [ ] **List of Pros & Cons:** For different options investigated.
*   [ ] **Recommendations:** Clear, actionable recommendations based on the research.
*   [ ] **Other:** `[Specify other deliverables]`

## ⏳ 6. Timeline & Effort (Optional)
> 💡 *Provide an estimated timeframe or effort for completing this research. This is a rough guideline.*

*   **Requested Completion Date:** `[YYYY-MM-DD]`
*   **Estimated Effort:** `[e.g., X hours, Y story points]`

**(To be filled in by the assignee during and after research)**

## 🔑 7. Key Findings
> 💡 *Document the main facts, data points, and observations gathered during the research. Be objective and cite sources where applicable.*

*   **Finding 1:** [Detailed finding]
    *   *Source/Evidence:* `[Link or reference]`
*   **Finding 2:** [Detailed finding]
    *   *Source/Evidence:* `[Link or reference]`
*   *(Add more findings as needed)*

## 📊 8. Analysis & Synthesis
> 💡 *Interpret the key findings. What do they mean in the context of the research objective? Identify patterns, trends, comparisons, and insights.*

[Your analysis and synthesis of the findings. How do the pieces of information connect?]

## ⭐ 9. Recommendations
> 💡 *Based on the findings and analysis, what are the specific, actionable recommendations? If comparing options, clearly state the recommended option and why.*

*   **Recommendation 1:** [Specific recommendation]
    *   *Justification:* [Why this is recommended based on the research]
*   **Recommendation 2:** [Specific recommendation]
    *   *Justification:* [Why this is recommended based on the research]
*   *(If applicable) **Chosen Option:** [If multiple options were evaluated, state the preferred one.]*

## 🚀 10. Next Steps (Post-Research)
> 💡 *What are the suggested next actions based on the research recommendations? This could involve creating new tickets, scheduling discussions, or proceeding with a specific plan.*

*   `[Actionable next step 1, e.g., Create user story for feature X based on recommendation Y]`
*   `[Actionable next step 2, e.g., Schedule a team meeting to discuss findings and decide on Z]`
*   `[Actionable next step 3, e.g., Begin PoC development for chosen technology A]`

## 🔗 11. Resources & Links Discovered
> 💡 *List any valuable articles, tools, repositories, or other resources discovered during the research that might be useful for future reference.*

*   `[Link 1: Description]`
*   `[Link 2: Description]`
*   `[Link 3: Description]`
    </template>
