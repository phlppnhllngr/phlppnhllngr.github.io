---
title: RAG
parent: AI
---

# RAG
 
## Tipps und Strategien
- <https://www.youtube.com/watch?v=smGbeghV1JE>
- <https://github.com/NirDiamant/RAG_Techniques> - *showcases various advanced techniques for RAG systems*
- <https://www.kapa.ai/blog/rag-best-practices>
- <https://old.reddit.com/r/LocalLLaMA/comments/1im35yl/how_to_scale_rag_to_20_million_documents/>
- <https://github.com/coleam00/ottomator-agents/tree/main/all-rag-strategies>
- <https://old.reddit.com/r/LocalLLaMA/comments/1pd1yqc/hot_take_were_overselling_semantic_search_in_rag/>
- [HN: So you wanna build a local RAG?, 12/2025](https://news.ycombinator.com/item?id=46080364)
- <https://foojay.io/today/navigating-the-nuances-of-graphrag-vs-rag/>
- [HN: Production RAG: what I learned from processing 5M+ documents, 10/2025](https://news.ycombinator.com/item?id=45645349)
- <https://eugeneyan.com/writing/llm-patterns/#retrieval-augmented-generation-to-add-knowledge>

## Tools
- **RAGFlow**
  - *Deep document understanding-based knowledge extraction from unstructured data with complicated formats*
  - *Supports Word, slides, excel, txt, images, scanned copies, structured data, web pages, and more.*
  - *Prerequisites: CPU >= 4 cores, RAM >= 16 GB, Disk >= 50 GB* 
  - <https://github.com/infiniflow/ragflow> <img loading="lazy" src="https://img.shields.io/github/stars/infiniflow/ragflow?style=flat-square"/>
- **RAGMeUp**
  - *generic framework (server + UIs) that enables you do to RAG on your own dataset easily* 
  - <https://github.com/AI-Commandos/RAGMeUp> <img loading="lazy" src="https://img.shields.io/github/stars/AI-Commandos/RAGMeUp?style=flat-square"/>
- **Quivr**
  - *Opiniated RAG for integrating GenAI in your apps*
  - Python 
  - <https://github.com/QuivrHQ/quivr/> <img loading="lazy" src="https://img.shields.io/github/stars/QuivrHQ/quivr?style=flat-square"/>
- **MegaParse**
  - *File Parser optimised for LLM Ingestion with no loss. Parse PDFs, Docx, PPTx in a format that is ideal for LLMs.* 
  - <https://github.com/quivrhq/megaparse> <img loading="lazy" src="https://img.shields.io/github/stars/quivrhq/megaparse?style=flat-square"/>
- **Haystack**
  - *AI orchestration framework to build customizable, production-ready LLM applications. Connect components (models, vector DBs, file converters) to pipelines or agents that can interact with your data. With advanced retrieval methods, it's best suited for building RAG, question answering, semantic search or conversational agent chatbots.* 
  - <https://github.com/deepset-ai/haystack> <img loading="lazy" src="https://img.shields.io/github/stars/deepset-ai/haystack?style=flat-square"/>
- **unstructured**
  - *The unstructured library provides open-source components for ingesting and pre-processing images and text documents, such as PDFs, HTML, Word docs, and many more. The use cases of unstructured revolve around streamlining and optimizing the data processing workflow for LLMs.*
  - <https://github.com/Unstructured-IO/unstructured> <img loading="lazy" src="https://img.shields.io/github/stars/Unstructured-IO/unstructured?style=flat-square"/>
- **Morphik**
  - *multimodal retrieval over documents like PDFs, where images and diagrams matter as much as the text*
  - <https://github.com/morphik-org/morphik-core>
  - <https://news.ycombinator.com/item?id=43763814>
- **Rlama**
  - *question-answering tool for your documents, seamlessly integrating with your local Ollama models. It enables you to create, manage, and interact with Retrieval-Augmented Generation (RAG) systems tailored to your documentation needs.*
  - *Creates a new RAG system by indexing all documents in the specified folder. Create a RAG system from a website.* 
  - <https://github.com/dontizi/rlama?tab=readme-ov-file>
- **kotaemon**
  - *customizable RAG UI for chatting with your documents*
  - <https://github.com/Cinnamon/kotaemon> <img loading="lazy" src="https://img.shields.io/github/stars/Cinnamon/kotaemon?style=flat-square"/>
- **GraphRAG**
  - *data pipeline and transformation suite that is designed to extract meaningful, structured data from unstructured text using the power of LLMs* 
  - <https://github.com/microsoft/graphrag> <img loading="lazy" src="https://img.shields.io/github/stars/microsoft/graphrag?style=flat-square"/>
- **LightRAG**
  - *leverage LLMs to identify and extract various entities (e.g., names, dates, locations, and events) along with the relationships between them. The information collected through this process will be used to create a comprehensive knowledge graph* 
  - <https://lightrag.github.io/> 
  - <https://github.com/HKUDS/LightRAG>
- **Skald**
  - *In the ingestion phase, Skald takes care of document parsing, chunking strategy, summaries, tagging, embedding generation, and vector storage.*
  - *In the retrieval phase, it handles query rewriting, vector search, LLM chat, chat history, and source references.*
  - *Our solid defaults will work for most use cases, but you can tune every part of your RAG to better suit your needs.*
  - <https://github.com/skaldlabs/skald> 

## Re-ranker
- <https://www.zeroentropy.dev/articles/ultimate-guide-to-choosing-the-best-reranking-model-in-2025>
- <https://fin.ai/research/how-we-built-a-world-class-reranker-for-fin/>

## Textsuche
- **ripgrep**
  - <https://github.com/BurntSushi/ripgrep>
- **BM25**
  - <https://en.wikipedia.org/wiki/Okapi_BM25> - *a ranking function used by search engines to estimate the relevance of documents to a given search query*

## Vector DB
- **Weaviate**
  - *to turn your data - text, images, and more - into a searchable vector database*
  - *can vectorize your data at import time*
  - *GraphQL API, REST API, gRPC API*
  - <https://github.com/weaviate/weaviate> <img loading="lazy" src="https://img.shields.io/github/stars/weaviate/weaviate?style=flat-square"/>
- **Milvus**
  - <https://github.com/milvus-io/milvus> <img loading="lazy" src="https://img.shields.io/github/stars/milvus-io/milvus?style=flat-square"/>
- **Postgres**
  - pgvector
    - <https://github.com/pgvector/pgvector> 
  - pg_search
  - PostgresML
    - *Postgres extension that seamlessly combines data storage and machine learning inference within your database*
    - *Run machine learning and AI operations directly within PostgreSQL*
    - *Built-in functions for chunking, embedding, ranking, and transforming text*
    - <https://github.com/postgresml/postgresml> <img loading="lazy" src="https://img.shields.io/github/stars/postgresml/postgresml?style=flat-square"/>
  - pgai
    - *suite of tools to develop RAG, semantic search, and other AI applications more easily with PostgreSQL*
    - <https://github.com/timescale/pgai>
- **Chroma**
  - <https://github.com/chroma-core/chroma> <img loading="lazy" src="https://img.shields.io/github/stars/chroma-core/chroma?style=flat-square"/>
- **Qdrant**
  - <https://github.com/qdrant/qdrant> <img loading="lazy" src="https://img.shields.io/github/stars/qdrant/qdrant?style=flat-square"/>
- **Pinecone**
- **txtai**
  - *all-in-one embeddings database for semantic search, LLM orchestration and language model workflows* 
  - <https://github.com/neuml/txtai> <img loading="lazy" src="https://img.shields.io/github/stars/neuml/txtai?style=flat-square"/>
- **LanceDB**
  - *embedded retrieval engine for multimodal AI* 
  - <https://github.com/lancedb/lancedb> <img loading="lazy" src="https://img.shields.io/github/stars/lancedb/lancedb?style=flat-square"/>

