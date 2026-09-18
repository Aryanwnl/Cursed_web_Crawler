# Tor . onion_Crawler
# 🕸️ Dark Web Crawler & Text Analysis Pipeline

A Python-based recursive web crawling pipeline designed to discover and extract structured information from Tor `.onion` webpages.

The project combines **Scrapy, BeautifulSoup, NLTK, MongoDB, and proxy-based request handling** to crawl webpages, extract metadata and textual content, preprocess unstructured text, and prepare the collected information for downstream analysis.

---
## 🎯 Problem Statement

Information available across Tor `.onion` services is highly decentralized and primarily exists as unstructured HTML and textual content. Unlike traditional websites or structured datasets, there is no centralized source for discovering pages or organizing their content for analysis.

Manually identifying `.onion` pages, following interconnected links, and extracting useful information such as page titles, descriptions, keywords, metadata, and textual content is time-consuming and difficult to scale.

The goal of this project was to develop an automated ** Web Crawling and Data Extraction Pipeline** capable of starting from predefined `.onion` seed URLs, discovering additional linked pages, recursively crawling available services, and transforming unstructured webpage content into structured records.

The crawler combines **Scrapy, BeautifulSoup, NLTK, proxy-based request handling, and MongoDB** to automate page discovery, metadata extraction, text preprocessing, and data storage, creating a foundation for downstream text analysis and research.

## 📌 Project Overview

### Situation

Information hosted across Tor `.onion` services is distributed across individual webpages and largely exists as unstructured HTML and textual content.

Unlike conventional structured datasets, useful information such as page titles, descriptions, keywords, body text, and relationships between pages must first be discovered and extracted before it can be analyzed.

This project explores how a recursive web crawler can automate that data-collection process.

---

### Task

The objective was to build a pipeline capable of:

- Starting from predefined `.onion` seed URLs
- Discovering additional `.onion` links automatically
- Recursively crawling discovered webpages
- Extracting structured webpage metadata
- Collecting unstructured body text
- Cleaning and preprocessing textual content
- Generating word-frequency information
- Passing collected records through a MongoDB-backed data pipeline
- Controlling crawl depth and handling failed requests

---

### Action

Built a recursive crawler using **Python and Scrapy** that begins with a collection of `.onion` seed URLs and parses each retrieved webpage.

The crawler uses **BeautifulSoup** to inspect HTML content and identify additional `.onion` hyperlinks. Newly discovered links are submitted back to Scrapy, allowing the crawler to continue exploring connected pages.

For each successfully processed webpage, the crawler extracts:

| Field | Description |
|---|---|
| `url` | URL of the crawled webpage |
| `title` | HTML page title |
| `title_keywords` | Processed words extracted from the title |
| `keywords` | HTML meta keywords |
| `description` | HTML meta description |
| `meta` | Scrapy request metadata with selected proxy information removed |
| `body` | Text extracted from the webpage body |

A text-processing function was also implemented using **NLTK and Python's Counter utilities** to:

- Remove HTML tags
- Normalize whitespace
- Remove punctuation
- Tokenize webpage text
- Remove English stopwords
- Calculate word-frequency distributions

The crawler was configured with a **depth limit of 5** to control recursive exploration.

Custom Scrapy middleware was also incorporated for **proxy handling and randomized user-agent management**, while an item pipeline was configured for MongoDB integration.

---

### Result

The project produced an end-to-end architecture for converting unstructured `.onion` webpages into structured, analysis-ready records.

Instead of manually examining individual webpages, the crawler automates:

**URL Discovery → Page Retrieval → HTML Parsing → Metadata Extraction → Text Processing → Structured Output → Database Pipeline**

The resulting architecture demonstrates how web crawling, text processing, and NoSQL storage can be combined into a reusable data-ingestion workflow.

> **Note:** Historical crawl logs show that some `.onion` requests were unavailable or terminated during execution. Tor services can be transient, and successful retrieval depends on service availability and network configuration.

---

⚠️ Disclaimer

This project was developed strictly for **educational, research, and cybersecurity/data-engineering learning purposes**. It demonstrates concepts related to web crawling, automated data extraction, text processing, proxy-based request handling, and structured data storage.

The project is **not intended to promote, facilitate, or support illegal activity**, unauthorized access, or the collection or distribution of unlawful content. The presence of `.onion` URLs or Tor-related functionality in this repository does not imply endorsement of, participation in, or affiliation with any websites, services, organizations, or content accessible through the Tor network.

`.onion` services are dynamic and may change ownership, availability, or content over time. Any URLs included in historical code, logs, or examples should therefore be treated solely as technical references from the development environment and should not be interpreted as recommendations or endorsements.

Users are responsible for ensuring that any use of this project complies with applicable **laws, regulations, website policies, authorization requirements, and ethical research practices**.

For safe testing and development, the crawler should be used with **authorized, controlled, or benign targets** whenever possible.

No sensitive credentials, authentication information, or personally identifiable information should be committed to the repository. Any exposed credentials should be immediately revoked or rotated.

 
