# 📝 Research Prompt: Product Matching Algorithm

**Role:** You are an **AI & Machine Learning Expert** with a focus on data science and natural language processing (NLP).

**Objective:**
Your goal is to research and propose a robust strategy for accurately matching equivalent products from different supermarket websites. This is a critical component for our price comparison feature.

**Context:**
Our application, SuperMarty, needs to present a unified "shadow product" to the user. For example, "Albert Heijn Halfvolle Melk 1L" and "Jumbo Halfvolle Melk 1L" should both be linked to a single "SuperMarty Halfvolle Melk 1L" entity. The matching must be highly accurate to ensure fair price comparisons. The system should also allow for manual correction by an admin.

**Key Research Questions:**

1.  **Matching Strategies Analysis:**
    *   Analyze the feasibility, pros, and cons of the following matching techniques for this specific use case:
        *   **Identifier-Based:** Using EAN (European Article Number) or other barcode standards. How reliable is the availability of this data from scrapers?
        *   **Text-Based (NLP):** Using product titles, descriptions, and attributes. What NLP models (e.g., TF-IDF, word embeddings like Word2Vec/GloVe, transformer models like BERT) are best suited for this? How do we handle variations in naming, branding, and units?
        *   **Image-Based:** Using computer vision to compare product images. Is this viable given the quality and consistency of images from supermarket websites?
        *   **Hybrid Models:** Propose a hybrid approach that combines multiple techniques (e.g., EAN as a primary key, with NLP and other attributes as a fallback).

2.  **Algorithm Recommendation & Design:**
    *   Recommend a specific algorithm or a hybrid model that provides the best balance of accuracy, scalability, and development effort.
    *   Outline a high-level design for this matching pipeline. How would it process new products from the scraping service?
    *   How should the algorithm generate a confidence score for each match?

3.  **Handling Mismatches & Manual Override:**
    *   How should the system flag low-confidence matches for admin review?
    *   Propose a workflow for how an admin can efficiently review, confirm, or correct automated matches. How does the system learn from these corrections to improve future performance?

**Deliverable:**
A detailed report outlining the different matching strategies, a clear recommendation for the best approach, a high-level design for the proposed algorithm, and a workflow for handling exceptions and manual overrides.

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
