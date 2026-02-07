![](https://genai.owasp.org/wp-content/uploads/2024/04/Slide02.png)

##
	LLM02:2025 Sensitive Information Disclosure

Sensitive information can affect both the LLM and its application context. This includes personal identifiable information (PII), financial details, health records, confidential business data, security credentials, and legal documents. Proprietary models may also have unique training methods and source code considered sensitive, especially in closed or foundation models.

LLMs, especially when embedded in applications, risk exposing sensitive data, proprietary algorithms, or confidential details through their output. This can result in unauthorized data access, privacy violations, and intellectual property breaches. Consumers should be aware of how to interact safely with LLMs. They need to understand the risks of unintentionally providing sensitive data, which may later be disclosed in the model's output.

To reduce this risk, LLM applications should perform adequate data sanitization to prevent user data from entering the training model. Application owners should also provide clear Terms of Use policies, allowing users to opt out of having their data included in the training model. Adding restrictions within the system prompt about data types that the LLM should return can provide mitigation against sensitive information disclosure. However, such restrictions may not always be honored and could be bypassed via prompt injection or other methods.

### [Common Examples of Vulnerability](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#common-examples-of-vulnerability)

https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#common-examples-of-vulnerability

#### 1. [PII Leakage](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#1-pii-leakage)

https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#1-pii-leakage

Personal identifiable information (PII) may be disclosed during interactions with the LLM.

#### 2. [Proprietary Algorithm Exposure](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#2-proprietary-algorithm-exposure)

https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#2-proprietary-algorithm-exposure

Poorly configured model outputs can reveal proprietary algorithms or data. Revealing training data can expose models to inversion attacks, where attackers extract sensitive information or reconstruct inputs. For instance, as demonstrated in the 'Proof Pudding' attack (CVE-2019-20634), disclosed training data facilitated model extraction and inversion, allowing attackers to circumvent security controls in machine learning algorithms and bypass email filters.

#### 3. [Sensitive Business Data Disclosure](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#3-sensitive-business-data-disclosure)

https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#3-sensitive-business-data-disclosure

Generated responses might inadvertently include confidential business information.

### [Prevention and Mitigation Strategies](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#prevention-and-mitigation-strategies)

https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#prevention-and-mitigation-strategies

###@ Sanitization:

#### 1. [Integrate Data Sanitization Techniques](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#1-integrate-data-sanitization-techniques)

https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#1-integrate-data-sanitization-techniques

Implement data sanitization to prevent user data from entering the training model. This includes scrubbing or masking sensitive content before it is used in training.

#### 2. [Robust Input Validation](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#2-robust-input-validation)

https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#2-robust-input-validation

Apply strict input validation methods to detect and filter out potentially harmful or sensitive data inputs, ensuring they do not compromise the model.

###@ Access Controls:

#### 1. [Enforce Strict Access Controls](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#1-enforce-strict-access-controls)

https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#1-enforce-strict-access-controls

Limit access to sensitive data based on the principle of least privilege. Only grant access to data that is necessary for the specific user or process.

#### 2. [Restrict Data Sources](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#2-restrict-data-sources)

https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#2-restrict-data-sources

Limit model access to external data sources, and ensure runtime data orchestration is securely managed to avoid unintended data leakage.

###@ Federated Learning and Privacy Techniques:

#### 1. [Utilize Federated Learning](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#1-utilize-federated-learning)

https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#1-utilize-federated-learning

Train models using decentralized data stored across multiple servers or devices. This approach minimizes the need for centralized data collection and reduces exposure risks.

#### 2. [Incorporate Differential Privacy](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#2-incorporate-differential-privacy)

https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#2-incorporate-differential-privacy

Apply techniques that add noise to the data or outputs, making it difficult for attackers to reverse-engineer individual data points.

###@ User Education and Transparency:

#### 1. [Educate Users on Safe LLM Usage](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#1-educate-users-on-safe-llm-usage)

https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#1-educate-users-on-safe-llm-usage

Provide guidance on avoiding the input of sensitive information. Offer training on best practices for interacting with LLMs securely.

#### 2. [Ensure Transparency in Data Usage](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#2-ensure-transparency-in-data-usage)

https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#2-ensure-transparency-in-data-usage

Maintain clear policies about data retention, usage, and deletion. Allow users to opt out of having their data included in training processes.

###@ Secure System Configuration:

#### 1. [Conceal System Preamble](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#1-conceal-system-preamble)

https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#1-conceal-system-preamble

Limit the ability for users to override or access the system's initial settings, reducing the risk of exposure to internal configurations.

#### 2. [Reference Security Misconfiguration Best Practices](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#2-reference-security-misconfiguration-best-practices)

https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#2-reference-security-misconfiguration-best-practices

Follow guidelines like "OWASP API8:2023 Security Misconfiguration" to prevent leaking sensitive information through error messages or configuration details. (Ref. link:[OWASP API8:2023 Security Misconfiguration](https://owasp.org/API-Security/editions/2023/en/0xa8-security-misconfiguration/))

###@ Advanced Techniques:

#### 1. [Homomorphic Encryption](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#1-homomorphic-encryption)

https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#1-homomorphic-encryption

Use homomorphic encryption to enable secure data analysis and privacy-preserving machine learning. This ensures data remains confidential while being processed by the model.

#### 2. [Tokenization and Redaction](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#2-tokenization-and-redaction)

https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#2-tokenization-and-redaction

Implement tokenization to preprocess and sanitize sensitive information. Techniques like pattern matching can detect and redact confidential content before processing.

### [Example Attack Scenarios](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#example-attack-scenarios)

https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#example-attack-scenarios

#### Scenario #1: [Unintentional Data Exposure](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#scenario-1-unintentional-data-exposure)

https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#scenario-1-unintentional-data-exposure

A user receives a response containing another user's personal data due to inadequate data sanitization.

#### Scenario #2: [Targeted Prompt Injection](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#scenario-2-targeted-prompt-injection)

https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#scenario-2-targeted-prompt-injection

An attacker bypasses input filters to extract sensitive information.

#### Scenario #3: [Data Leak via Training Data](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#scenario-3-data-leak-via-training-data)

https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#scenario-3-data-leak-via-training-data

Negligent data inclusion in training leads to sensitive information disclosure.

### [Reference Links](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#reference-links)

https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#reference-links

1. [Lessons learned from ChatGPT's Samsung leak](https://cybernews.com/security/chatgpt-samsung-leak-explained-lessons/): **Cybernews**
2. [AI data leak crisis: New tool prevents company secrets from being fed to ChatGPT](https://www.foxbusiness.com/politics/ai-data-leak-crisis-prevent-company-secrets-chatgpt): **Fox Business**
3. [ChatGPT Spit Out Sensitive Data When Told to Repeat 'Poem' Forever](https://www.wired.com/story/chatgpt-poem-forever-security-roundup/): **Wired**
4. [Using Differential Privacy to Build Secure Models](https://neptune.ai/blog/using-differential-privacy-to-build-secure-models-tools-methods-best-practices): **Neptune Blog**
5. [Proof Pudding (CVE-2019-20634)](https://avidml.org/database/avid-2023-v009/) **AVID** (`moohax` & `monoxgas`)

### [Related Frameworks and Taxonomies](https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#related-frameworks-and-taxonomies)

https://github.com/OWASP/www-project-top-10-for-large-language-model-applications/blob/main/2_0_vulns/LLM02_SensitiveInformationDisclosure.md#related-frameworks-and-taxonomies

Refer to this section for comprehensive information, scenarios strategies relating to infrastructure deployment, applied environment controls and other best practices.

- [AML.T0024.000 – Infer Training Data Membership](https://atlas.mitre.org/techniques/AML.T0024.000) **MITRE ATLAS**
- [AML.T0024.001 – Invert ML Model](https://atlas.mitre.org/techniques/AML.T0024.001) **MITRE ATLAS**
- [AML.T0024.002 – Extract ML Model](https://atlas.mitre.org/techniques/AML.T0024.002) **MITRE ATLAS**
