# 📝 Research Prompt: Supermarket Checkout Integration

**Role:** You are a **Technical Integration & API Research Expert**.

**Objective:**
Your goal is to investigate and report on the technical feasibility of integrating the SuperMarty shopping bag with the checkout processes of major EU supermarkets, starting with Albert Heijn, Jumbo, and Plus in the Netherlands.

**Context:**
A key user flow in our SuperMarty app is allowing a user to compile a shopping bag and then seamlessly transfer that bag to their chosen supermarket's website or app to complete the purchase. We plan to implement this progressively, starting with the simplest methods and moving towards deeper integration where possible.

**Key Research Questions:**

1.  **Integration Methods Analysis:**
    *   For each target supermarket (Albert Heijn, Jumbo, Plus), investigate the availability and viability of the following integration methods:
        *   **Shared Cart URLs:** Do they support creating a shopping list via a URL with query parameters (e.g., `?product_id=123&qty=2`)? If so, what is the exact format and what product identifiers are used?
        *   **Official APIs:** Do they offer public or partner APIs for cart creation or checkout? What are the requirements to gain access?
        *   **Affiliate Programs:** Do they have affiliate programs that provide tools or links for this purpose?
        *   **Reverse Engineering (High Risk):** Is it technically possible (though legally risky) to simulate adding items to a cart via their web interface? (Note: This is for informational purposes to understand the landscape, not as a primary recommendation).

2.  **Technical Limitations & Requirements:**
    *   For each available method, what are the technical limitations? (e.g., maximum number of items, requirement for the user to be logged in, identifier mapping challenges).
    *   What product identifiers (e.g., internal ID, SKU, EAN) are used by each supermarket for their integration methods? How does this align with the data we can get from our scraping service?

3.  **Progressive Implementation Roadmap:**
    *   Based on your findings, propose a phased roadmap for checkout integration.
        *   **Phase 1 (MVP):** What is the simplest, most reliable method we can implement for each supermarket right now (e.g., redirecting to the homepage with a list, or using a shared URL)?
        *   **Phase 2 (Enhancement):** What would be the next logical step to improve the experience (e.g., moving from a simple redirect to a pre-filled cart)?
        *   **Phase 3 (Deep Integration):** What would a full API-based integration look like, and what would be required to achieve it (e.g., partnerships)?

**Deliverable:**
A detailed report organized by supermarket (Albert Heijn, Jumbo, Plus). For each, document the available integration methods, their technical requirements and limitations, and provide a clear, actionable recommendation for a phased implementation approach.

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
