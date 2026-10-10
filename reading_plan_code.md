[200~# LightRAG Examples: A Reading Plan This guide provides a structured path to understanding LightRAG's capabilities by walking through the official and unofficial examples. 
The examples are grouped into tiers, starting from basic usage and moving to advanced customization.
## Tier 1: Core Concepts & Quick Start
**Goal:** Understand the basic end-to-end workflow of LightRAG: initializing the system, inserting data, and performing queries. **Reading Order:** 1.  
`lightrag_openai_demo.py`: This is the best starting point. It demonstrates the simplest way to get a RAG pipeline running using the OpenAI API. It covers initialization, data 
insertion, and querying with different modes. 2.  `lightrag_openai_compatible_demo.py`: This builds on the first demo by showing how to connect to any OpenAI-compatible API. 
This is useful for using locally hosted models (via vLLM, Ollama, etc.) or other API providers that follow the OpenAI format. **Outcome:** You will be able to run a basic RAG 
pipeline and understand the core pattern of injecting your own LLM and embedding functions into LightRAG. ---
## Tier 2: Integrating with Different LLM & Embedding Providers
**Goal:** Learn how to adapt LightRAG for popular, non-OpenAI model providers. **Reading Order:** * `lightrag_gemini_demo.py`: For users of Google's Gemini models. * 
`lightrag_azure_openai_demo.py`: For users on the Microsoft Azure platform. * `lightrag_ollama_demo.py`: A key example for running with local models managed by Ollama. 
**Outcome:** You will be able to configure LightRAG to use your preferred LLM service. ---
## Tier 3: Advanced Features
**Goal:** Explore features that enhance retrieval quality, allow for custom data ingestion, and provide ways to inspect the knowledge graph. **Reading Order:** 1.  
`rerank_example.py`: Demonstrates how to add a reranker to the query pipeline. This is a crucial step for improving retrieval accuracy, especially in `mix` mode. 2.  
`insert_custom_kg.py`: For advanced users who have a pre-existing knowledge graph and want to ingest it directly, rather than building one from text. 3.  
`graph_visual_with_html.py` & `graph_visual_with_neo4j.py`: These show how to export the generated knowledge graph to a visual format, allowing you to inspect the relationships 
and entities that LightRAG has created. **Outcome:** You will understand how to enhance, inspect, and customize the core RAG process. ---
## Tier 4: Customizing the Storage Backend
**Goal:** Learn how to configure production-grade storage backends for persistence, scalability, and advanced querying. **Reading Order:** 1.  
`lightrag_gemini_postgres_demo.py`: An excellent example of using a single, powerful database (PostgreSQL) for all storage types (Key-Value, Vector, and Graph). This is a common 
production setup. 2.  `lightrag_openai_neo4j_milvus_redis_demo.py`: A "mix-and-match" example showing how to combine specialized databases: Neo4j for graph, Milvus for vectors, 
and Redis for caching. This demonstrates the flexibility of the storage layer. 3.  `lightrag_openai_mongodb_graph_demo.py` & `lightrag_openai_opensearch_graph_demo.py`: Demos 
for other popular database options. **Outcome:** You will be able to configure LightRAG to use external, persistent databases suitable for production environments. ---
## Tier 5: Community & Unofficial Samples
**Goal:** Explore community-contributed examples for a wider range of integrations and use cases. These are great for seeing how LightRAG can be adapted to various platforms. 
**Directory:** `unofficial-sample/` **Key Files to Review:** * `lightrag_hf_demo.py` & `lightrag_lmdeploy_demo.py`: Essential for users wanting to run with open-source models 
hosted locally via Hugging Face libraries. * `lightrag_llamaindex_direct_demo.py`: Shows how to integrate LightRAG within the popular LlamaIndex ecosystem. * **Other Provider 
Demos**:
    * `lightrag_nvidia_demo.py` * `lightrag_bedrock_demo.py` (AWS) * `lightrag_cloudflare_demo.py` * **Utility Scripts**: * `copy_llm_cache_to_another_storage.py`: A very useful 
    script for migrating your LLM cache when you decide to switch storage backends, saving you time and money on re-processing documents.
**Outcome:** You will have a broad view of how LightRAG can be extended and integrated into many different platforms and workflows.
