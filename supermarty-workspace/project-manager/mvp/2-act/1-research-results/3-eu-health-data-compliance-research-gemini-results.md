
# **Legal Brief: GDPR Compliance for Health Data Personalization in the SuperMarty Application**

## **Executive Summary**

### **Purpose and Scope**

This legal brief provides an exhaustive analysis of the General Data Protection Regulation (GDPR) requirements pertinent to the development and deployment of health-related personalization features within the SuperMarty application. The scope of this analysis is tailored to the application's target audience within the European Union (EU) and is intended to serve as a foundational, actionable guide for the product, development, and legal teams during the MVP 3 phase and for all subsequent iterations. It addresses the complete lifecycle of user health data, from initial collection and classification to automated processing and the fulfillment of data subject rights.

### **Key Findings**

A thorough review of the GDPR, relevant case law, and guidance from EU data protection authorities yields several critical conclusions for the SuperMarty application:

* **Data Classification:** All user-provided data intended for personalization features—including dietary goals, allergies, intolerances, age, weight, and activity level—unequivocally constitutes "special category data concerning health" as defined under GDPR Article 9\. This classification is based on both the explicit nature of the data and the health-related inferences the application's AI is designed to make.
* **Legal Basis:** The only viable legal basis for processing this special category data within a commercial application like SuperMarty is "explicit consent" under Article 9(2)(a). The standards for obtaining and managing this consent are exceptionally high and form the cornerstone of the feature's legal compliance.
* **Automated Decision-Making:** The use of an AI assistant to generate personalized dietary suggestions falls under the strict regulations of GDPR Article 22 concerning automated individual decision-making. This necessitates the implementation of specific, robust safeguards, most notably the right for a user to obtain meaningful human intervention and contest the AI's decisions.
* **Data Security and Residency:** The high-risk nature of the data mandates stringent technical and organizational security measures, including end-to-end encryption (e.g., AES-256) and strict access controls. Furthermore, to mitigate significant legal and financial risks associated with international data transfers, all EU user health data must be stored and processed exclusively within the EU or European Economic Area (EEA).
* **Compliance Documentation:** A Data Protection Impact Assessment (DPIA) is a mandatory prerequisite before launching the personalization features, due to the high-risk nature of the processing.

### **Strategic Recommendations**

Based on these findings, the following strategic actions are recommended to ensure compliance and mitigate risk:

1. **Prioritize Consent User Experience (UX):** Significant resources should be allocated to designing and implementing a granular, unbundled, and transparent consent mechanism. This is the single most critical compliance step and the primary foundation for lawful processing.
2. **Adopt a "Fortress" Security Model:** The development team must implement the prescribed technical and organizational measures (TOMs) with an unwavering focus on EU-only data storage and processing. This approach designs out the complexities and risks of international data transfer compliance.
3. **Build for User Rights from Inception:** The application's backend and frontend architecture must be engineered to facilitate all data subject rights (access, portability, erasure, etc.) as core user features. This "compliance by design" approach is more efficient and less risky than manual, ad-hoc fulfillment.
4. **Operationalize Human Review:** A clear, adequately resourced process for providing meaningful human review of AI-driven decisions must be established. This is an operational commitment that extends beyond a simple in-app button and requires qualified personnel.
5. **Conduct a DPIA Immediately:** The DPIA process should be initiated in parallel with development. This will allow for the proactive identification, assessment, and mitigation of data protection risks, ensuring they are addressed before the feature goes live.

## **Data Classification: The Implications of Processing "Special Category Data"**

### **A. Legal Foundation: Defining "Data Concerning Health"**

The GDPR establishes a tiered system for personal data, affording the highest level of protection to what it terms "special categories of personal data" in **Article 9(1)**.1 This heightened protection is due to the inherently sensitive nature of this information and the significant risks to individuals' fundamental rights and freedoms should it be compromised.3 Central to this category is "data concerning health."

The regulation provides a broad and encompassing definition in **Article 4(15)**, which states that "data concerning health" is any "personal data related to the physical or mental health of a natural person, including the provision of health care services, which reveal information about his or her health status".5 This definition is not limited to data originating from a clinical setting.

Further clarification is provided by **Recital 35**, which expands the scope to include "all data pertaining to the health status of a data subject which reveal information relating to the past, current or future physical or mental health status of the data subject".7 This forward-looking element is particularly relevant for SuperMarty, as it explicitly covers data related to health goals and potential future health states, not just diagnosed conditions. Regulatory bodies, such as the UK's Information Commissioner's Office (ICO), consistently interpret this definition broadly, confirming that it applies to a wide spectrum of information, from a formal medical diagnosis to data generated by a consumer fitness or nutrition app.3

### **B. Application to SuperMarty: Direct and Inferred Health Data**

For the SuperMarty application, the data collected for its personalization features falls into two categories, both of which are subject to the strictures of Article 9\.

**Direct Health Data:** Certain data points provided by the user are unambiguously "data concerning health." Information about food allergies (e.g., "peanut allergy") and intolerances (e.g., "lactose intolerant") directly reveals information about a person's physiological and immune system responses, placing it squarely within the Article 4(15) definition.10 Legal advice provided to organizations in other contexts confirms that allergen data is considered special category health data requiring explicit consent for processing.12

**Inferred Health Data:** This category presents a more nuanced but equally critical compliance challenge. The GDPR's definition of health data is not limited to what a user explicitly states but extends to what can be inferred from the data collected. The ICO's guidance is dispositive on this point: if an organization processes data with the *intent* to make an inference linked to a special category, or to treat someone differently based on such an inference, that processing falls under Article 9\.3

The very purpose of SuperMarty's AI assistant is to analyze a collection of data points to infer a user's health status and needs. Data points such as dietary goals ("weight loss," "manage diabetes"), age, weight, height, and activity level, when processed in combination, are used to create a detailed health profile. For instance, combining a user's weight, height, and a stated goal of "weight loss" allows the application to calculate their Body Mass Index (BMI) and infer a health status such as "overweight" or "obese".9 This inference is itself "data concerning health." The AI assistant functions as an inference engine, transforming seemingly non-clinical data into a sensitive health profile through the act of processing. The legal obligations are therefore triggered not merely by the user's input, but by the conclusions the system is designed to draw about them.

**Conclusion:** All data points collected for the SuperMarty personalization feature—whether direct (allergies, intolerances) or inferential (goals, weight, height, age, activity level)—must be treated as a single, unified set of "special category data" under Article 9\. There can be no distinction in the level of protection applied across this dataset.

### **C. Actionable Guidance & Recommendations**

To ensure compliance with this classification, the following measures are necessary:

* **Do:**
    * Treat every piece of data collected for the personalization feature with the highest standard of care applicable to Article 9\.
    * Explicitly document this classification in the organization's Record of Processing Activities (RoPA) as required by Article 30\.
    * Conduct mandatory training for all developers, product managers, and data scientists to ensure they understand that even seemingly innocuous "lifestyle" data becomes sensitive special category data in the context of this processing activity.
* **Don't:**
    * Do not create a tiered system of protection where declared allergies are treated as more sensitive than dietary goals or weight. All are part of a single, high-risk dataset.
    * Do not collect any data "just in case" it might be useful for future, undefined features. The principle of data minimization—collecting only what is strictly necessary for the specified purpose—is paramount when processing special category data and serves as a critical risk-mitigation strategy.2

To provide absolute clarity for all internal teams, the following classification table should be adopted as a foundational document for the DPIA and all development work.

| Data Point | Example Value | GDPR Classification | Justification for Classification | Inferred Health Information | Risk Level |
| :---- | :---- | :---- | :---- | :---- | :---- |
| Allergy | "Peanuts" | Art. 9 Special Category (Health) | Directly reveals a specific immune system condition with potentially severe health consequences.10 | Anaphylaxis risk, immune system status. | Very High |
| Intolerance | "Lactose" | Art. 9 Special Category (Health) | Reveals a physiological condition related to the digestive system that affects physical health.10 | Digestive health status, metabolic function. | High |
| Dietary Goal | "Weight Loss" | Art. 9 Special Category (Health) | When combined with other metrics, it reveals information about a user's current or desired health status and potential underlying conditions.3 | Potential overweight/obesity status, metabolic health goals. | High |
| Weight/Height | "95 kg / 1.8m" | Art. 9 Special Category (Health) | These are key metrics used to calculate Body Mass Index (BMI), a direct and widely used indicator of health status.14 | BMI, body composition, cardiovascular risk factors. | High |
| Age | "45" | Personal Data (Art. 4), becomes Art. 9 in context | A fundamental factor in assessing health risks, nutritional requirements, and the likelihood of age-related conditions. | Age-related health risks (e.g., metabolic syndrome, heart disease). | High |
| Activity Level | "Sedentary" | Art. 9 Special Category (Health) | Reveals critical information about a user's lifestyle and its direct impact on their physical health and disease risk.9 | Cardiovascular health risk, metabolic rate. | High |

## **Establishing a Lawful Basis: The Centrality of Explicit Consent**

### **A. Legal Foundation: Why Explicit Consent is the Only Option**

The processing of special category data is, by default, prohibited under **Article 9(1)** of the GDPR. This prohibition can only be lifted if the data controller can satisfy one of the specific exceptions enumerated in **Article 9(2)**.1 A careful evaluation of these exceptions reveals that for a commercial, direct-to-consumer application like SuperMarty, only one is viable.

A review of the other potentially relevant exceptions demonstrates their inapplicability:

* **Article 9(2)(h) \- Health or social care:** This exception applies to processing necessary for medical diagnosis or the provision of health care, where the data is processed by or under the responsibility of a professional subject to an obligation of secrecy, such as a doctor or hospital.4 SuperMarty is a commercial technology platform, not a registered healthcare provider, and its employees are not health professionals in a therapeutic relationship with the user. Therefore, this exception does not apply.18
* **Article 9(2)(i) \- Public health:** This exception is reserved for processing necessary for reasons of public interest in the area of public health, such as protecting against serious cross-border threats to health.1 It is not designed for and cannot be used to justify a commercial personalization service.
* **Article 9(2)(j) \- Archiving, research, or statistical purposes:** While the data collected by SuperMarty could have secondary research value, the *primary purpose* of the processing is to deliver a personalized service to the individual user. The research exception cannot be used as a lawful basis for this primary operational purpose.20

This process of elimination leaves **Article 9(2)(a) \- Explicit consent** as the only appropriate and legally defensible lawful basis for SuperMarty's health personalization features.2

### **B. The Anatomy of "Explicit" Consent under GDPR**

"Explicit consent" is a higher bar than the standard of consent required for non-sensitive personal data. While the GDPR does not provide a formal definition of "explicit," guidance from regulators and the conditions outlined in **Article 7** make its requirements clear. It must be a specific, direct, and unambiguous statement from the user agreeing to the processing of their named special category data for a named purpose.22

The core components of valid explicit consent are:

* **Freely Given (Art. 7(4)):** The user must have a genuine, free choice. Consent is not considered freely given if there is a clear imbalance of power between the user and the controller, or if the provision of a service is made conditional on consent to processing that is not strictly necessary for that service.24 For SuperMarty, this means a user must be able to refuse consent for the personalization features and still be able to use the core functionality of the app (i.e., as a standard online supermarket). Making access to the entire app conditional on consenting to health data processing would invalidate the consent.26 This architectural decision is a powerful way to mitigate the risk of a regulator finding a "power imbalance" that would otherwise taint the consent, a concern often raised in health-related contexts.21
* **Specific:** Consent must be obtained for distinct, specified purposes. A single, bundled request for "data processing" is invalid. The principle of granularity requires separate consent for separate processing operations.28 For SuperMarty, this means seeking separate, un-ticked opt-ins for:
    1. The core purpose: Processing health data to provide personalized dietary suggestions.
    2. Any secondary purpose, such as using anonymized data for internal research and development to improve the AI model.
    3. Any other purpose, such as sending marketing communications about health-related products.
* **Informed:** Before giving consent, the user must be provided with clear, concise, and easily understandable information about the processing. This must include, at a minimum: the controller's identity, the specific types of health data being collected, the precise purposes of the processing, the existence of their right to withdraw consent at any time, and information about any automated decision-making involved.23 This information must be presented in a way that is clearly distinguishable from other text, such as the general terms and conditions.25
* **Unambiguous (by a clear affirmative action):** Consent must be given through an active, opt-in motion. The GDPR and regulatory guidance are unequivocal that pre-ticked boxes, silence, scrolling, or continued use of the service do not constitute valid consent.24 The user must take a deliberate action, such as ticking an unchecked box or clicking an "I Agree" button, to signify their agreement.
* **Easily Withdrawn:** Article 7(3) mandates that it must be as easy for a user to withdraw their consent as it was to give it.24 This requires a clear, persistent, and accessible mechanism within the application's settings menu, allowing a user to revoke their consent at any time.

### **C. Actionable Guidance: Designing a Compliant Consent Workflow**

To meet these stringent requirements, a multi-step, user-centric consent workflow must be implemented.

* **Consent UI/UX Workflow Template:**
    * **Step 1: The Invitation (Uncoupled from Core Service):** Upon first encountering the personalization feature, the user is presented with a choice that does not lock them out of the main application.
        * *Headline:* "Unlock Personalized Suggestions\!"
        * *Body Text:* "To help you find the best products for your health goals, SuperMarty can create personalized dietary suggestions. This feature requires you to share sensitive health information. Would you like to set up your health profile?"
        * *Buttons:* /
    * **Step 2: The Just-in-Time Consent Request:** If the user opts in, this screen appears immediately *before* any data entry fields are shown. It is dedicated solely to obtaining consent.
        * *Headline:* "Your Health, Your Data, Your Choice"
        * *Plain Language Explanation:* "To provide you with personalized suggestions, we need your explicit consent to collect and process the health information you provide (like allergies, dietary goals, and weight). Our AI assistant uses this data to recommend suitable products. You are always in control and can change your mind or withdraw your consent at any time in your profile settings."
        * *Link to Full Privacy Notice:* "For full details on how we protect your data, please read our."
        * **Granular Consent Checkboxes (all unticked by default):**
            * \[ \] **I explicitly consent** to SuperMarty collecting and processing my health data (including allergies, intolerances, dietary goals, weight, height, age, and activity level) for the specific purpose of providing me with personalized dietary and product suggestions. (This is mandatory to proceed with the feature).
            * \[ \] (Optional) I agree that my health data may be anonymized and used in aggregate for internal research and development to help SuperMarty improve its AI models and for general health trend analysis.
        * **Affirmative Action Button:** \`\`
* **Do's:**
    * Use a layered information approach: provide a simple, clear explanation on the consent screen with a direct link to the more detailed privacy notice.24
    * Maintain robust consent records. The system must log the user's unique ID, the specific version of the consent text they agreed to, a precise timestamp, and a record of which specific checkboxes they ticked.28 This is crucial for demonstrating compliance under the accountability principle.
    * Design the withdrawal mechanism to be as simple as the consent process—for example, a "Manage Consents" section in the app settings where the user can simply un-tick the boxes.
* **Don't:**
    * Do not bundle the request for health data consent within the general Terms of Service or any other agreement.25 It must be a distinct, separate action.
    * Do not use pre-ticked checkboxes or any other form of default opt-in.25
    * Do not use vague or ambiguous language such as "to improve your experience" or "for personalization." Be specific about the purpose.26

## **Data Security and Storage: Technical and Organizational Mandates**

### **A. Legal Foundation: Article 32 and Privacy by Design**

The GDPR places a significant emphasis on the security of personal data, particularly when it involves high-risk processing of special categories. The legal obligations are primarily rooted in two articles.

**Article 32 (Security of Processing)** is the central provision, mandating that controllers and processors implement "appropriate technical and organisational measures" (TOMs) to ensure a level of security that is appropriate to the risk.32 The article explicitly mentions pseudonymization and encryption as examples of such measures. Given that SuperMarty will be processing special category health data on a large scale, the risk is inherently high, and therefore the most robust and state-of-the-art security measures are required, not merely suggested.15

**Article 25 (Data Protection by Design and by Default)** complements this by requiring that data protection principles are embedded into the very architecture of systems and processes from the outset.34 Security cannot be a feature that is added on later; it must be a foundational component of the application's design.

### **B. Required Technical and Organizational Measures (TOMs)**

Based on Article 32 and best practices for securing health data, the following TOMs are mandatory for SuperMarty:

* **Encryption:** This is a fundamental and non-negotiable control.
    * **Data in Transit:** All data transmitted between the user's device, the application servers, and any internal services must be encrypted using a strong, modern cryptographic protocol such as **Transport Layer Security (TLS) 1.3**.15
    * **Data at Rest:** All personal data, especially the health data profiles, must be encrypted when stored in databases, file systems, backups, or any other persistent storage medium. The industry standard for this is the **Advanced Encryption Standard with a 256-bit key (AES-256)**.15
* **Pseudonymization:** As defined in Article 4(5), pseudonymization involves processing personal data in such a manner that it can no longer be attributed to a specific individual without the use of additional, separately stored information.32 For SuperMarty, a robust pseudonymization strategy would involve storing the sensitive health profiles (allergies, goals, biometrics) in a logically and physically separate database from the user's directly identifying information (name, email address, account credentials). The link between these two datasets should be a randomly generated, non-identifying key or token.
* **Access Control:** Strict controls must be in place to limit who can access the data.
    * **Role-Based Access Control (RBAC):** Implement a granular RBAC system where employees are granted access only to the data necessary to perform their job functions (the principle of least privilege).15 For example, a customer support agent should not have default access to a user's health data. Access should only be granted on a case-by-case basis for a specific support issue, and this access must be temporary and fully logged.
    * **Multi-Factor Authentication (MFA):** All employees and administrators accessing internal systems that contain or provide a path to personal data must be required to use MFA.15
    * **Comprehensive Audit Logging:** The system must maintain detailed and immutable audit logs that record every instance of access to personal data, including who accessed it, when the access occurred, and what actions were taken.15
* **System Resilience and Integrity:**
    * **Regular Security Testing:** The application and its infrastructure must undergo regular, systematic security assessments, including automated vulnerability scanning and annual third-party penetration tests, to identify and remediate weaknesses.41
    * **Incident Response Plan:** A formal, documented Incident Response Plan must be in place to ensure the organization can effectively detect, respond to, and report a data breach. This plan must incorporate the GDPR's requirement to notify the relevant supervisory authority within 72 hours of becoming aware of a breach (Article 33).39
    * **Backup and Recovery:** The organization must have robust backup and disaster recovery processes to fulfill the Article 32(1)(c) requirement to "restore the availability and access to personal data in a timely manner in the event of a physical or technical incident".32
* **Organizational Measures:**
    * **Staff Training:** All employees, particularly those in development, product, and customer support roles, must receive regular and mandatory data protection and security training.42
    * **Formal Policies:** A comprehensive set of internal policies, including a Data Protection Policy, an Information Security Policy, and a Breach Notification Protocol, must be developed, approved, and disseminated.41
    * **Vendor Management:** All third-party service providers (processors) who may have access to personal data must be rigorously vetted. Legally binding **Data Processing Agreements (DPAs)** compliant with Article 28 must be in place with every vendor.41

### **C. Data Residency and International Transfers**

The GDPR imposes strict rules on the transfer of personal data outside the EU/EEA, as outlined in Chapter V. While it does not mandate absolute data localization, the practical effect for high-risk data is often the same.43

Transfers are only permitted to countries that the European Commission has deemed to provide an "adequate" level of data protection, or where the controller has put in place "appropriate safeguards," such as Standard Contractual Clauses (SCCs). The United States does not have an adequacy decision.44 The EU-U.S. Data Privacy Framework, while in place, is a successor to previous frameworks that were invalidated by the Court of Justice of the European Union (CJEU) in the

*Schrems* cases. These invalidations were based on the finding that U.S. surveillance laws are not "essentially equivalent" to the fundamental rights protections afforded in the EU.

The record-breaking fine of €1.2 billion levied against Meta for its transfers of EU user data to the U.S. serves as a stark warning of the extreme legal and financial risks involved, especially for sensitive data.44 Attempting to justify the transfer of special category health data to the U.S. using SCCs would require a complex and legally precarious Transfer Impact Assessment (TIA), which would likely fail to demonstrate adequate protection.

For a new feature involving sensitive health data, the only legally robust and low-risk strategy is to design out the transfer risk entirely. This means ensuring that all personal data from EU users is stored and processed exclusively on servers physically located within the borders of the EU or EEA.15 This is not merely a hosting choice; it is a fundamental architectural and risk management decision that simplifies compliance, reduces legal exposure, and demonstrates a serious commitment to protecting user data.

To provide a clear and actionable checklist for the technical teams, the following table outlines the mandatory TOMs.

| Measure Category | Specific Control | Technical Implementation Example | GDPR Article | Priority |
| :---- | :---- | :---- | :---- | :---- |
| **Encryption** | Encryption in Transit | Enforce TLS 1.3 or higher for all API and client-server communication, with no support for legacy protocols. | Art. 32(1)(a) | High |
|  | Encryption at Rest | Utilize AES-256 to encrypt all databases, object storage (e.g., S3 buckets), and automated backups. Manage encryption keys securely. | Art. 32(1)(a) | High |
| **Access Control** | Role-Based Access Control (RBAC) | Define strict roles (e.g., 'Developer', 'Support Agent', 'Nutritionist') in the Identity and Access Management (IAM) system with minimum necessary privileges. | Art. 32(2) | High |
|  | Audit Logging | Log all access to personal data, including user ID, timestamp, data accessed, and action taken. Store logs in a secure, immutable format (e.g., AWS CloudTrail). | Art. 32(1)(b) | High |
|  | Multi-Factor Authentication (MFA) | Mandate MFA for all internal systems containing or providing access to personal data, including cloud provider consoles and internal dashboards. | Art. 32(1)(b) | High |
| **Pseudonymization** | Data Separation | Store health profiles (allergies, goals) in a separate database from identity data (name, email), linked only by a non-identifying pseudonymized key. | Art. 32(1)(a) | High |
| **Resilience** | Incident Response Plan | Documented plan for detecting, responding to, and reporting a data breach within 72 hours. Conduct regular tabletop exercises and drills. | Art. 32(1)(c), Art. 33 | High |
|  | Regular Testing | Conduct quarterly automated vulnerability scans of all production infrastructure and annual third-party penetration tests of the application and APIs. | Art. 32(1)(d) | Medium |
| **Data Residency** | EU/EEA Hosting | Configure all cloud services (e.g., AWS, Azure, GCP) to store and process data exclusively in EU regions (e.g., eu-west-1, eu-central-1). Verify that no sub-processors transfer data outside the EU. | Art. 44-46 | High |

## **Automated Decision-Making: Navigating Article 22 with AI-Powered Suggestions**

### **A. Legal Foundation: The Scope of Article 22**

GDPR **Article 22(1)** provides individuals with a qualified right "not to be subject to a decision based *solely* on automated processing, including profiling, which produces *legal effects* concerning him or her or *similarly significantly affects* him or her".46 Understanding the key terms in this provision is essential to determining its application to SuperMarty.

* **"Solely" Automated:** This term refers to a decision made without any meaningful human involvement.49 If a human simply "rubber-stamps" the output of an automated system without conducting a genuine review and having the authority to change the outcome, the decision is still considered "solely" automated. The intervention must be substantive, not a token gesture.
* **"Legal or Similarly Significant Effect":** A "legal effect" is one that impacts a person's legal rights, such as the termination of a contract. A "similarly significant effect" is less precise but is interpreted by regulators to include decisions that have a serious impact on an individual's circumstances, behavior, or choices.51 Examples provided in guidance include decisions affecting access to credit, employment opportunities, or health services.46

For SuperMarty, the AI-generated dietary suggestions and meal plans are based on sensitive health data. An incorrect recommendation—for example, one that fails to account for a severe allergy or a medical condition like diabetes—could have a direct and significant impact on the user's physical health and well-being. Therefore, a conservative and legally prudent approach is to assume that these automated decisions have a "similarly significant effect" on the user, bringing the processing squarely within the scope of Article 22\.52

### **B. Compliance Pathway: Exceptions and Safeguards**

The general prohibition on this type of automated decision-making in Article 22(1) is not absolute. **Article 22(2)** provides three exceptions that can legitimize the processing 47:

a) The decision is necessary for entering into or performing a contract.  
b) The decision is authorized by Union or Member State law.  
c) The decision is based on the data subject's explicit consent.  
For SuperMarty, a commercial application, the only applicable exception is **(c) the data subject's explicit consent**.48 This is further reinforced by

**Article 22(4)**, which states that when such decisions are based on special categories of personal data (which is the case here), the processing is only permissible on the grounds of "explicit consent" or "substantial public interest." This eliminates any ambiguity and confirms that explicit consent is the sole compliance pathway.47

However, relying on this exception comes with a critical condition. **Article 22(3)** mandates that when using explicit consent, the controller *must* implement "suitable measures to safeguard the data subject's rights and freedoms and legitimate interests." At a minimum, these safeguards must include the right for the user to **obtain human intervention**, to **express his or her point of view**, and to **contest the decision**.47

### **C. Actionable Guidance: Implementing Article 22 Safeguards**

To comply with these requirements, SuperMarty must integrate specific features and processes into its application and operations.

* **Transparency:**
    * The privacy notice and the just-in-time consent screen must explicitly and clearly inform the user that they will be subject to automated decision-making, including profiling, for the purpose of generating personalized suggestions.
    * This information must include "meaningful information about the logic involved, as well as the significance and the envisaged consequences" of the processing for the user (Article 13(2)(f)).54 This does not require disclosing the full algorithm, but it does require a simple, high-level explanation, such as: "Our AI assistant analyzes your health profile (goals, biometrics, allergies) and compares it with nutritional data and established dietary principles to recommend products and meal plans that are a good match for you."
* **In-App Rights Facilitation:** The user interface must provide clear, simple, and accessible ways for users to exercise their Article 22 rights.
    * **Request Human Intervention:** Next to any AI-generated meal plan or significant dietary recommendation, there should be a clearly labeled button or link, such as "Request Review by a Nutritionist."
    * **Express Point of View / Contest Decision:** The application should include a dedicated feedback mechanism, such as a structured form or a chat interface, allowing a user to contest a recommendation and explain why. For example, a user could state, "This suggestion is not suitable for me because it includes too much red meat," or "This meal plan seems to ignore my stated preference for plant-based protein."
* **Backend Process and Operational Commitment:**
    * A documented internal procedure must be established to handle these requests efficiently and effectively.
    * Crucially, the "human intervention" must be meaningful. The review cannot be performed by a standard customer service agent reading from a script. It must be conducted by an individual who has the necessary competence and authority to understand the context and override the automated decision.49 For a dietary application, this almost certainly requires a qualified nutritionist or registered dietitian.
    * This requirement is not simply a technical feature to be built but an ongoing operational capability that must be resourced. The business must budget for this human review function as a core operational cost of offering the AI-powered feature. The feasibility, cost, and service-level agreements (SLAs) for this review process are critical components that must be assessed and documented in the mandatory DPIA.

## **Upholding Data Subject Rights: Operationalizing User Control**

### **A. Legal Foundation: User Rights under GDPR Chapter 3**

Chapter 3 of the GDPR grants individuals a powerful suite of rights, designed to provide them with genuine control over their personal data.55 As the data controller, SuperMarty has a legal obligation to establish clear, accessible, and efficient procedures to facilitate the exercise of these rights.

Key operational requirements for handling these requests, known as Data Subject Access Requests (DSARs), include:

* **Response Timeframe:** The standard deadline for responding to a request is **one month** from the date of receipt. This can be extended by two further months for particularly complex or numerous requests, but the individual must be informed of the extension and the reasons for it within the initial one-month period.57
* **No Fee:** In most cases, requests must be handled free of charge. A fee can only be charged if a request is "manifestly unfounded or excessive," a high threshold to meet.57
* **Identity Verification:** The organization must take reasonable steps to verify the identity of the person making the request to ensure data is not disclosed to the wrong person. However, this process must be proportionate and should not place an unnecessary burden on the user.58

### **B. Procedures for Handling Key Data Subject Rights**

SuperMarty must be prepared to handle the following key rights for its health data personalization feature:

* **Right to be Informed (Art. 13 & 14):** This right is primarily fulfilled proactively through the clear, layered, and granular privacy notice and consent mechanism detailed in Section III of this brief.
* **Right of Access (Art. 15):** This gives users the right to obtain confirmation that their data is being processed, and to receive a copy of all the personal data held about them, along with supplementary information (e.g., purposes of processing, categories of data, retention periods, recipients of the data).59
    * **Procedure:** A robust, automated process must be in place to compile all of a specific user's data from various systems—including their identity information, their full health profile, usage logs, AI-generated recommendations, and any support interactions—into a single, coherent, and readable package.
* **Right to Rectification (Art. 16):** This is the right for users to have inaccurate personal data corrected, or to have incomplete data completed.59
    * **Procedure:** The application must provide user-editable fields for all self-declared information (e.g., weight, goals, preferences). For any data that cannot be edited directly, a clear and responsive support channel must be available to process rectification requests.
* **Right to Erasure / "Right to be Forgotten" (Art. 17):** This right allows users to request the deletion of their personal data without undue delay under specific circumstances. The most relevant grounds for SuperMarty are when a user withdraws the consent upon which the processing is based, or when the data is no longer necessary for the purpose for which it was collected.59
    * **Procedure:** A "Delete Account" function within the app must trigger a process for the complete and irreversible deletion of the user's personal data from all production systems. This process should also add the user to a suppression list to prevent accidental re-contact. While there are exceptions to this right (e.g., for compliance with a legal obligation or for the defense of legal claims), these are unlikely to apply to the majority of SuperMarty's user data.60
* **Right to Data Portability (Art. 20):** This is a particularly important right in the context of digital services. It empowers users to obtain their personal data in a "structured, commonly used and machine-readable format" and gives them the right to transmit that data to another controller without hindrance.56
    * **Procedure:** This right goes beyond the Right of Access. The data must be provided in a format that is not just human-readable but is also structured for easy reuse by another service (e.g., JSON, XML, or CSV). This requires specific engineering to create a data export function that packages the user's health profile and activity history in a portable format.

### **C. Actionable Guidance: Building for Rights by Design**

To ensure compliance and operational efficiency, data subject rights must be treated as core product features, not as administrative burdens.

* Develop detailed internal playbooks and provide training to all customer-facing staff on how to recognize, log, and escalate a DSAR.58
* Implement technical solutions that automate the fulfillment of these rights wherever possible. A "compliance by design" approach is far more scalable and less error-prone than relying on manual fire drills for every request.

The following table translates these legal rights into concrete technical specifications for the product and engineering teams.

| Data Subject Right | Required In-App Functionality | Required Backend Procedure |
| :---- | :---- | :---- |
| **Right of Access (Art. 15\)** | A "Request My Data" button in the user's account settings. The UI should inform the user that the process may take up to 30 days. | A script that queries all relevant databases (user profiles, health data, activity logs) for a given user ID and compiles the data into a human-readable and electronic format (e.g., a zip file containing JSON files). |
| **Right to Rectification (Art. 16\)** | Editable fields in the user profile for name, email, weight, goals, allergies, etc. A clear link to customer support for correcting other data. | Standard CRUD (Create, Read, Update, Delete) operations on the user database, with all changes logged for audit purposes. |
| **Right to Erasure (Art. 17\)** | A "Delete My Account and All Data" button with a clear confirmation step explaining that the action is permanent and irreversible. | A script that triggers a hard delete of the user's personal data across all production systems. The process should also create a suppression list entry (e.g., a hashed email) to ensure compliance with the erasure request. |
| **Right to Data Portability (Art. 20\)** | An "Export My Data" button that allows the user to download their health profile and logged activities in a structured, machine-readable format (JSON is the recommended standard). | An API endpoint that, upon authenticated request, generates a structured JSON file containing all personal data the user has provided or that has been generated through their activity. |
| **Right to Withdraw Consent (Art. 7\)** | A clear "Manage Consents" or "Privacy Settings" section where users can easily view their current consent status and un-tick the consent boxes they previously ticked. | Toggling consent off must immediately cease the processing for that specific purpose (e.g., stop generating personalized suggestions). This action should be logged. It may also trigger the erasure process if no other legal basis remains for holding the data. |

## **Overarching Compliance Obligations and Future Outlook**

### **A. Data Protection Impact Assessment (DPIA)**

A DPIA is a process designed to help identify and minimize the data protection risks of a project. It is a key part of the accountability principle under the GDPR.

* **Legal Requirement:** According to **Article 35**, a DPIA is a mandatory requirement for any processing that is "likely to result in a high risk to the rights and freedoms of natural persons".22 The GDPR and guidance from data protection authorities explicitly list several types of processing that automatically trigger this requirement. The SuperMarty personalization feature meets at least two of these triggers:
    1. Processing of special category data (health data) on a large scale.34
    2. Use of new technologies (AI/machine learning) for profiling and automated decision-making that has a significant effect on individuals.35
* **Actionable Guidance:** SuperMarty *must* conduct and document a comprehensive DPIA *before* the health personalization features are launched. This is not an optional step. The DPIA must, at a minimum:
    * Describe the nature, scope, context, and purposes of the processing.
    * Assess the necessity and proportionality of the processing operations.
    * Identify and assess the risks to the rights and freedoms of users (e.g., risks from inaccurate recommendations, data breaches, discrimination).
    * Define the measures envisaged to address and mitigate those risks (e.g., the TOMs, consent mechanisms, and Article 22 safeguards identified throughout this brief).

### **B. Record of Processing Activities (RoPA)**

* **Legal Requirement:** Under **Article 30**, all data controllers are required to maintain a detailed record of their data processing activities.65 This is a core accountability document that must be made available to supervisory authorities upon request.
* **Actionable Guidance:** The organization's RoPA must be updated with a new, specific entry for the health data personalization feature. This entry must detail: the specific purpose (personalized dietary suggestions), the categories of data subjects (EU app users), the categories of data processed (special category health data, including allergies, goals, biometrics), the lawful basis (explicit consent), any data transfers (and the safeguards in place), data retention schedules, and a high-level description of the technical and organizational security measures (TOMs).

### **C. Future Outlook: The European Health Data Space (EHDS)**

It is crucial to look beyond immediate compliance and consider the evolving regulatory landscape for digital health in the EU. The most significant development is the **European Health Data Space (EHDS) Regulation**, which was approved by the European Parliament in April 2024\.66

* **The Trend:** The EHDS aims to create a harmonized framework across the EU to empower individuals with greater control over their electronic health data while simultaneously facilitating the secondary use of this data for research, innovation, and public policy under strict, regulated conditions.66
* **Key Features:** The EHDS will establish national **Health Data Access Bodies (HDABs)** to act as gatekeepers for requests to access health data for secondary purposes. It clarifies controller and processor roles and provides a legal basis for such secondary use, though Member States retain the right to impose stricter measures for highly sensitive data like genetic information.20 The regulation is expected to become fully applicable around 2028\.66

This development is not a distant concern but a strategic consideration for today's architectural decisions. The EHDS signals a future where data interoperability, structured data formats, and robust, granular consent for secondary use will be the norm. Organizations that build their data architecture with this future in mind will hold a significant strategic advantage. Those with poorly structured data and bundled, ambiguous consent models will face substantial technical and legal barriers to participating in this new data ecosystem.

* **Actionable Guidance:**
    * **Data Governance:** Implement a strong internal data governance framework from day one. This includes documenting data schemas, maintaining a comprehensive data dictionary, and using standardized data formats where feasible.
    * **Consent for Research:** The inclusion of an optional, granular consent checkbox for R\&D purposes (as detailed in Section III) is a crucial first step. It builds a foundation of user data that is ethically and legally sound, potentially allowing SuperMarty to contribute to valuable research in the future, in full compliance with the principles of the EHDS.
    * **Monitor EHDS Developments:** The legal and compliance team should be tasked with actively monitoring the implementation of the EHDS Regulation and any forthcoming guidance from the European Data Protection Board (EDPB). This will ensure that SuperMarty remains ahead of the curve and can adapt its strategies as the new framework takes shape.20 By architecting for this future, SuperMarty positions itself not as a compliance laggard, but as a trustworthy and forward-thinking leader in the digital health landscape.

#### **Works cited**

1. Art. 9 GDPR – Processing of special categories of personal data, accessed June 17, 2025, [https://gdpr-info.eu/art-9-gdpr/](https://gdpr-info.eu/art-9-gdpr/)
2. GDPR Article 9: Special Personal Data Categories and How to Protect Them | Exabeam, accessed June 17, 2025, [https://www.exabeam.com/explainers/gdpr-compliance/gdpr-article-9-special-personal-data-categories-and-how-to-protect-them/](https://www.exabeam.com/explainers/gdpr-compliance/gdpr-article-9-special-personal-data-categories-and-how-to-protect-them/)
3. What is special category data? | ICO, accessed June 17, 2025, [https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/lawful-basis/special-category-data/what-is-special-category-data/](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/lawful-basis/special-category-data/what-is-special-category-data/)
4. Sensitive personal data \- special category under the GDPR \- Data Privacy Manager, accessed June 17, 2025, [https://dataprivacymanager.net/sensitive-personal-data-special-category-under-the-gdpr/](https://dataprivacymanager.net/sensitive-personal-data-special-category-under-the-gdpr/)
5. Art. 4 GDPR – Definitions \- General Data Protection Regulation (GDPR), accessed June 17, 2025, [https://gdpr-info.eu/art-4-gdpr/](https://gdpr-info.eu/art-4-gdpr/)
6. Data concerning health \- Practical Law, accessed June 17, 2025, [https://uk.practicallaw.thomsonreuters.com/w-014-8175?transitionType=Default\&contextData=(sc.Default)](https://uk.practicallaw.thomsonreuters.com/w-014-8175?transitionType=Default&contextData=\(sc.Default\))
7. Recital No.35 \- UK GDPR \- Mishcon de Reya, accessed June 17, 2025, [https://www.mishcon.com/uk-gdpr/recital/no-35](https://www.mishcon.com/uk-gdpr/recital/no-35)
8. Recital 35 | Health data \- General Data Protection Regulation (GDPR) \- VeraSafe, accessed June 17, 2025, [https://gdpr.verasafe.com/recital-35/](https://gdpr.verasafe.com/recital-35/)
9. GDPR for digital health: developing EU privacy-compliant apps, accessed June 17, 2025, [https://www.chino.io/post/do-fitness-tracking-apps-need-to-be-complied-with-data-protection-law](https://www.chino.io/post/do-fitness-tracking-apps-need-to-be-complied-with-data-protection-law)
10. Food Safety Management Parents Frequently Asked Questions, accessed June 17, 2025, [http://www.stanfordschool.org/doucments/lunches/Food%20Safety%20Management%20-%20Parents%20Frequently%20Asked%20Questions.pdf](http://www.stanfordschool.org/doucments/lunches/Food%20Safety%20Management%20-%20Parents%20Frequently%20Asked%20Questions.pdf)
11. What Personal Data is Sensitive? \- Complete IT, accessed June 17, 2025, [https://www.complete-it.co.uk/what-personal-data-is-sensitive/](https://www.complete-it.co.uk/what-personal-data-is-sensitive/)
12. Food Allergy Form \- Coxheath Primary School, accessed June 17, 2025, [https://www.coxheath.kent.sch.uk/attachments/download.asp?file=856\&type=pdf](https://www.coxheath.kent.sch.uk/attachments/download.asp?file=856&type=pdf)
13. What Personal Data Is Sensitive? | Sharp, accessed June 17, 2025, [https://www.sharp.co.uk/news-and-events/blog/what-personal-data-is-sensitive](https://www.sharp.co.uk/news-and-events/blog/what-personal-data-is-sensitive)
14. GDPR Compliance for Fitness Apps: Safeguarding Personal Health Information, accessed June 17, 2025, [https://www.gdpr-advisor.com/gdpr-compliance-for-fitness-apps-safeguarding-personal-health-information/](https://www.gdpr-advisor.com/gdpr-compliance-for-fitness-apps-safeguarding-personal-health-information/)
15. What Do You Need to Know About Building GDPR-Compliant Healthcare Apps? \- Glance, accessed June 17, 2025, [https://thisisglance.com/learning-centre/what-do-you-need-to-know-about-building-gdpr-compliant-healthcare-apps](https://thisisglance.com/learning-centre/what-do-you-need-to-know-about-building-gdpr-compliant-healthcare-apps)
16. Handling severe allergies in the workplace \- HR Magazine, accessed June 17, 2025, [https://www.hrmagazine.co.uk/content/features/handling-severe-allergies-in-the-workplace/](https://www.hrmagazine.co.uk/content/features/handling-severe-allergies-in-the-workplace/)
17. www.exabeam.com, accessed June 17, 2025, [https://www.exabeam.com/explainers/gdpr-compliance/gdpr-article-9-special-personal-data-categories-and-how-to-protect-them/\#:\~:text=Healthcare%3A%20Processing%20necessary%20for%20medical,contract%20with%20a%20health%20professional.](https://www.exabeam.com/explainers/gdpr-compliance/gdpr-article-9-special-personal-data-categories-and-how-to-protect-them/#:~:text=Healthcare%3A%20Processing%20necessary%20for%20medical,contract%20with%20a%20health%20professional.)
18. University of Groningen Health Apps, their Privacy Policies and the GDPR Mulder, Trix, accessed June 17, 2025, [https://pure.rug.nl/ws/files/84309473/667\_3060\_2\_PB.pdf](https://pure.rug.nl/ws/files/84309473/667_3060_2_PB.pdf)
19. Health apps, their privacy policies and the GDPR, accessed June 17, 2025, [https://ejlt.org/index.php/ejlt/article/view/667/897](https://ejlt.org/index.php/ejlt/article/view/667/897)
20. European Data Protection Board publishes study on secondary use of personal health data for scientific research | BioSlice Blog, accessed June 17, 2025, [https://www.biosliceblog.com/2025/04/european-data-protection-board-publishes-study-on-secondary-use-of-personal-health-data-for-scientific-research/](https://www.biosliceblog.com/2025/04/european-data-protection-board-publishes-study-on-secondary-use-of-personal-health-data-for-scientific-research/)
21. EDPB Clarifies Key Health Research Data Protection Rules, accessed June 17, 2025, [https://www.wsgrdataadvisor.com/2021/02/edpb-clarifies-key-health-research-data-protection-rules/](https://www.wsgrdataadvisor.com/2021/02/edpb-clarifies-key-health-research-data-protection-rules/)
22. UK ICO Publishes New Guidance on Special Category Data \- Inside Privacy, accessed June 17, 2025, [https://www.insideprivacy.com/eu-data-protection/uk-ico-publishes-new-guidance-on-special-category-data/](https://www.insideprivacy.com/eu-data-protection/uk-ico-publishes-new-guidance-on-special-category-data/)
23. Consent \- General Data Protection Regulation (GDPR), accessed June 17, 2025, [https://gdpr-info.eu/issues/consent/](https://gdpr-info.eu/issues/consent/)
24. What is valid consent? | ICO, accessed June 17, 2025, [https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/lawful-basis/consent/what-is-valid-consent/](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/lawful-basis/consent/what-is-valid-consent/)
25. Article 7 GDPR \- GDPRhub, accessed June 17, 2025, [https://gdprhub.eu/Article\_7\_GDPR](https://gdprhub.eu/Article_7_GDPR)
26. What are the GDPR consent requirements?, accessed June 17, 2025, [https://gdpr.eu/gdpr-consent-requirements/](https://gdpr.eu/gdpr-consent-requirements/)
27. New European Data Protection Board (EDPB) Guidance Highlights – but Leaves Unresolved – Several GDPR Compliance Issues Facing Clinical Researchers | Insights | Ropes & Gray LLP, accessed June 17, 2025, [https://www.ropesgray.com/en/insights/alerts/2021/02/new-european-data-protection-board-edpb-guidance-highlights-but-leaves-unresolved](https://www.ropesgray.com/en/insights/alerts/2021/02/new-european-data-protection-board-edpb-guidance-highlights-but-leaves-unresolved)
28. GDPR Consent Requirements: 7 Conditions for Valid Consent \- Usercentrics, accessed June 17, 2025, [https://usercentrics.com/knowledge-hub/7-criteria-for-a-gdpr-compliant-consent/](https://usercentrics.com/knowledge-hub/7-criteria-for-a-gdpr-compliant-consent/)
29. GDPR Consent Requirements: A Detailed Guide for 2024 Compliance \- Transcend.io, accessed June 17, 2025, [https://transcend.io/blog/gdpr-consent-requirements](https://transcend.io/blog/gdpr-consent-requirements)
30. Europe: EDPB Updated Guidelines on Consent \- Securiti.ai, accessed June 17, 2025, [https://securiti.ai/blog/edpb-updated-guidelines-on-consent/](https://securiti.ai/blog/edpb-updated-guidelines-on-consent/)
31. The European Union (EU) General Data Protection Regulation (GDPR) \- Pitt HRPO, accessed June 17, 2025, [https://www.hrpo.pitt.edu/european-union-eu-general-data-protection-regulation-gdpr](https://www.hrpo.pitt.edu/european-union-eu-general-data-protection-regulation-gdpr)
32. Art. 32 GDPR – Security of processing \- General Data Protection Regulation (GDPR), accessed June 17, 2025, [https://gdpr-info.eu/art-32-gdpr/](https://gdpr-info.eu/art-32-gdpr/)
33. GDPR and its Relationship with Healthcare | GoAnywhere MFT, accessed June 17, 2025, [https://www.goanywhere.com/blog/gdpr-and-its-relationship-with-healthcare](https://www.goanywhere.com/blog/gdpr-and-its-relationship-with-healthcare)
34. GDPR Considerations for Healthcare: Ensuring Data Protection Compliance, accessed June 17, 2025, [https://gdprlocal.com/gdpr-considerations-for-healthcare-ensuring-data-protection-compliance/](https://gdprlocal.com/gdpr-considerations-for-healthcare-ensuring-data-protection-compliance/)
35. GDPR Compliance for Digital Health Apps \- Taylor Wessing, accessed June 17, 2025, [https://www.taylorwessing.com/en/insights-and-events/insights/2021/04/dsgvo-compliance-bei-digital-health-apps](https://www.taylorwessing.com/en/insights-and-events/insights/2021/04/dsgvo-compliance-bei-digital-health-apps)
36. What Regulations Must Your Mobile Health App Comply With? \- Glance, accessed June 17, 2025, [https://thisisglance.com/learning-centre/what-regulations-must-your-mobile-health-app-comply-with](https://thisisglance.com/learning-centre/what-regulations-must-your-mobile-health-app-comply-with)
37. Best Practices for User Data Privacy in Fitness Apps on Apple Watch \- Protecting Your Health Information \- MoldStud, accessed June 17, 2025, [https://moldstud.com/articles/p-best-practices-for-user-data-privacy-in-fitness-apps-on-apple-watch-protecting-your-health-information](https://moldstud.com/articles/p-best-practices-for-user-data-privacy-in-fitness-apps-on-apple-watch-protecting-your-health-information)
38. Recital 35 GDPR | General Data Protection Regulation \- DSGVO Portal, accessed June 17, 2025, [https://www.dsgvo-portal.de/gdpr\_recital\_35.php](https://www.dsgvo-portal.de/gdpr_recital_35.php)
39. 7 Security Controls You Need For General Data Protection Regulation (GDPR), accessed June 17, 2025, [https://www.processunity.com/6-security-controls-need-general-data-protection-regulation-gdpr/](https://www.processunity.com/6-security-controls-need-general-data-protection-regulation-gdpr/)
40. GDPR Cybersecurity Framework: A Definitive Guide \- FireMon, accessed June 17, 2025, [https://www.firemon.com/blog/gdpr-cybersecurity-compliance/](https://www.firemon.com/blog/gdpr-cybersecurity-compliance/)
41. GDPR Compliance Checklist for Healthcare Technology Companies \- Legal Nodes, accessed June 17, 2025, [https://legalnodes.com/article/gdpr-compliance-checklist](https://legalnodes.com/article/gdpr-compliance-checklist)
42. Technical organisational measures (TOMs) \- Robin Data GmbH, accessed June 17, 2025, [https://www.robin-data.io/en/data-protection-and-data-security-academy/wiki/technical-organisational-measures-gdpr-compliant-implementation](https://www.robin-data.io/en/data-protection-and-data-security-academy/wiki/technical-organisational-measures-gdpr-compliant-implementation)
43. Data residency laws: An international guide \- Persona, accessed June 17, 2025, [https://withpersona.com/blog/data-residency-laws-international-guide](https://withpersona.com/blog/data-residency-laws-international-guide)
44. Data Residency & GDPR: It's Time to Take It Seriously \- Skyflow, accessed June 17, 2025, [https://www.skyflow.com/post/data-residency-why-2023-is-the-year-to-take-it-seriously](https://www.skyflow.com/post/data-residency-why-2023-is-the-year-to-take-it-seriously)
45. GDPR Data Residency: Countries with Strict Privacy Laws \- Kiteworks, accessed June 17, 2025, [https://www.kiteworks.com/gdpr-compliance/gdpr-data-residency/](https://www.kiteworks.com/gdpr-compliance/gdpr-data-residency/)
46. Article 22 GDPR. Automated individual decision-making, including profiling, accessed June 17, 2025, [https://gdpr-text.com/read/article-22/](https://gdpr-text.com/read/article-22/)
47. Art. 22 GDPR – Automated individual decision-making, including profiling \- General Data Protection Regulation (GDPR), accessed June 17, 2025, [https://gdpr-info.eu/art-22-gdpr/](https://gdpr-info.eu/art-22-gdpr/)
48. Rights related to automated decision making including profiling | ICO, accessed June 17, 2025, [https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/individual-rights/individual-rights/rights-related-to-automated-decision-making-including-profiling/](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/individual-rights/individual-rights/rights-related-to-automated-decision-making-including-profiling/)
49. Evaluating human intervention in automated decisions | AEPD, accessed June 17, 2025, [https://www.aepd.es/en/press-and-communication/blog/evaluating-human-intervention-in-automated-decisions](https://www.aepd.es/en/press-and-communication/blog/evaluating-human-intervention-in-automated-decisions)
50. What does the UK GDPR say about automated decision-making and profiling? | ICO, accessed June 17, 2025, [https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/individual-rights/automated-decision-making-and-profiling/what-does-the-uk-gdpr-say-about-automated-decision-making-and-profiling/](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/individual-rights/automated-decision-making-and-profiling/what-does-the-uk-gdpr-say-about-automated-decision-making-and-profiling/)
51. Article 22 GDPR \- GDPRhub, accessed June 17, 2025, [https://gdprhub.eu/Article\_22\_GDPR](https://gdprhub.eu/Article_22_GDPR)
52. health-conformant reading of the GDPR's right not to be subject to automated decision-making | Medical Law Review | Oxford Academic, accessed June 17, 2025, [https://academic.oup.com/medlaw/article/32/3/373/7732100](https://academic.oup.com/medlaw/article/32/3/373/7732100)
53. What are the rules on special category data? | ICO \- Information Commissioner's Office, accessed June 17, 2025, [https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/lawful-basis/special-category-data/what-are-the-rules-on-special-category-data/](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/lawful-basis/special-category-data/what-are-the-rules-on-special-category-data/)
54. Artificial Intelligence, Profiling and Automated Decision Making | EU | Global Data and Cyber Handbook | Baker McKenzie Resource Hub, accessed June 17, 2025, [https://resourcehub.bakermckenzie.com/en/resources/global-data-and-cyber-handbook/emea/eu/topics/artificial-intelligence-profiling-and-automated-decision-making](https://resourcehub.bakermckenzie.com/en/resources/global-data-and-cyber-handbook/emea/eu/topics/artificial-intelligence-profiling-and-automated-decision-making)
55. Rights of the Individual | European Data Protection Supervisor, accessed June 17, 2025, [https://www.edps.europa.eu/data-protection/our-work/subjects/rights-individual\_en](https://www.edps.europa.eu/data-protection/our-work/subjects/rights-individual_en)
56. A guide to individual rights | ICO, accessed June 17, 2025, [https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/individual-rights/individual-rights/](https://ico.org.uk/for-organisations/uk-gdpr-guidance-and-resources/individual-rights/individual-rights/)
57. Respect individuals' rights | European Data Protection Board, accessed June 17, 2025, [https://www.edpb.europa.eu/sme-data-protection-guide/respect-individuals-rights\_en](https://www.edpb.europa.eu/sme-data-protection-guide/respect-individuals-rights_en)
58. Your Roadmap to Compliance: ICO's Guidance on DSARs \- Securiti.ai, accessed June 17, 2025, [https://securiti.ai/ico-guidance-on-dsar/](https://securiti.ai/ico-guidance-on-dsar/)
59. What are 8 Data Subject rights according to the GDPR \- Data Privacy Manager, accessed June 17, 2025, [https://dataprivacymanager.net/what-are-data-subject-rights-according-to-the-gdpr/](https://dataprivacymanager.net/what-are-data-subject-rights-according-to-the-gdpr/)
60. Data Protection: rights for data subjects \- GOV.UK, accessed June 17, 2025, [https://www.gov.uk/government/publications/data-protection-rights-for-data-subjects/data-protection-rights-for-data-subjects](https://www.gov.uk/government/publications/data-protection-rights-for-data-subjects/data-protection-rights-for-data-subjects)
61. Art. 16 GDPR – Right to rectification \- General Data Protection Regulation (GDPR), accessed June 17, 2025, [https://gdpr-info.eu/art-16-gdpr/](https://gdpr-info.eu/art-16-gdpr/)
62. Art. 17 GDPR – Right to erasure ('right to be forgotten') \- General Data Protection Regulation (GDPR), accessed June 17, 2025, [https://gdpr-info.eu/art-17-gdpr/](https://gdpr-info.eu/art-17-gdpr/)
63. The right to erasure (Articles 17 & 19 of the GDPR) \- Data Protection Commission, accessed June 17, 2025, [http://www.dataprotection.ie/en/individuals/know-your-rights/right-erasure-articles-17-19-gdpr](http://www.dataprotection.ie/en/individuals/know-your-rights/right-erasure-articles-17-19-gdpr)
64. New ICO Guidance on Subject Access Requests \- Dechert LLP, accessed June 17, 2025, [https://www.dechert.com/knowledge/onpoint/2020/11/new-ico-guidance-on-subject-access-requests.html](https://www.dechert.com/knowledge/onpoint/2020/11/new-ico-guidance-on-subject-access-requests.html)
65. 35: Health Data \- Prighter, accessed June 17, 2025, [https://prighter.com/resources/legal/gdpr/recital/35/](https://prighter.com/resources/legal/gdpr/recital/35/)
66. GDPR Brief: The European Health Data Space — From approval to national implementation, accessed June 17, 2025, [https://www.ga4gh.org/news\_item/the-european-health-data-space-from-approval-to-national-implementation/](https://www.ga4gh.org/news_item/the-european-health-data-space-from-approval-to-national-implementation/)
67. Health | European Data Protection Board, accessed June 17, 2025, [https://www.edpb.europa.eu/our-work-tools/our-documents/topic/health\_en](https://www.edpb.europa.eu/our-work-tools/our-documents/topic/health_en)
