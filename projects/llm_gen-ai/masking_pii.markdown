---
# Feel free to add content and custom Front Matter to this file.
# To modify the layout, see https://jekyllrb.com/docs/themes/#overriding-theme-defaults

layout: default
title: Masking PII data
parent: LLM and Gen-AI
permalink: /llm_genai/mask_pii
nav_order: 106
---

# Self-Hosted Offline LLM-Based PII Detection and Masking System
LLM
{: .badge .badge-pill .badge-primary }
PII
{: .badge .badge-pill .badge-secondary }

* Do not remove this line (it will not be displayed)
{:toc}

Self-hosted web interface for detecting and masking PII data using an LLM model. Fully offline and customizable.

# Schema

  {% include whimsical.html src="https://whimsical.com/embed/EaVTkCZnTn61tmXHzVd2Xm@8ADn3nfZACauWrMNNNkjN1CJWEquE6Ajo6rm" %}

# Video

  {% include video.html src="/assets/videos/detect_PII.mp4" %}


# Self-Hosted Web Interface for PII Detection and Masking

Develop a self-hosted web interface that enables users to identify and protect Personally Identifiable Information (PII) using a local Large Language Model (LLM) workflow. The system is designed to operate fully offline, ensuring that sensitive information remains inside the internal infrastructure without being transferred to external AI services.

Provide a customizable interface that allows users to submit different types of content and automatically detect sensitive entities. The system combines document processing, Natural Language Processing (NLP), and entity recognition techniques to analyze input content and replace sensitive information with secure masking labels.

This approach enables organizations to safely process internal documents, customer information, or confidential text while maintaining data privacy and compliance requirements.

## Dual Input Processing Interface

Design the interface with two main input methods to support different user scenarios: **URL-based input** and **direct text input**.

Allow users to select the most suitable ingestion method depending on their data source. 
- **For online documents or webpages**, provide a URL ingestion workflow that automatically retrieves and processes webpage content. 
- **For manually prepared information**, provide a text input workflow that directly accepts user-provided content.

Both input methods are standardized into the same markdown-based processing format before entering the PII detection pipeline. This ensures that different data sources can be processed consistently using the same detection and masking mechanism.

## URL-Based Document Ingestion Using Docling

Implement URL-based ingestion by using Docling to extract and transform webpage content into a structured markdown format.

The system receives a webpage URL from the user and performs document extraction to capture the main content, including paragraphs, tables, lists, and other relevant webpage elements. The extracted information is converted into markdown representation to preserve document structure while making it easier for downstream processing.

The markdown output becomes the standardized input format for the PII detection module. This approach allows the system to process webpages while maintaining the original document context and layout.

## Text-Based Input Processing

Support direct text processing by allowing users to provide raw text content through the interface. The system accepts the user-provided string input and converts it into markdown format before performing PII analysis.

The conversion step ensures consistency between manually entered content and extracted webpage content. By using markdown as the intermediate format, the detection pipeline can analyze structured elements such as paragraphs, tables, and text blocks using the same processing logic.

This design simplifies the overall architecture because all input sources follow a single processing flow after normalization.

## PII Entity Detection Using GLiNER Model

Implement the PII detection engine using the **GLiNER model** to identify sensitive entities from processed markdown content. The model performs zero-shot named **entity recognition (NER)**, allowing the system to detect different categories of sensitive information without requiring a separate model for each entity type.

Configure the detection pipeline with predefined PII labels, including:
- Work
- Booking Number
- Personally Identifiable Information
- Driver Licence
- Person
- Full Address
- Company
- Actor
- Character
- Email
- Passport Number
- Social Security Number
- Phone Number

The model scans the processed content and identifies text spans that match these categories. Each detected entity is mapped with its corresponding label, allowing the masking process to understand what type of sensitive information needs protection.

## Advanced PII Obfuscation and Markdown Element Scanning

Apply the Advanced PII Obfuscator after entity detection to transform identified sensitive information into protected representations.

The system scans every markdown element, including text blocks and table cells, to ensure that PII entities are detected regardless of their location inside the document structure. This prevents sensitive information from being missed in structured content such as reports, tables, or formatted documents.

Replace detected entities with reversible masking markers based on their assigned labels. The obfuscation layer maintains the relationship between the original value and the generated placeholder, allowing authorized users to restore the original information when required.

This process provides a balance between privacy protection and operational usability.

## Masked Output Generation and Reversible Data Protection

Generate the final output by preserving the original document structure while replacing sensitive entities with masked values.

Display the processed content in a similar format to the original input, ensuring that users can still understand the document context without exposing confidential information. Detected entities are replaced with labeled placeholders that indicate the type of protected information.

For example, sensitive information such as names, emails, phone numbers, or identification numbers will be transformed into categorized markers while maintaining document readability.

The reversible masking mechanism allows the system to support secure workflows where data can be anonymized for analysis, sharing, or processing, while still providing controlled recovery when necessary.

## System Objective

Build the platform as a privacy-first AI solution for automatic PII detection and protection. The combination of local LLM infrastructure, document processing, entity recognition, and reversible obfuscation enables organizations to safely analyze sensitive information without exposing raw data outside their environment.

The system provides:
- Fully offline AI processing
- Customizable PII detection categories
- Multi-source document ingestion
- Structured markdown-based processing
- Automated sensitive data masking
- Reversible anonymization workflow

This architecture supports secure enterprise AI adoption by protecting confidential information while preserving the usability of processed documents.