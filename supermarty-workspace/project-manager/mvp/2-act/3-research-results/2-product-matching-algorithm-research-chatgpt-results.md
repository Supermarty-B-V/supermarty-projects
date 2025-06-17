Great. I will investigate and propose a robust strategy for accurately matching equivalent products across different supermarket websites to power SuperMarty’s price comparison engine.

This will include an analysis of identifier-based, NLP-based, image-based, and hybrid matching methods, a specific algorithm recommendation with high-level design, and a system for handling low-confidence matches through manual admin review and learning.

I’ll get back to you with a comprehensive report summarizing the findings and clear recommendations.


# Matching Supermarket Products Across Retailers

To compare supermarket prices fairly, SuperMarty must group identical real-world products from different stores into unified **shadow products**. This is hard because product catalogs use different titles, formats, or may lack common IDs. Accurate matching is crucial – as one price monitoring vendor notes, *“with no product matching our client wouldn’t be able to perform any kind of price comparison.”*. We compare several approaches below.

## 1. Identifier-Based Matching (EAN/GTIN)

EANs (GTINs) are globally unique barcodes for products. When available, they give exact equivalence: if two items share the same EAN, they are the same SKU. Price2Spy’s automatch uses these **unique IDs (EAN, UPC, ASIN, MPN)** to link products. EAN matching is highly reliable *if* the code is present and correctly scraped. It makes matching trivial (100% precision if two retailers use the same barcode). In theory this is ideal: unique codes eliminate ambiguity. In practice, however, EANs are often **missing or inconsistent** on retailer websites. Many e-commerce pages omit barcodes or use internal SKUs, and some retailers (especially marketplaces) use their own IDs (e.g. Amazon’s ASIN). Thus identifier-based matching can only cover products when metadata is complete. Without an EAN, this method has no result. In summary:

* **Pros:** Exact match, language-independent, minimal false positives. Highly reliable when available.
* **Cons:** Often unavailable in scraped data. Requires an external database or parsing of hidden fields/OCR. Cannot match items lacking standard codes.

## 2. Text-Based (NLP) Matching

When barcodes are missing, we compare textual data: product names, descriptions, brands, sizes, etc. Traditional methods include token-based similarity (TF-IDF or character n-gram distance). These can catch simple matches but fail on synonyms, abbreviations, or reordered words. Modern NLP uses **vector embeddings**. For example, pretrained models like Word2Vec/GloVe embed words, while deep models (e.g. BERT) embed whole titles. Transformer models (BERT, RoBERTa, multilingual BERT) have proven especially effective: one study found that applying *BERT-based similarity learning* dramatically improved e-commerce product matching performance. Classical methods “rely on rule-based methods and string similarities”, but BERT-like models capture context and semantics. For instance, two titles with different wording but the same meaning will have similar BERT embeddings. Multilingual BERT can even match across languages: one experiment showed multilingual BERT achieving \~87% F1 on German products, outperforming a German-specific model by 14%.

**Approach:** A common strategy is to compute embeddings for product titles (and optionally descriptions/brands) and measure cosine similarity. Sentence-transformers (SBERT) or custom fine-tuning on product pairs can boost accuracy. Numerical attributes (weights, volumes) are normalized (e.g. converting “400g” vs “0.4 kg”). If two items’ embeddings are above a threshold, they are matched. Transformers require more computation but handle variation well.

**Pros:** Works without explicit IDs; robust to minor wording differences; handles multiple languages (with multilingual models). Learns context (e.g. brand knowledge) that simple string rules miss. Easily scales via approximate nearest-neighbor search on vectors.
**Cons:** Can still confuse similar-but-different products (false positives), especially if packaging words differ only slightly. Requires labeled data or careful threshold tuning. Performance depends on quality of text (missing descriptors or inconsistent naming can mislead the model). Also sensitive to numerical and unit mismatches unless specially handled.

## 3. Image-Based Matching

Another cue is the product image. Convolutional neural networks (CNNs) can encode visual features so that identical packaging yields similar embeddings. In some domains (clothing, furniture) image matching has proven effective. For groceries, images often vary (different lighting, angles, watermarks, or show partial packaging), making matching harder. Advanced methods like OpenAI’s CLIP learn joint image-text embeddings, which can handle diverse images. In practice, an image model can serve as a *tie-breaker*: if two textually-similar items also look alike, confidence increases; if they look different, it may flag an error.

**Approach:** Use a pretrained image encoder (ResNet, EfficientNet, or CLIP’s visual model) to compute an image vector for each product photo. Compute cosine similarity between images of candidate matches. High image similarity suggests a match.

**Pros:** Captures visual details that text misses; robust to different titles for identical packaging. Useful when product names are very generic or differ greatly.
**Cons:** Product photos from web scraping may have noise: inconsistent backgrounds, added labels, or low resolution. Packaging redesigns or multiple images per product complicate matching. CNNs are computationally heavy. As one blog notes, image similarity is “powerful” but typically requires fine-tuning to the exact use case. Also, identical-looking products (e.g. store-brand vs national brand) can deceive an image model. Overall, image matching alone is usually less reliable than text for grocery items, but it provides complementary evidence.

## 4. Hybrid Matching Pipeline

A practical system combines all signals in stages. **Priority order:**

1. **EAN/IDs first.** If a scraped product has a valid barcode or GS1 ID, look it up in the master catalog. Exact match = high confidence shadow product.
2. **Text similarity next.** If no ID, use the text-NLP model. Compute similarity of the new item’s title/attributes against existing shadow-product entries (indexed by category or brand for efficiency). If the top candidate exceeds a threshold, tentatively match them.
3. **Image validation.** Optionally, for candidates near the threshold or for high-value items, check image similarity. A high image score can bump confidence; a low score might veto a text match.
4. **Ensemble decision.** Combine these scores into a composite confidence. For example, treat EAN matches as 100% confidence, then use a weighted sum or learned logistic regression on text-sim and image-sim. If overall confidence is high, assign the match; if it’s low, mark it “uncertain” or as a new product.

A hybrid model maximizes coverage: barcodes ensure precise linking where available, while text+image handle all others. Many vendors take this approach. For instance, Price2Spy calls their hybrid method “Automatch” + human review, where IDs supply initial candidates and people verify them. An illustration of such a pipeline:

| **Step**                          | **Description**                                                                                                                                                 |
| --------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 1. **Data Ingestion**             | Scrape new products, parse titles, descriptions, brands, units, images. Normalize fields (e.g. convert weights). Store attributes in a database.                |
| 2. **Identifier Lookup**          | If a barcode/GTIN is present, search for a matching shadow product. If found, link immediately.                                                                 |
| 3. **Text Embedding**             | Encode title/description via a transformer (BERT/SBERT) or word-based model. Retrieve nearest neighbor products (e.g. using FAISS) within the same category.    |
| 4. **Image Embedding (Optional)** | Compute image vector for the new item. Compare with image vectors of candidate matches.                                                                         |
| 5. **Similarity Scoring**         | Combine the text similarity and image similarity into a single score. Possibly incorporate brand or attribute matches.                                          |
| 6. **Decision Threshold**         | If score > high threshold, auto-match to that shadow product. If score is moderate, flag for manual review. If below low threshold, create a new product entry. |
| 7. **Update Indexes**             | Add the new product’s embeddings to the search index for future matching.                                                                                       |

## Comparative Analysis of Methods

| **Method**           | **Pros**                                                                                                                                                                           | **Cons**                                                                                                                                               |
| -------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------ |
| **Identifier (EAN)** | + Unique and exact match when available<br>+ Simple and fast lookup                                                                                                                | – Often missing in scraped data<br>– Relies on manufacturer sharing<br>– Not all stores expose it                                                      |
| **Text (NLP)**       | + Utilizes available text fields (title/description/brand)<br>+ Captures semantic similarity (via embeddings)<br>+ Handles different naming conventions and languages (with mBERT) | – May mis-match similar items if text is ambiguous<br>– Sensitive to synonyms, typos, unit differences<br>– Requires heavy models (BERT) and tuning    |
| **Image (CV)**       | + Can match by visual packaging (useful if names differ)<br>+ Handles multilingual cases transparently                                                                             | – Product photos vary widely (angle, lighting, watermark)<br>– Computationally expensive<br>– Less effective for low-uniqueness items (e.g. plain box) |
| **Hybrid Ensemble**  | + Leverages all available signals<br>+ Fallback mechanisms improve coverage<br>+ Can tune confidence thresholds for desired precision/recall                                       | – Most complex to implement<br>– Requires combining heterogeneous models/logic<br>– Needs careful calibration to avoid cascading errors                |

## Recommended Approach

**Ensemble Model:** A multi-stage hybrid approach balances accuracy and scale. We recommend:

1. **Exact-ID Step:** Use EAN/GTIN matching wherever possible. This gives perfect precision for many grocery items.
2. **Text Embedding:** Encode product titles (and key attributes) using a Transformer model. In practice, a fine-tuned *Sentence-BERT* or multilingual BERT can serve; such models have been shown to greatly boost matching accuracy over older string methods. For example, Tracz et al. found that transformer-based similarity learning “significantly boosts performance” on product matching tasks. This model outputs a vector for each title; matches are found via cosine similarity in the vector space.
3. **Image Check:** Compute an image embedding (e.g. using CLIP or a product-trained CNN). Use it to double-check tricky cases. Width.ai reports that image similarity models “can learn the similarity between products no matter the angle, image quality, \[or] background”, though this requires fine-tuning on product images. In our context, use images to raise confidence when text is close but ambiguous.
4. **Scoring & Decision:** Combine scores (e.g. a weighted sum of text and image similarities, or a small neural/logistic model that takes both embeddings). To keep it scalable, precompute and index embeddings for existing products (e.g. via a vector DB) for fast lookup. Use approximate nearest-neighbor search (FAISS or ElasticSearch) for retrieval.

By using pretrained models (no full re-training needed) and approximate search, this design is scalable. It leans on the strong performance of transformer embeddings while falling back on IDs for quick matches.

## Confidence Scoring and Matching Thresholds

Each candidate match is assigned a **confidence score** between 0 and 1. For example:

* If EANs match exactly, confidence = 1.0 (full trust).
* Otherwise, use the model’s similarity score (cosine) or a calibrated probability. For instance, one can convert cosine similarity to a pseudo-probability (possibly via a logistic regression on a held-out validation set).
* Empirically determine thresholds: e.g., if text-sim > 0.9, auto-match; if 0.7–0.9, mark uncertain; below 0.7, treat as new. These values depend on the chosen model and desired precision/recall balance. Price2Spy notes that even “99%” match accuracy is not sufficient without verification, so it’s prudent to set conservative thresholds.

Confidence should also reflect **model ensemble**: if text and image both agree (both high similarity), the overall confidence increases; if they conflict, lower it. The system can maintain a single scalar score per candidate (for example, 0.6 from text + 0.4 from image = 1.0 total), or a learned classifier output. Calibration (e.g. Platt scaling) ensures this score is interpretable as likelihood of true match.

## Manual Review Workflow

To avoid erroneous matches, implement a human-in-the-loop process for low-confidence cases. All pairs with confidence below a high threshold (e.g. 0.95) should be **flagged for admin review**. The review UI should display the two product entries side by side, including images, full titles, brands, size/unit, and price. Administrators can then **confirm or reject** the match (or merge into an existing product).

A suggested UI/workflow:

* **Review Queue:** List all flagged matches with their confidence score. Admin can filter/sort (e.g. by lowest confidence).
* **Match Detail View:** Show Product A and Product B fields in columns, highlight differences (e.g. quantities or brand names). Include thumbnail images. Provide buttons “Accept as Match” or “Reject (Not Same Product)”.
* **Feedback Capture:** Each decision is logged. Accepted pairs become part of the training data; rejected ones are noted as true negatives.

This feedback loop is crucial. As Price2Spy emphasizes, **100% match quality** is the goal. Learning from corrections can improve the model over time (active learning). For example, newly confirmed matches can be added to the matching database or used to fine-tune the similarity model, raising future confidence on similar items.

**Summary:** A combined EAN + NLP + image approach with confidence scoring and human oversight offers the best trade-off. EANs provide high precision when present, transformers handle variation, and images add an orthogonal check. Tables below recap pros/cons and pipeline steps.

| **Approach**            | **Advantages**                                                                                                        | **Drawbacks**                                                                                                                     |
| ----------------------- | --------------------------------------------------------------------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------------------- |
| **EAN/ID Matching**     | • Exact, language-neutral matches<br>• Fast lookup                                                                    | • Often missing on websites<br>• Dependency on barcode database<br>• No match if ID absent                                        |
| **Text (NLP) Matching** | • Uses existing data fields<br>• Captures semantic context<br>• Handles multiple languages (with multilingual models) | • Ambiguous text can cause false positives<br>• Sensitive to synonyms, typos, unit variations<br>• Requires heavy models/training |
| **Image Matching**      | • Bypasses text ambiguity<br>• Useful for visually distinctive packaging                                              | • Scraped images vary in quality/format<br>• High computational cost (CNN inference)<br>• Less reliable if packaging changes      |
| **Hybrid Ensemble**     | • Combines all signals for robust matching<br>• Higher overall accuracy; partial cover-all strategy                   | • Complex to implement (multiple models)<br>• Needs careful tuning of weights/thresholds                                          |

| **Pipeline Step**                 | **Description**                                                                                                                               |
| --------------------------------- | --------------------------------------------------------------------------------------------------------------------------------------------- |
| **1. Scrape & Parse**             | Collect raw product data (title, description, brand, image, price) from each retailer. Normalize fields (e.g. unify units, remove stopwords). |
| **2. Identifier Lookup**          | If an EAN/UPC is found, query the product database. If a match exists, assign immediately; else, proceed.                                     |
| **3. Text-Embedding Similarity**  | Encode titles/descriptions with a pre-trained language model. Retrieve nearest neighbors (within same category/brand) by cosine similarity.   |
| **4. Image-Embedding Similarity** | (Optional) Compute image vectors (e.g. via CLIP or CNN). Compare the new image to images of candidate products.                               |
| **5. Score Computation**          | Combine text and image similarity into a composite score. Incorporate other features (brand match, unit match, price range).                  |
| **6. Thresholding & Match**       | If score ≥ high threshold, auto-match. If score is low, create new product. If intermediate, flag for review.                                 |
| **7. Human Review**               | Present low-confidence candidates to admins for confirmation (side-by-side UI with images and details). Admins mark true matches.             |
| **8. Update & Learn**             | Add confirmed matches to the catalog and optionally re-train or fine-tune the model on this feedback to improve future accuracy.              |

**Conclusion:** The most effective strategy is a **hybrid ensemble**: use EANs for exact links, and powerful NLP/image models to catch the rest. This multi-tiered pipeline balances precision (via IDs and strict thresholds) with recall (via semantic matching). Low-confidence cases are vetted by humans to ensure accuracy, consistent with best practices in data linking. Over time, administrator feedback can be used to refine the thresholds and models, moving the system closer to 100% correctness. The tables above summarize each method’s trade-offs and the proposed pipeline steps for robust supermarket product matching.
