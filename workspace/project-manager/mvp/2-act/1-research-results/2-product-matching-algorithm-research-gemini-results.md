
# **A Strategic Framework for High-Accuracy Product Matching in E-Commerce**

## **Executive Summary**

The capacity to accurately and scalably match equivalent products across disparate online retailers is the cornerstone of any effective price comparison service. For the SuperMarty application, achieving this capability is not merely a feature but the foundational pillar upon which user trust and business viability are built. Incorrect matches erode user confidence and render price comparisons meaningless, while an inability to match a significant portion of products limits the application's utility. This report presents a comprehensive strategic and technical framework for developing a robust, multi-modal product matching system designed to meet the specific challenges of the supermarket domain.

The core recommendation of this analysis is the implementation of a **hybrid, tiered product matching architecture**. This system is designed to leverage the distinct strengths of multiple data modalities—product identifiers, text, and images—while systematically mitigating their individual weaknesses. The proposed architecture prioritizes computational efficiency and accuracy by operating in sequential tiers. The first and fastest tier utilizes the **European Article Number (EAN)**, a globally unique identifier, to achieve near-perfect matching accuracy (upwards of 99%) for a significant portion of the product catalog.

For products lacking a reliable EAN, the system escalates to a sophisticated **Natural Language Processing (NLP) tier**. This tier employs a **Siamese Network architecture powered by a fine-tuned Sentence-BERT (SBERT) model**. This approach moves beyond simple keyword matching to understand the semantic meaning of product titles and descriptions, enabling it to accurately match items with varied naming conventions (e.g., "Albert Heijn Halfvolle Melk 1L" and "Jumbo Halfvolle Melk 1L"). A third, supplementary tier uses **Computer Vision** to compare product images, providing a crucial verification signal that helps resolve ambiguity and increases overall confidence.

To manage the inherent uncertainty in any automated system, we propose a dynamic **hybrid confidence score**. This score synthesizes evidence from all tiers to produce a calibrated probability of a correct match. This score is the linchpin of the system's operational workflow, automatically confirming high-confidence matches, rejecting low-confidence ones, and, most importantly, routing ambiguous cases to a **Human-in-the-Loop (HITL) review system**.

The HITL workflow is designed not merely as a quality assurance mechanism but as the primary data labeling engine for continuous model improvement. By implementing an **Active Learning** strategy, the system intelligently prioritizes the most informative product pairs for human review, maximizing the value of each human decision and accelerating the model's learning curve. This creates a virtuous cycle where human expertise systematically reduces future ambiguity, driving the system towards greater automation and unparalleled accuracy over time.

This report provides a detailed analysis of each matching methodology, a high-level design of the recommended pipeline, a framework for confidence scoring, and a complete workflow for the HITL system. The proposed strategy represents a scalable, accurate, and cost-effective solution for building a world-class product matching capability.

## **Section 1: Strategic Analysis of Product Matching Methodologies**

The successful implementation of a product matching system hinges on a clear-eyed assessment of the available techniques, their respective strengths, and their inherent limitations within the specific context of scraping data from supermarket websites. No single method is a panacea; therefore, a strategic analysis is required to inform the design of a hybrid system that is greater than the sum of its parts. This section evaluates the three primary modalities for product matching: identifiers, text, and images.

### **1.1 The Gold Standard: Identifier-Based Matching (EAN/GTIN)**

The most direct and reliable method for matching products is through a globally unique identifier. In the European retail context, this is the European Article Number (EAN), a 13-digit barcode standard that is a subset of the Global Trade Item Number (GTIN) system.1

#### **Core Functionality & Benefits**

The fundamental value of an EAN is its uniqueness and standardization. Each specific product variant—down to the size and flavor—is assigned a distinct EAN by the manufacturer, governed by the global standards organization GS1.3 This creates a "product fingerprint" that is consistent across all retailers and platforms.3 For a price comparison tool, this is the ideal scenario. When two products from different retailers share the same EAN, they can be matched with extremely high confidence, ensuring a true "apples-to-apples" comparison. The use of EANs for matching can achieve accuracy rates exceeding 99% 6, drastically reducing catalog errors and eliminating duplicates.6 Major e-commerce marketplaces like Amazon and Google Shopping not only support but often mandate the use of GTINs for product listings, which underscores their central role in the modern digital retail ecosystem.3

#### **Data Availability & Reliability from Scrapers**

The efficacy of this strategy is entirely dependent on the presence and accessibility of EANs within the HTML or backend data of the target supermarket websites. Our research indicates that this is often feasible. Scraping services for major Dutch retailers like Albert Heijn and Jumbo explicitly advertise the extraction of comprehensive product data, including details like price, descriptions, and availability, which are often co-located with identifiers.9 Furthermore, open-source projects and developer tools like the

SupermarktConnector for Python demonstrate the ability to programmatically query the private APIs of these supermarkets using EANs as search keys, confirming their presence and accessibility in the backend systems.12

However, reliance on EANs alone is insufficient due to significant gaps in coverage. Certain product categories are systematically excluded from the global EAN system. Fresh foods like produce, meats, and bakery items are typically priced by weight and receive "in-store marking" with internal SKUs, not universal EANs.15 Private-label or store-brand products may also lack a public EAN. Additionally, the act of web scraping itself is inherently fragile. Supermarkets may implement anti-scraping technologies, alter their website's structure without notice, or have terms of service that legally prohibit automated data collection, posing both technical and legal risks.16

#### **Drawbacks of EANs**

Beyond availability, the EAN itself has limitations. The 13-digit code has a finite data capacity and contains no descriptive information; it is merely a pointer to a record in a database.19 Its physical barcode representation is susceptible to damage and printing errors, which, while less relevant for web scraping, underscores its simplicity as just an identifier.7 Therefore, while EAN matching is the most precise tool available, it cannot be the only tool.

### **1.2 The Semantic Engine: Text-Based Matching (NLP)**

When EANs are unavailable or unreliable, the system must infer matches from textual data such as product titles and descriptions. This requires Natural Language Processing (NLP) to move beyond simple string comparison and understand semantic meaning. The choice of NLP technology is a critical architectural decision with direct implications for both accuracy and long-term operational cost.

#### **Comparative Analysis of NLP Techniques**

* **Baseline (TF-IDF):** Term Frequency-Inverse Document Frequency is a classical information retrieval technique that represents documents as vectors based on the statistical importance of words.20 While fast and simple to implement, it is fundamentally flawed for this use case because it has no concept of semantics. For TF-IDF, the phrases "low-fat milk" and "reduced-fat milk" are entirely different if they do not share exact words. It cannot grasp that these phrases refer to the same concept, making it unsuitable for the nuanced variations present in product naming.22
* **Static Embeddings (Word2Vec/GloVe):** An improvement over TF-IDF, models like Word2Vec and GloVe learn dense vector representations (embeddings) for words, capturing semantic relationships.20 For example, the vectors for "milk" and "yogurt" would be closer in vector space than the vectors for "milk" and "detergent." However, these embeddings are static and context-agnostic. The word "light" would have the same vector representation in "light beer" (low calorie) and "light bulb" (illumination), leading to potential ambiguity and incorrect matches.23
* **Contextual Embeddings (BERT & Sentence-BERT):** Transformer-based models, pioneered by BERT (Bidirectional Encoder Representations from Transformers), revolutionized NLP by generating word embeddings that are dependent on their context within a sentence.20 This allows the model to differentiate between the different meanings of "light." For the task of large-scale product matching, a specific variant,  
  **Sentence-BERT (SBERT)**, is the superior choice. Standard BERT is too computationally expensive for the massive number of pairwise comparisons required. SBERT is fine-tuned to produce semantically meaningful embeddings for entire sentences (or product titles) that can be directly and efficiently compared using cosine similarity.24 This makes it highly scalable. Academic research demonstrates that SBERT-based systems can achieve remarkable performance, with accuracies reaching  
  **98.10%** and precision of **100%** on real-world product matching datasets.24

#### **The Architectural Choice: Siamese Networks**

To effectively leverage SBERT for matching, it should be implemented within a **Siamese Network** architecture. A Siamese Network consists of two or more identical sub-networks (the SBERT encoders) that process two inputs (e.g., two product titles) in parallel.27 The network is not trained to classify products, but rather to learn a similarity function. This is typically achieved using a

**triplet loss function**, where the model is given an "anchor" product, a "positive" (matching) product, and a "negative" (non-matching) product. The training objective is to minimize the distance between the anchor and positive embeddings while maximizing the distance between the anchor and negative embeddings.29

A key advantage of this architecture for an e-commerce application is its **"one-shot" learning** capability. Once the network is trained, it can generate a high-quality embedding for a brand-new product it has never encountered before. This new embedding can then be used to find the closest match in the existing database without needing to retrain the entire model, a crucial feature for a system dealing with a constantly evolving product catalog.30

The selection of a sophisticated NLP model like SBERT over simpler alternatives is not just a technical preference; it is a strategic decision that directly influences downstream operational costs. A less advanced model will inevitably produce more ambiguous or low-confidence matches. These cases must be funneled to a human review queue for manual resolution.31 A higher rate of ambiguity from the model directly translates to a larger, more expensive human review team. Therefore, an upfront investment in a superior NLP architecture minimizes long-term operational expenditures.

### **1.3 The Visual Verifier: Image-Based Matching (Computer Vision)**

Comparing product images offers an intuitive, third modality for matching. Computer Vision (CV) techniques can range from simple template matching to advanced deep learning models that generate image embeddings for similarity comparison.33

#### **Potential & Viability**

In an ideal world with perfect, standardized imagery, CV would be a powerful tool. Models can learn to generate vector "fingerprints" of images, which can then be compared using cosine distance to find visually identical products.26

#### **Significant Real-World Challenges**

The practical viability of image matching as a primary strategy is severely undermined by the inconsistent and often poor quality of product images found on supermarket websites.36 These images are not studio-grade photographs and suffer from numerous issues:

* **Data Inconsistency:** Images of the same product can vary dramatically in lighting, camera angle, background, resolution, and even packaging design due to manufacturer updates.38
* **Subtle but Critical Differences:** Computer vision models may struggle to distinguish between product variations that are visually very similar but functionally different. For example, packages for "Coca-Cola Classic" and "Coca-Cola Zero Sugar" might be nearly identical except for a small band of color or text, which a CV model might overlook.36
* **Computational Cost:** Generating and comparing high-dimensional image embeddings at scale is significantly more computationally intensive than processing text.

#### **Recommended Role**

Given these challenges, image matching should not be a primary matching strategy. Its optimal role is as a **supplementary signal or verification step** within a multi-modal system.26 For instance, if two products receive a moderately high text similarity score from the NLP model, a high image similarity score can significantly boost the overall confidence in the match. Conversely, if text similarity is high but image similarity is very low, it serves as a strong red flag, indicating that the pair should be prioritized for human review.

The foundational principle for the SuperMarty matching system must be an "EAN-First, NLP-Second" paradigm. This is the only approach that can achieve both the high precision demanded by users and the comprehensive coverage needed for the application to be useful. EANs provide near-perfect precision but suffer from incomplete coverage.6 NLP, specifically with a state-of-the-art SBERT model, provides the semantic matching capability to fill these coverage gaps but carries an inherent, albeit small, margin of error.24 Relying on one without the other would create a system that is either accurate but misses a large swath of products, or one that has broad coverage but is plagued by incorrect and trust-eroding matches. This establishes a clear hierarchical dependency that must be reflected in the system's architecture.

### **Table 1: Comparative Analysis of Matching Strategies**

| Strategy | Core Technology | Expected Accuracy | Pros | Cons | Scalability | Use Case for SuperMarty |
| :---- | :---- | :---- | :---- | :---- | :---- | :---- |
| **Identifier-Based** | EAN/GTIN Lookup | \>99% (when available) | Unambiguous, extremely high precision, fast lookup. 1 | Incomplete coverage (fresh produce, private labels), dependent on scraper reliability. 15 | High (simple database lookup). | **Primary Matcher (Tier 1):** The first and most reliable method for matching. The "fast lane" for definitive matches. |
| **Text-Based (NLP)** | Sentence-BERT in a Siamese Network | 95-98% (with fine-tuning) | Handles semantic variations, covers products without EANs, high accuracy with modern models. 24 | Requires training data, computationally more intensive than EAN lookup, can be confused by very subtle differences. | High (with ANN index like FAISS). 40 | **Secondary Matcher (Tier 2):** The core engine for products without EANs. Fills coverage gaps with high semantic accuracy. |
| **Image-Based (CV)** | CNN/Transformer Embeddings (e.g., CLIP) | 50-80% (highly variable) | Intuitive, can catch matches where text is sparse or misleading. | Highly sensitive to image quality, angle, lighting. Computationally expensive. Struggles with subtle text differences on packaging. 37 | Medium (computationally intensive). | **Verification Signal (Tier 3):** Used to increase or decrease confidence in matches proposed by NLP. Not a primary matcher. |

## **Section 2: Recommended Architecture: A Hybrid, Multi-Modal Matching System**

Building on the strategic analysis, this section presents the recommended architectural design for the SuperMarty product matching system. The design prioritizes accuracy, scalability, and resilience by integrating the different matching modalities into a single, cohesive pipeline.

### **2.1 The Case for a Hybrid Approach**

A system relying on a single matching strategy is destined to fail. An EAN-only system would be precise but would miss a large fraction of a supermarket's inventory, particularly high-frequency items like fresh produce and store brands. An NLP-only system would have better coverage but would be susceptible to subtle errors that erode user trust. An image-only system would be unreliable due to inconsistent source data.

A hybrid, multi-modal architecture is therefore not merely an option but a necessity.26 By layering the different techniques, the system can leverage the near-perfect precision of EANs for the majority of CPGs, the powerful semantic understanding of NLP for the rest, and the visual verification of computer vision to resolve ambiguity. This layered defense strategy is the optimal design to maximize accuracy, coverage, and robustness simultaneously.

### **2.2 High-Level System Design and Pipeline**

The product matching system should be designed as an event-driven, asynchronous pipeline that processes new or updated product information as it is delivered by the scraping service. This ensures that the matching process does not block the data ingestion flow and can be scaled independently.

The pipeline consists of five primary stages:

**Step 1: Data Ingestion & Preprocessing**

* A new or updated product record from a scraper (e.g., from Albert Heijn or Jumbo) is published to a message queue (e.g., RabbitMQ, Kafka), triggering the start of the pipeline.
* The first worker in the pipeline consumes the message and performs critical data cleaning and normalization.41 This includes:
    * Converting all text (titles, descriptions) to a consistent case (e.g., lowercase).
    * Removing extraneous special characters and HTML tags.
    * Standardizing units of measurement (e.g., "1L", "1 L", "1 Liter" are all converted to a canonical form like 1L).
    * Parsing and validating the EAN, if present.

**Step 2: Tier 1 \- EAN Matching (The Fast Lane)**

* The system first checks for the presence of a valid, normalized EAN on the incoming product record.
* If an EAN exists, it performs a direct lookup against a dedicated index (e.g., a hash map or a database table indexed on the EAN field) of all products in the SuperMarty catalog.
* **Success Condition:** If a single, unambiguous match is found, the incoming product is immediately linked to the corresponding "shadow product." A very high confidence score (e.g., 0.99) is assigned, and the pipeline terminates successfully for this item.1 This "fast lane" efficiently handles the easiest and most common matches with minimal computational overhead.
* **Failure Condition:** If the EAN is missing, invalid, or does not exist in the catalog, the product record is passed to the next tier.

**Step 3: Tier 2 \- NLP Similarity Matching (The Semantic Engine)**

* For products without a definitive EAN match, the system leverages the NLP model.
* The preprocessed product title and description are fed into the trained SBERT-based Siamese Network, which generates a high-dimensional feature vector (embedding) that captures the product's semantic essence.24
* This new embedding is then used to query a specialized vector similarity search index, such as FAISS or Annoy. This index contains the pre-computed embeddings for all unmatched products in the SuperMarty catalog.40 Using an Approximate Nearest Neighbor (ANN) index is critical for performance, as it allows for sub-linear time searches over millions of vectors, avoiding a costly brute-force comparison.
* The ANN search returns the top-k (e.g., top 5\) most similar product candidates from the catalog, along with their respective cosine similarity scores.

**Step 4: Tier 3 \- Image Similarity Verification (The Sanity Check)**

* This tier acts as a refinement and verification layer for the candidates proposed by the NLP tier.
* The system retrieves the pre-computed image embeddings for the incoming product and the top-k candidates.
* It then calculates the cosine similarity between the incoming product's image embedding and each of the candidates' image embeddings.26
* This image similarity score does not override the text score but serves as an additional, powerful feature. It is especially useful for disambiguating products with very similar names but different packaging (e.g., distinguishing between different flavors of a yogurt or diet vs. regular versions of a soda).

**Step 5: Confidence Calculation & Routing**

* The system now has a rich set of features for each potential match pair: the NLP similarity score, the image similarity score, and potentially other structured data matches (e.g., brand, quantity).
* These features are fed into a hybrid confidence score model (detailed in Section 3\) to calculate a final, calibrated probability of a correct match.
* Based on predefined thresholds, the system makes a final routing decision:
    * **High Confidence:** The match is automatically confirmed and the product is linked.
    * **Low Confidence:** The match is automatically rejected, and the incoming item is flagged for creation as a new shadow product.
    * **Medium Confidence:** The match is deemed ambiguous and is sent to the Human-in-the-Loop (HITL) review queue for manual validation.

This tiered architecture is intentionally designed to maximize computational efficiency. The most frequent and easiest matches are resolved using a simple, fast key-value lookup in Tier 1\. Only the more complex and ambiguous cases proceed to the more computationally expensive NLP and CV tiers. This prevents the system from wasting valuable compute resources on problems that have a simple solution, ensuring the entire pipeline remains scalable and cost-effective as the product catalog grows. Furthermore, the architecture is designed for modularity and graceful degradation. If, for example, image data cannot be scraped for a particular product, the pipeline can still function effectively using only the EAN and NLP tiers. This resilience is critical for a system dependent on external, and often unreliable, data sources.16

### **2.3 Core Algorithm Recommendation**

To implement this architecture, the following specific algorithms and technologies are recommended:

* **Identifier:** **EAN-13** should be treated as the primary key for product matching.
* **NLP Model:** A **Siamese Network** architecture is the recommended framework.30 The encoder within this network should be a  
  **fine-tuned Sentence-BERT model**. A model like all-MiniLM-L6-v2 serves as an excellent starting point due to its balance of high performance and computational efficiency.24 The network must be trained with a  
  **triplet loss function** on a custom dataset of known matching and non-matching supermarket product pairs to adapt it to the specific vocabulary and nuances of the domain.29
* **Image Model:** A pre-trained multi-modal model such as **CLIP** (Contrastive Language–Image Pre-training) is a strong candidate for generating image embeddings. Alternatively, a state-of-the-art Convolutional Neural Network (e.g., **EfficientNet**) can be fine-tuned on product images.35 The objective is not image classification but the generation of robust, comparable vector representations.
* **Similarity Search Index:** For both the NLP and image embedding vectors, using a library like **FAISS (Facebook AI Similarity Search)** is highly recommended. FAISS is purpose-built for efficient similarity search and clustering of dense vectors and is designed to scale to billions of vectors, making it essential for a production-grade system.40

## **Section 3: Quantifying Certainty: The Confidence Score Framework**

A reliable confidence score is the central nervous system of the automated matching pipeline. It translates the multi-faceted outputs of the matching tiers into a single, actionable metric. This score dictates whether a match is confirmed automatically, rejected, or escalated for the costly but necessary process of human review. Therefore, its design and calculation methodology are of paramount importance.

### **3.1 Principles of Confidence Scoring**

A confidence score is a calibrated probability, expressed as a normalized value between 0 and 1, that represents the system's certainty that a predicted match is correct.44 It is crucial to distinguish this from a raw similarity score. While a high similarity score (e.g., from NLP) is an input to the confidence calculation, the final confidence score should reflect the likelihood of correctness based on all available evidence.

The primary business function of this score is to enable threshold-based automation.31 A typical three-tiered thresholding strategy would be:

* **High Threshold (e.g., \> 0.95):** Matches exceeding this value are considered highly reliable and are automatically accepted.
* **Low Threshold (e.g., \< 0.70):** Matches below this value are considered unlikely to be correct and are automatically rejected.
* **Review Zone (e.g., 0.70 to 0.95):** Matches falling within this range are ambiguous and are routed to the human review queue.

Setting these thresholds is a business decision that balances the cost of manual review against the risk of incorrect automatic matches. A good starting point is to target an overall model confidence of 80% or higher, with more sensitive applications requiring scores closer to 100% before full automation is trusted.44

### **3.2 A Hybrid Confidence Score Methodology**

To produce a single, reliable score, evidence from the various pipeline tiers must be synthesized. A simple approach would be to use hand-tuned weights, but a far more robust and defensible method is to train a lightweight model to predict the probability of a match based on the features generated by the pipeline.

#### **Input Features for the Score Model**

The following features should be generated for each candidate product pair and used as input to the confidence model:

1. EAN\_Match\_Found (Binary: 1 or 0): The single most powerful predictive feature.
2. NLP\_Similarity\_Score (Float: 0.0 to 1.0): The raw cosine similarity score from the SBERT model comparison.
3. Image\_Similarity\_Score (Float: 0.0 to 1.0): The raw cosine similarity score from the image embedding comparison.
4. Brand\_Match (Binary: 1 or 0): A feature indicating whether the parsed brand names are an exact or fuzzy match.
5. Quantity\_Match (Binary: 1 or 0): A feature indicating whether the parsed quantities (e.g., "1L", "500g") match.
6. Numeric\_Overlap\_Ratio (Float: 0.0 to 1.0): The Jaccard similarity of the sets of numbers found in each product title (e.g., model numbers, pack sizes).

#### **Proposed Calculation Logic**

A multi-step logic ensures that the strongest signals are given appropriate priority.

* Step 1: EAN Override. The presence of a confirmed EAN match is considered definitive evidence. If the EAN\_Match\_Found feature is 1, the confidence score is set to a high, fixed value, bypassing the rest of the model.  
  Confidence \= 0.99
* **Step 2: Model-Based Scoring.** For all pairs without an EAN match, the remaining features are fed into a trained classification model. The recommended model is **Logistic Regression**. This model is simple, fast to train and execute, and its output is a naturally calibrated probability between 0 and 1, which is exactly what is needed for a confidence score.45  
  The model would be trained on a labeled dataset of product pairs (generated initially by manual labeling and continuously updated by the HITL workflow). The model learns the optimal weights (wi​) for each input feature (xi​) to predict the probability of a match. The formula is:  
  P(match)=1+e−(β0​+w1​x1​+w2​x2​+...+wn​xn​)1​

  The output, P(match), becomes the confidence score. This data-driven approach is superior to a simple weighted average because it learns the complex interplay and relative importance of the features directly from evidence, rather than relying on heuristics. For example, it might learn that for certain product categories, image similarity is more important than for others.

This framework creates a system where the confidence score is not a static, arbitrary number. It is a dynamic output of the entire ML system and must be treated as such. When the underlying NLP or image models are retrained with new data from the HITL feedback loop, their output distributions can change—a phenomenon known as data drift.46 A similarity score of 0.85 from the old model might not represent the same level of certainty as a 0.85 from the newly retrained model. Consequently, the confidence score model (the logistic regression classifier) must also be recalibrated or retrained, and the automation thresholds (e.g., 0.95 and 0.70) must be re-evaluated to ensure the business logic remains consistent.47

Ultimately, the average confidence score across all predictions becomes a key performance indicator (KPI) for the health of the entire matching system. A consistently increasing average confidence score indicates that the models are learning effectively from the HITL feedback and are becoming better at resolving matches without ambiguity. Conversely, a stagnant or declining average confidence score is a critical alert. It may signal that the models are failing to generalize or, more likely, that the nature of the incoming product data is changing ("concept drift"), necessitating a more fundamental review of the models and features.46

### **Table 2: Hybrid Confidence Score Components**

| Signal Source | Feature Name | Data Type | Calculation Method | Proposed Importance |
| :---- | :---- | :---- | :---- | :---- |
| **Tier 1: Identifier** | EAN\_Match\_Found | Binary | Direct lookup in EAN index. | **Highest:** Acts as an override. |
| **Tier 2: NLP** | NLP\_Similarity\_Score | Float (0-1) | Cosine similarity of SBERT embeddings. | **High:** The primary signal for non-EAN matches. |
| **Tier 3: Image** | Image\_Similarity\_Score | Float (0-1) | Cosine similarity of image embeddings. | **Medium:** A strong verification signal. |
| **Structured Data** | Brand\_Match | Binary | Fuzzy string matching on parsed brand names. | **Medium:** Helps differentiate between similar products from different brands. |
| **Structured Data** | Quantity\_Match | Binary | Comparison of normalized quantity values. | **Medium:** Critical for distinguishing different product sizes. |

## **Section 4: The Human Element: An Active Learning and Manual Override Workflow**

No automated system, however sophisticated, can achieve perfect accuracy on a task as complex and nuanced as product matching. Ambiguity is inevitable. The Human-in-the-Loop (HITL) system is the critical component that addresses this ambiguity, ensures the final accuracy of the platform, and, most importantly, provides the feedback necessary for the machine learning models to continuously improve.

### **4.1 Designing the Admin Review Interface**

The admin review interface is the primary tool for human validators. Its design must be relentlessly focused on efficiency, clarity, and minimizing the cognitive load on the user to enable rapid and accurate decision-making.48

The interface should be built around three core components:

1. **Review Queue Dashboard:** This is the landing page for validators. It should present a clear, sortable, and filterable list of product pairs that require manual review.48 Key functionalities include:
    * Displaying the queue of items, with the highest priority items (based on the active learning strategy) at the top.
    * Showing the system's confidence score for each pair, allowing validators to grasp the level of ambiguity at a glance.
    * Allowing sorting and filtering by confidence score, product category, or date to manage the workload effectively.
2. **Side-by-Side Comparison View:** When a validator selects an item from the queue, they are taken to the main review screen. This view must present all necessary information for an informed decision in a clean, side-by-side layout.32 It must include:
    * **Primary Information:** Large, clear product images, full product titles, and full product descriptions.
    * **Key Attributes:** A structured table showing brand, price, and normalized quantity/size for both products.
    * **AI Context:** The system's overall **Confidence Score** should be prominently displayed. Critically, a breakdown of the contributing scores (e.g., NLP Similarity: 0.82, Image Similarity: 0.75) should also be visible. This provides the validator with context on *why* the system was uncertain, which can guide their attention and build trust.
3. **Action & Feedback Module:** This module allows the validator to render a judgment and provide structured feedback.
    * **Action Buttons:** Two large, clear, and mutually exclusive buttons: \[Confirm Match\] and \`\`.
    * **Structured Feedback:** If \`\` is selected, the system must prompt the user for a reason using a mandatory dropdown menu. This is far more valuable for model training than a free-text field. The categories should be tailored to common failure modes, such as: "Different Size/Volume," "Different Flavor/Variety," "Different Brand," "Different Product Line (e.g., Organic vs. Regular)," or "Completely Wrong Product".49
    * **Optional Comments:** An optional text box for complex cases that don't fit the predefined categories.

### **4.2 The Human-in-the-Loop (HITL) Operational Workflow**

The HITL system automates the flow of information between the AI and human experts, ensuring that human attention is applied precisely where it is most valuable.32

* **Step 1: Triage by Confidence Score:** As described in Section 3, the matching pipeline automatically triages every potential match based on its confidence score.
    * Confidence \> 0.95: **Auto-Approve.** The match is finalized and persisted in the database without human intervention.
    * Confidence \< 0.70: **Auto-Reject.** The match is discarded, and the new item is slated for creation as a new "shadow product."
    * 0.70 \<= Confidence \<= 0.95: **Send to Review Queue.** These ambiguous pairs are the primary input for the HITL system and are populated into the admin review interface.32
* **Step 2: Human Review:** A validator logs into the admin interface, selects a pair from the queue (prioritized by the active learning algorithm), and uses the comparison view to make a Confirm or Reject decision.
* **Step 3: Feedback Ingestion and Propagation:** Every decision made by a validator is logged as a high-quality, human-verified data point. For example, a Confirm action creates a labeled pair (product\_A, product\_B, label: match). This new labeled data is added to a "gold standard" dataset, which serves as the ground truth for subsequent model retraining.32

### **4.3 Closing the Loop: Retraining with User Feedback & Active Learning**

The ultimate goal of the HITL system is to make itself obsolete over time by teaching the AI to handle cases it previously found ambiguous. This is achieved through a combination of periodic retraining and an intelligent sampling strategy known as active learning.

#### **Periodic Retraining**

The "gold standard" dataset of human-verified labels is the most valuable asset for model improvement. The core NLP and image embedding models must be periodically fine-tuned on this growing dataset.47 This process allows the models to learn from their past mistakes, adapt to new product naming conventions, and become more accurate over time. The retraining pipeline should be automated but include manual gates for deploying the new model into production to prevent unforeseen performance regressions.47

#### **Active Learning Strategy**

To maximize the efficiency of the human review process and accelerate model improvement, an active learning strategy should be implemented. Instead of presenting validators with a random or FIFO (First-In, First-Out) queue of ambiguous items, the system should intelligently prioritize the items that will provide the most new information to the model.

* **Core Strategy: Uncertainty Sampling.** The most common and effective active learning strategy for this type of problem is uncertainty sampling. The system will prioritize pairs for review for which the model is most uncertain. In a binary classification task (match vs. no-match), this corresponds to items with a confidence score closest to **0.5**.43 These are the data points that lie on or near the model's decision boundary. Providing a correct label for these "edge cases" gives the model the most information needed to adjust its boundary, leading to the fastest improvement in performance.
* **Benefit:** Active learning dramatically reduces the number of labels required to achieve a high level of model accuracy compared to random sampling.43 This makes the entire HITL process more cost-effective and allows the system to reach a state of high automation much more quickly.

The HITL system should be viewed not as a simple quality assurance backstop, but as the primary **data labeling engine** for the entire machine learning platform. Its immediate function is to correct errors 50, but its most significant long-term value lies in the creation of a continuous stream of high-quality, proprietary training data that is perfectly tailored to the system's specific domain and failure modes.32 This reframes the cost of the human review team from a mere operational expense into a strategic investment in a core competitive asset. By implementing an active learning framework, this process is transformed from a reactive error-correction task into a proactive, intelligent data acquisition strategy that systematically targets and eliminates model uncertainty.43

## **Section 5: Conclusion and Strategic Roadmap**

The ability to perform high-accuracy product matching at scale is a non-negotiable prerequisite for the success of the SuperMarty price comparison application. The analysis conducted in this report demonstrates that achieving this goal requires a sophisticated, multi-faceted approach that combines the strengths of deterministic identifiers, advanced machine learning, and targeted human expertise. A simplistic or single-modality solution will inevitably fail, either by providing inaccurate matches that destroy user trust or by failing to cover a sufficient portion of the product catalog to be useful.

### **5.1 Summary of Recommendations**

The optimal path forward is the development of a hybrid, multi-modal product matching system built on the following core principles:

1. **Adopt a Hybrid, Tiered Architecture:** Implement the proposed tiered pipeline that prioritizes efficiency and accuracy. Leverage EANs for fast, precise matches, followed by a sophisticated NLP model for semantic coverage, and finally use computer vision for verification.
2. **Prioritize EANs for Precision:** Treat the European Article Number (EAN) as the primary and most reliable matching key. The system should be optimized to handle these matches in a computationally efficient "fast lane."
3. **Implement State-of-the-Art NLP:** The core of the non-EAN matching engine should be a Sentence-BERT-based Siamese Network. This provides the necessary semantic understanding to handle the variations in product naming found in the real world.
4. **Use Images for Verification:** Computer vision should be used as a supplementary signal to increase or decrease confidence in matches proposed by the NLP tier, not as a primary matching method.
5. **Develop a Data-Driven Confidence Score:** Create a hybrid confidence score based on a lightweight logistic regression model. This provides a calibrated and defensible mechanism for automating match decisions.
6. **Invest in a Human-in-the-Loop System with Active Learning:** The HITL workflow is essential for handling ambiguity and achieving near-perfect accuracy. Crucially, it must be designed as a data labeling engine that feeds an active learning strategy to continuously and efficiently improve the core ML models.

### **5.2 Phased Implementation Roadmap**

A phased implementation is recommended to manage complexity, deliver value incrementally, and allow the system to learn and adapt as it is being built.

#### **Phase 1: MVP \- High Accuracy & Core Coverage**

* **Tasks:**
    * Develop the foundational data scraping and preprocessing pipeline for target supermarkets (e.g., Albert Heijn, Jumbo).
    * Implement the Tier 1 EAN-based matching logic.
    * Implement the Tier 2 NLP matching model using a pre-trained, off-the-shelf Sentence-BERT model (e.g., all-MiniLM-L6-v2) without initial fine-tuning.
    * Build the initial version of the admin review interface and the HITL workflow, using a simple confidence score based on NLP similarity to route items for review.
* **Goal:** Achieve very high accuracy on the significant portion of products that have EANs. Establish a functional baseline for NLP matching and begin the critical process of collecting human-labeled data for future model improvement.

#### **Phase 2: Enhancement \- Increased Accuracy & Efficiency**

* **Tasks:**
    * Use the labeled data collected in Phase 1 to **fine-tune** the Sentence-BERT model. This will adapt the model to the specific language and patterns of supermarket products, significantly boosting its accuracy.
    * Implement the Tier 3 image similarity model and integrate its output as a feature into the confidence score calculation.
    * Refine the confidence score by replacing the simple similarity-based score with the recommended **logistic regression model**, training it on the human-labeled dataset.
* **Goal:** Substantially improve match accuracy for non-EAN products. Reduce the volume of items sent for manual review by improving the model's confidence and calibration.

#### **Phase 3: Optimization \- Scalability & Automation**

* **Tasks:**
    * Implement the **Active Learning** strategy (Uncertainty Sampling) in the HITL queue. This will prioritize the most informative items for review, accelerating model improvement and optimizing the use of human resources.
    * Automate the model retraining and deployment pipeline, incorporating manual approval gates to ensure production stability.47
    * Scale the underlying infrastructure, particularly by implementing a high-performance Approximate Nearest Neighbor index like **FAISS** for both text and image vector search.
* **Goal:** Achieve an overall system accuracy exceeding 99%. Minimize the need for human intervention to only the most novel or complex cases. Create a fully scalable, resilient, and self-improving product matching platform that serves as a durable competitive advantage.

#### **Works cited**

1. Master Amazon Price Scraping \- Guide Using EAN Codes \- Actowiz Solutions, accessed June 17, 2025, [https://www.actowizsolutions.com/amazon-price-scraping-using-ean-codes.php](https://www.actowizsolutions.com/amazon-price-scraping-using-ean-codes.php)
2. EAN Barcode Finder: Unlocking Product Information \- StartupBros, accessed June 17, 2025, [https://startupbros.com/ean-barcode-finder/](https://startupbros.com/ean-barcode-finder/)
3. How to Generate EAN Codes for Your Business \- Pricefy Blog, accessed June 17, 2025, [https://www.pricefy.io/articles/how-to-generate-ean-codes-for-your-business](https://www.pricefy.io/articles/how-to-generate-ean-codes-for-your-business)
4. EAN number \- What Is It and Do I Need It? \- Taxually, accessed June 17, 2025, [https://www.taxually.com/blog/the-ean-number-what-is-it-and-do-i-need-it](https://www.taxually.com/blog/the-ean-number-what-is-it-and-do-i-need-it)
5. European Article Numbering: Everything About EAN Codes \- Prisync, accessed June 17, 2025, [https://prisync.com/blog/ean-code/](https://prisync.com/blog/ean-code/)
6. Scrape EAN Numbers from Douglas for 2025 Matching \- Actowiz Solutions, accessed June 17, 2025, [https://www.actowizsolutions.com/douglas-ean-scraping-product-matching.php](https://www.actowizsolutions.com/douglas-ean-scraping-product-matching.php)
7. EAN : What is it? Structure, benefits and challenges \- Solidpepper, accessed June 17, 2025, [https://www.solidpepper.com/en/blog/ean-what-is-it-structure-benefits-and-challenges](https://www.solidpepper.com/en/blog/ean-what-is-it-structure-benefits-and-challenges)
8. What Is an EAN Code, and Why Do You Need One? \- e-tailize, accessed June 17, 2025, [https://e-tailize.com/blog/what-is-an-ean-code-and-why-do-you-need-one/](https://e-tailize.com/blog/what-is-an-ean-code-and-why-do-you-need-one/)
9. Albert Heijn Price and Data Scraper \- ShoppingScraper, accessed June 17, 2025, [https://shoppingscraper.com/scrapers/ah](https://shoppingscraper.com/scrapers/ah)
10. Albert Heijn Grocery Data Scraping \- Extract Albert Heijn Supermarket Data \- Actowiz Solutions, accessed June 17, 2025, [https://www.actowizsolutions.com/albert-heijn-grocery-data-scraping-services.php](https://www.actowizsolutions.com/albert-heijn-grocery-data-scraping-services.php)
11. Jumbo Grocery Data Scraping \- Extract Jumbo Supermarket Data \- Actowiz Solutions, accessed June 17, 2025, [https://www.actowizsolutions.com/jumbo-grocery-data-scraping-services.php](https://www.actowizsolutions.com/jumbo-grocery-data-scraping-services.php)
12. Albert Heijn Plugin (alternative for OpenFoodFacts) : r/grocy \- Reddit, accessed June 17, 2025, [https://www.reddit.com/r/grocy/comments/1jc2yn2/albert\_heijn\_plugin\_alternative\_for\_openfoodfacts/](https://www.reddit.com/r/grocy/comments/1jc2yn2/albert_heijn_plugin_alternative_for_openfoodfacts/)
13. grocy-dutch-supermarket/README.md at main · PaulVerhoeven1 ..., accessed June 17, 2025, [https://github.com/PaulVerhoeven1/grocy-dutch-supermarket/blob/main/README.md](https://github.com/PaulVerhoeven1/grocy-dutch-supermarket/blob/main/README.md)
14. PaulVerhoeven1/grocy-dutch-supermarket: Python application that searches for product infromation with the Jumbo.com or AH.nl api to download product information and posting those information to the self-hosted grocery management solution Grocy. \- GitHub, accessed June 17, 2025, [https://github.com/PaulVerhoeven1/grocy-dutch-supermarket](https://github.com/PaulVerhoeven1/grocy-dutch-supermarket)
15. EAN | Basics of Barcodes \- Keyence, accessed June 17, 2025, [https://www.keyence.com/ss/products/auto\_id/codereader/basic/ean.jsp](https://www.keyence.com/ss/products/auto_id/codereader/basic/ean.jsp)
16. How new large data sources require price statisticians to re-think their index, accessed June 17, 2025, [https://www.bundesbank.de/resource/blob/635820/11870abc82e494c16421a6e87a1de8ab/472B63F073F071307366337C94F8C870/2017-05-10-ottawa-group-06-3-paper-data.pdf](https://www.bundesbank.de/resource/blob/635820/11870abc82e494c16421a6e87a1de8ab/472B63F073F071307366337C94F8C870/2017-05-10-ottawa-group-06-3-paper-data.pdf)
17. How Can Businesses Effectively Scrape EAN Numbers and Product Details for Competitive Analysis?, accessed June 17, 2025, [https://www.iwebdatascraping.com/scrape-ean-numbers-and-product-details-for-competitive-analysis.php](https://www.iwebdatascraping.com/scrape-ean-numbers-and-product-details-for-competitive-analysis.php)
18. If I were to web crawl supermarkets' websites and retrieve info and create a comparison tool for sale would that be illegal? \- Quora, accessed June 17, 2025, [https://www.quora.com/If-I-were-to-web-crawl-supermarkets-websites-and-retrieve-info-and-create-a-comparison-tool-for-sale-would-that-be-illegal](https://www.quora.com/If-I-were-to-web-crawl-supermarkets-websites-and-retrieve-info-and-create-a-comparison-tool-for-sale-would-that-be-illegal)
19. Advantages and disadvantages of EAN-13 barcode, accessed June 17, 2025, [https://free-barcode.com/barcode/barcode-types/advantages-disadvantages-ean-13-barcode.asp](https://free-barcode.com/barcode/barcode-types/advantages-disadvantages-ean-13-barcode.asp)
20. Calculating Document Similarities using BERT and other models \- Towards Data Science, accessed June 17, 2025, [https://towardsdatascience.com/calculating-document-similarities-using-bert-and-other-models-b2c1a29c9630/](https://towardsdatascience.com/calculating-document-similarities-using-bert-and-other-models-b2c1a29c9630/)
21. Text Classification: Tf-Idf vs Word2Vec vs Bert \- Kaggle, accessed June 17, 2025, [https://www.kaggle.com/code/naim99/text-classification-tf-idf-vs-word2vec-vs-bert](https://www.kaggle.com/code/naim99/text-classification-tf-idf-vs-word2vec-vs-bert)
22. Word embeddings in NLP: A Complete Guide \- Turing, accessed June 17, 2025, [https://www.turing.com/kb/guide-on-word-embeddings-in-nlp](https://www.turing.com/kb/guide-on-word-embeddings-in-nlp)
23. What are the differences between GloVe, word2vec and tf-idf? \- Quora, accessed June 17, 2025, [https://www.quora.com/What-are-the-differences-between-GloVe-word2vec-and-tf-idf](https://www.quora.com/What-are-the-differences-between-GloVe-word2vec-and-tf-idf)
24. Product Matching using Sentence-BERT: A Deep ... \- Everant Journals, accessed June 17, 2025, [https://www.everant.org/index.php/etj/article/download/1648/1191/4636](https://www.everant.org/index.php/etj/article/download/1648/1191/4636)
25. Comparing NLP Techniques for Scalable Product Search \- MongoDB, accessed June 17, 2025, [https://www.mongodb.com/developer/products/atlas/compare-nlp-techniques-product-search/](https://www.mongodb.com/developer/products/atlas/compare-nlp-techniques-product-search/)
26. Product Matching through Multimodal Image and Text ... \- DiVA portal, accessed June 17, 2025, [https://www.diva-portal.org/smash/get/diva2:1591884/FULLTEXT01.pdf](https://www.diva-portal.org/smash/get/diva2:1591884/FULLTEXT01.pdf)
27. Siamese Network In NLP Made Simple & How To Tutorial In Python \- Spot Intelligence, accessed June 17, 2025, [https://spotintelligence.com/2023/01/19/siamese-network-in-nlp/](https://spotintelligence.com/2023/01/19/siamese-network-in-nlp/)
28. Using Siamese Networks to Power Accurate Product Matching in eCommerce \- DataWeave, accessed June 17, 2025, [https://dataweave.com/blog/using-siamese-networks-to-power-accurate-product-matching-in-ecommerce](https://dataweave.com/blog/using-siamese-networks-to-power-accurate-product-matching-in-ecommerce)
29. Siamese Neural Networks with Triplet Loss and Cosine Distance | Towards Data Science, accessed June 17, 2025, [https://towardsdatascience.com/siamese-neural-networks-with-tensorflow-functional-api-6aef1002c4e/](https://towardsdatascience.com/siamese-neural-networks-with-tensorflow-functional-api-6aef1002c4e/)
30. Transformer-Based Deep Siamese Network for At-Scale Product ..., accessed June 17, 2025, [https://oars-workshop.github.io/2021/Pang.pdf](https://oars-workshop.github.io/2021/Pang.pdf)
31. eCommerce Product Matching \- Competitive Pricing Intelligence \- Actowiz Solutions, accessed June 17, 2025, [https://www.actowizsolutions.com/ecommerce-product-maching-and-pricing-intelligence.php](https://www.actowizsolutions.com/ecommerce-product-maching-and-pricing-intelligence.php)
32. Augmenting AI-powered Product Matching with Human Expertise to ..., accessed June 17, 2025, [https://dataweave.com/blog/augmenting-ai-powered-product-matching-with-human-expertise-to-achieve-unparalleled-accuracy](https://dataweave.com/blog/augmenting-ai-powered-product-matching-with-human-expertise-to-achieve-unparalleled-accuracy)
33. How to Do Template Matching with Computer Vision \- Roboflow Blog, accessed June 17, 2025, [https://blog.roboflow.com/template-matching-computer-vision/](https://blog.roboflow.com/template-matching-computer-vision/)
34. paritoshtripathi935/Product-Matching: The topic is about product matching via Machine Learning. This involves using various machine learning techniques such as natural language processing, image recognition, and collaborative filtering algorithms to match similar products together. \- GitHub, accessed June 17, 2025, [https://github.com/paritoshtripathi935/Product-Matching](https://github.com/paritoshtripathi935/Product-Matching)
35. \[2403.11593\] End-to-end multi-modal product matching in fashion e-commerce \- arXiv, accessed June 17, 2025, [https://arxiv.org/abs/2403.11593](https://arxiv.org/abs/2403.11593)
36. Using Images and Metadata for Product Fuzzy Matching with Zingg \- Databricks, accessed June 17, 2025, [https://www.databricks.com/blog/using-images-and-metadata-product-fuzzy-matching-zingg](https://www.databricks.com/blog/using-images-and-metadata-product-fuzzy-matching-zingg)
37. SOTA SKU Image Classification for Product Matching | How we outperformed the Fashion CLIP model | Width.ai, accessed June 17, 2025, [https://www.width.ai/post/sku-image-classification-for-product-matching](https://www.width.ai/post/sku-image-classification-for-product-matching)
38. Announcing the 2020 Image Matching Benchmark and Challenge \- Google Research, accessed June 17, 2025, [https://research.google/blog/announcing-the-2020-image-matching-benchmark-and-challenge/](https://research.google/blog/announcing-the-2020-image-matching-benchmark-and-challenge/)
39. Product Matching in Fashion and Footwear: Use and Benefits | Centric Software, accessed June 17, 2025, [https://www.centricsoftware.com/blog/product-matching-in-fashion/](https://www.centricsoftware.com/blog/product-matching-in-fashion/)
40. \[Discussion\] NLP for products matching : r/datascience \- Reddit, accessed June 17, 2025, [https://www.reddit.com/r/datascience/comments/108a5sj/discussion\_nlp\_for\_products\_matching/](https://www.reddit.com/r/datascience/comments/108a5sj/discussion_nlp_for_products_matching/)
41. Perfecting Data Matching: Essential Techniques and Best Practices Revealed, accessed June 17, 2025, [https://dataladder.com/definitive-guide-to-data-matching/](https://dataladder.com/definitive-guide-to-data-matching/)
42. Mastering Address Matching: Techniques and Best Practices \- Placekey, accessed June 17, 2025, [https://www.placekey.io/blog/address-matching](https://www.placekey.io/blog/address-matching)
43. Deep Indexed Active Learning for Matching ... \- VLDB Endowment, accessed June 17, 2025, [http://www.vldb.org/pvldb/vol15/p31-jain.pdf](http://www.vldb.org/pvldb/vol15/p31-jain.pdf)
44. Interpret and improve model accuracy and confidence scores \- Azure AI services, accessed June 17, 2025, [https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/concept/accuracy-confidence?view=doc-intel-4.0.0](https://learn.microsoft.com/en-us/azure/ai-services/document-intelligence/concept/accuracy-confidence?view=doc-intel-4.0.0)
45. US20140136549A1 \- System and method for automatic product matching \- Google Patents, accessed June 17, 2025, [https://patents.google.com/patent/US20140136549A1/en](https://patents.google.com/patent/US20140136549A1/en)
46. Retraining Model During Deployment: Continuous Training and Continuous Testing, accessed June 17, 2025, [https://neptune.ai/blog/retraining-model-during-deployment-continuous-training-continuous-testing](https://neptune.ai/blog/retraining-model-during-deployment-continuous-training-continuous-testing)
47. Automatic retraining for machine learning models \- Building Nubank, accessed June 17, 2025, [https://building.nubank.com/automatic-retraining-for-machine-learning-models/](https://building.nubank.com/automatic-retraining-for-machine-learning-models/)
48. How to Design User-Friendly Dashboard Interfaces \- MetricsWatch, accessed June 17, 2025, [https://metricswatch.com/insights/how-to-design-user-friendly-dashboard-interfaces](https://metricswatch.com/insights/how-to-design-user-friendly-dashboard-interfaces)
49. User feedback \- the missing piece of your ML monitoring stack | Towards Data Science, accessed June 17, 2025, [https://towardsdatascience.com/user-feedback-the-missing-piece-of-your-ml-monitoring-stack-46b2bbf0b5e4/](https://towardsdatascience.com/user-feedback-the-missing-piece-of-your-ml-monitoring-stack-46b2bbf0b5e4/)
50. The Complete Guide to Human-in-the-Loop Automation \- Klippa, accessed June 17, 2025, [https://www.klippa.com/en/blog/information/human-in-the-loop/](https://www.klippa.com/en/blog/information/human-in-the-loop/)
51. Feedback Loops, Model Validation, and Retraining \- sensXPERT, accessed June 17, 2025, [https://www.sensxpert.com/blog/feedback-loops-model-validation-retraining/](https://www.sensxpert.com/blog/feedback-loops-model-validation-retraining/)
52. Why, When, and How to Retrain Machine Learning Models \- Striveworks, accessed June 17, 2025, [https://www.striveworks.com/blog/why-when-and-how-to-retrain-machine-learning-models](https://www.striveworks.com/blog/why-when-and-how-to-retrain-machine-learning-models)
53. Active Learning for Matching Problems, accessed June 17, 2025, [https://icml.cc/2012/papers/197.pdf](https://icml.cc/2012/papers/197.pdf)
