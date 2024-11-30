# Vector-and-Faceted-Search


## *Overview:*

This repository contains the analysis for the generic dataset, which evaluates the performance of DuckDB and Redis for vector search and faceted search operations. This application compares the performance of both databases in terms of search latency, memory usage, and index build time.

Technologies and Methods Used
Programming Language: Python 3.11.7
Libraries:

NumPy, Pandas, random,matplotlib

Sentence-Transformers (for generating embeddings)

time, string, pickle, base64,memory_profiler, concurrent


## *Databases:*

DuckDB: For SQL-based querying and vector search.

Redis: For Redis Stack-based vector search and faceted filtering.

Vector Search Techniques: Cosine similarity is used for vector matching.


## *Data Generation*
A dataset of 100,000 product records is created with the following attributes:

Product ID: A unique identifier (e.g., 000001, 000002, …, 100000).

Product Name: Randomly generated product names(adjectives + nouns +conjunctions + adjectives + nouns).

Category: Books

Price: A random integer between 5 and 200.

Description: Randomly generated (adjectives + genres + "book for" + audience)

Vector Embedding: A vector representation of the product description using the Sentence-Transformers library.

Vector and Faceted Search Implementation
The project evaluates the performance of two databases in handling vector search and faceted search, with specific emphasis on:

With vector matching method selected top 10 similar products given a query vector, output example(Redis);

*{'Product_ID': 'Unknown', 'Product_Name': 'Enigmatic Quest for Unforgettable Chronicles', 'Product_Description': 'No Description', 'Product_Price': 0.0, 'Similarity': 0.0879556342527879}*

*{'Product_ID': 'Unknown', 'Product_Name': 'Enigmatic Journey in Charming Journey', 'Product_Description': 'No Description', 'Product_Price': 0.0, 'Similarity': 0.0879556342527879}*

*{'Product_ID': 'Unknown', 'Product_Name': 'Unforgettable Story in Charming Chronicles', 'Product_Description': 'No Description', 'Product_Price': 0.0, 'Similarity': 0.0879556342527879}*


## Performance Results
Overall Insight:

DuckDB is well suited for scenarios prioritizing lightweight operations and quick indexing, while Redis provides substantial benefits for both small and large datasets, especially where query performance and memory optimization are critical.


## For DuckDB
-DuckDB performs exceptionally well for larger datasets after indexing, with reduced query latency and memory usage. -However, for small datasets, the performance gain is minimal or even slightly negative, suggesting that indexing is more beneficial for large scale data operations.

(Dataset with 1.000 samples)

=== Performance Comparison ===

Before Index Query Latency: 0.0040 seconds

After Index Query Latency: 0.0091 seconds

Improvement in Query Latency: -0.0051 seconds

Before Index Memory Usage: 0.1523 MB

After Index Memory Usage: 0.0977 MB

Improvement in Memory Usage: 0.0547 MB

(Dataset with 100.000 samples)

=== Performance Comparison ===

Before Index Query Latency: 0.0131 seconds

After Index Query Latency: 0.0068 seconds

Improvement in Query Latency: 0.0063 seconds

Before Index Memory Usage: 0.3359 MB

After Index Memory Usage: 0.1016 MB

Improvement in Memory Usage: 0.2344 MB

## For Redis
-Index creation in Redis consistently improves query latency and memory usage for both small and large datasets. -While the relative latency improvement is more pronounced for smaller datasets, memory optimization is significant across both dataset sizes.

(Dataset with 1.000 samples)

=== Performance Comparison ===

Before Index Query Latency: 3.6771 seconds

After Index Query Latency: 2.4949 seconds

Improvement in Query Latency: 1.1821 seconds

Before Index Memory Usage: 2.9531 MB

After Index Memory Usage: 0.5352 MB

Improvement in Memory Usage: 2.4180 MB

(Dataset with 100.000 samples)

=== Before Index Creation ===

Query Latency: 110.8202 seconds

Memory Usage: 11.6953 MB

=== After Index Creation ===

Query Latency: 103.6501 seconds

Memory Usage: 4.8008 MB

## Tests for both Databases
*For DuckDB*
Query Time Analysis: The average time for queries decreases as more filters are applied, significantly reducing from 1 filter to 2 filters. The addition of a vector does not seem to affect the query time drastically, though it is slightly higher for a single filter.

Statistical Insights:

Mean value of 0.00135 seconds indicates that, on average, the queries are very fast. Standard Deviation of 0.0009 seconds suggests a moderate level of consistency in the query performance, with a small variation between query times. Median of 0.0008 seconds further confirms the low and consistent query times, with most queries falling below 0.001 seconds.

Conclusion
DuckDB is ideal for scenarios where quick indexing and lightweight operations are crucial.
However, Redis stands out for its ability to optimize both query latency and memory usage, particularly beneficial for both small and large datasets. It is highly recommended when query performance and memory efficiency are critical.
