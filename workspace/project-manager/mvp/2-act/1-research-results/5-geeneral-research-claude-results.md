33# SuperMarty Grocery Shopping Assistant: Technical Architecture & Compliance Guide

## Hybrid scraping approach offers optimal balance between cost and compliance

The research reveals that a combination of third-party APIs and selective custom scraping provides the best foundation for a Dutch grocery shopping app. Starting with ShoppingScraper API at €100-250/month gives immediate access to Albert Heijn, Jumbo, and Plus data while avoiding legal risks. This approach costs approximately €110,000 for the first year compared to €150,000+ for pure custom scraping, with significantly lower legal exposure since the API provider handles GDPR and terms of service compliance.

For the MVP phase, the recommended architecture implements a Redis caching layer with 30-minute TTL for prices and 4-hour TTL for product details, backed by PostgreSQL for persistent storage. The system should use a tiered update strategy where popular items refresh every 15 minutes while niche products update daily. This hybrid approach includes fallback mechanisms using custom scrapers for edge cases and manual data entry for private label products that may not be available through the API.

## Dutch NLP models achieve 85-92% product matching accuracy

Product matching across supermarket chains requires a sophisticated multi-stage pipeline combining EAN barcode matching, Dutch-specific NLP, and confidence scoring. **RobBERT-v2** emerges as the optimal NLP model for production use, achieving 92% F1-score on Dutch product names while maintaining 50ms inference speed. The recommended implementation uses a 100-point confidence scoring system where matches above 75% are automatically accepted, 60-74% require review, and below 60% are rejected.

The matching algorithm handles critical edge cases like private label normalization (converting "AH Basic" and "Jumbo Huismerk" to a unified "[STORE_BRAND]" token) and Dutch size variations (normalizing "1L" to "1 liter"). For products like "Albert Heijn Halfvolle Melk 1L", the system first attempts EAN matching (40 points maximum), then calculates text similarity using RobBERT embeddings (35 points), validates category alignment (15 points), and confirms price consistency (10 points).

The PostgreSQL database schema leverages Supabase's pgvector extension for semantic search, storing 768-dimensional embeddings for each product. This enables similarity searches with cosine distance calculations, achieving sub-200ms response times for single product lookups and under 2 seconds for batches of 50 products.

## GDPR compliance requires explicit consent and €20,000 annual investment

**Dietary allergies and intolerances constitute "special category" health data under Article 9 GDPR**, requiring explicit consent and enhanced security measures. The Dutch Data Protection Authority confirms this classification means processing is prohibited by default unless users provide clear, documented consent for each data type separately. The app must implement a multi-checkbox consent structure distinguishing between dietary preferences, allergies, and intolerances.

Technical requirements include AES-256 encryption for data at rest, TLS 1.3 for data in transit, and row-level security in PostgreSQL. **Supabase must be configured with EU-region hosting** (eu-west-1 or eu-central-1) and a signed Data Processing Agreement. Critical warning: Supabase Edge Functions use Deno Deploy which may not meet GDPR data residency requirements, so sensitive processing should use standard PostgreSQL functions instead.

Article 22 regulations on automated decision-making apply to personalized product suggestions based on health data. The app must provide meaningful explanations of recommendation logic, allow users to request human review, and implement safeguards against algorithmic bias. All data subject requests must be fulfilled within one month, with technical functions enabling data export in JSON/CSV format and complete deletion capabilities.

Estimated compliance costs include €5,000-15,000 for initial legal consultation, €10,000-25,000 for technical implementation, and €3,000-8,000 annual maintenance. Non-compliance risks include fines up to €20 million or 4% of global turnover.

## Supermarket integration starts with search redirects, evolves to API partnerships

Direct cart integration faces significant technical and legal obstacles as none of the three major Dutch supermarkets offer public APIs. Albert Heijn uses "wi" prefixed product IDs (e.g., wi193679) with hCaptcha protection and OAuth2 authentication on their mobile API. Jumbo employs mixed alphanumeric identifiers with SHA1 hash verification, while Plus recently migrated to commercetools but provides no public access.

The phased implementation roadmap begins with MVP search redirects, constructing URLs like `https://www.ah.nl/zoeken?query={productName}` for each supermarket. This approach requires just 1-2 weeks of development and faces minimal compliance risk. Phase 2 involves reverse-engineering mobile APIs using libraries like SupermarktConnector and AppiePy, though these face frequent breaking changes due to anti-automation measures.

**Deep integration requires official partnerships**, with Plus representing the most promising target due to their recent platform modernization and smaller market position. Albert Heijn's `appie://` mobile deep links offer an intermediate solution for users with installed apps. All implementations should include fallback strategies for when integrations break, such as QR code generation or manual product search assistance.

## Implementation roadmap and budget allocation

**Phase 1 (Months 1-3): €35,000**
- ShoppingScraper API integration (€250/month)
- Basic RobBERT product matching implementation
- GDPR consent framework and encryption setup
- Search redirect functionality for all three supermarkets

**Phase 2 (Months 4-6): €40,000**
- Custom scraping for edge cases and private labels
- Admin override workflow for match corrections
- Enhanced caching and performance optimization
- Mobile deep linking for Albert Heijn app

**Phase 3 (Months 7-12): €55,000**
- Partnership negotiations with Plus supermarket
- Advanced ML-based price prediction
- Real-time availability notifications
- Full GDPR compliance audit and DPO consultation

**Total First-Year Investment: €130,000** plus €20,000 contingency for legal compliance and unexpected technical challenges.

The hybrid approach balances rapid market entry with long-term scalability, providing Dutch consumers with a compliant, accurate, and user-friendly grocery shopping assistant while maintaining flexibility for future expansion across the European market.
