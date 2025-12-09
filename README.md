Multi-Modal RAG Ingestion Pipeline

Project Summary:

This project implements a complete multi-modal Retrieval-Augmented Generation ingestion pipeline capable of processing complex documents containing text, tables, and images. The system converts raw unstructured PDF documents into enriched, searchable vector representations using Unstructured.io, LangChain, OpenAI models, and ChromaDB. The ingestion flow is designed to reflect production-grade RAG systems with clear stages for parsing, chunking, multimodal summarization, metadata preservation, and vector store creation. This ensures that downstream retrieval tasks benefit not only from plain text but also from visual and tabular information, enabling richer and more accurate responses from large language models.

Document Partitioning:

The pipeline begins by parsing the source PDF into its atomic elements such as headings, narrative text, tables, lists, captions, and embedded images. Unstructured.io’s high-resolution partitioning extracts each element with detailed metadata, allowing a fine-grained understanding and reconstruction of the original document structure. The result is a set of atomic elements, each labeled with its semantic type.

Chunking by Title:

After partitioning, the pipeline groups elements into meaningful sections using a title-based chunking strategy. This approach aligns content based on natural document boundaries rather than fixed sizes, allowing each chunk to represent a coherent unit of information. Chunk sizes are managed using soft and hard character limits, and small sections are merged when necessary to maintain context completeness. The outcome is a well-structured set of document chunks that may include text, tables, images, or mixed content.

Multimodal AI-Enhanced Summarization:

Each chunk is then analyzed to determine the types of content it contains. Chunks that include tables or images are processed through a multimodal large language model capable of interpreting both text and visual information. The system generates a retrieval-oriented summary designed to enhance semantic search, covering key facts from the text, extracted insights from tables, interpretations of visual elements, topic summaries, and variations of user search intent. For purely textual chunks, the raw content is preserved directly. The final output of this stage is a set of LangChain Document objects enriched with metadata such as original raw text, HTML tables, and base64-encoded images.

Vector Store Creation:

The enriched documents are embedded using the text-embedding-3-small model and stored in a persistent ChromaDB vector database. Each vector entry contains both the enhanced summary and full metadata, allowing retrieval operations to return contextually accurate and semantically rich information. This enables improved table-aware, image-aware, and text-aware retrieval for downstream RAG applications.

Final Output:

The completed pipeline produces a fully searchable vector database representing the entire document in a multimodal semantic format. It supports complex question answering, contextual retrieval, and enterprise document intelligence use cases. This ingestion workflow forms the foundation of a production-ready RAG system designed for real-world applications requiring accurate multimodal understanding.


Pipeline Architecture:

The ingestion pipeline follows four main stages:
	1.	Partition PDF into atomic elements
Using Unstructured.io to extract structured elements such as text, tables, images, lists, headers, and captions.
	2.	Chunk elements using a title-based strategy
Producing coherent, semantically meaningful sections that respect document structure.
	3.	Enhance chunks using multimodal LLM summarization
Generating enriched retrieval-focused representations including text, table insights, and visual analysis.
	4.	Store embeddings and documents in ChromaDB
Creating a persistent vector store for efficient retrieval and downstream question answering.


Features:
	1.	End-to-end multimodal pipeline supporting text, tables, and images
	2.	High-resolution Unstructured.io parsing
	3.	Intelligent chunking using title-based segmentation
	4.	Multimodal summarization using OpenAI GPT-4o
	5.	Rich metadata preservation for original elements
	6.	Persisted vector store with ChromaDB
	7.	Retrieval-ready document database for RAG systems
	8.	Example querying pipeline for document-based Q&A


How to Run:

    1. Install system dependencies (macOS)

        brew install poppler tesseract libmagic

    2. Install Python dependencies

        pip install -U unstructured[all-docs]
        pip install -U langchain langchain-openai langchain-community langchain-chroma
        pip install -U python-dotenv

    3. Add your .env file

        OPENAI_API_KEY=your_key

    4. Run the notebook or the pipeline functions
	    •	Partition PDF
	    •	Chunk by title
	    •	Summarize chunks
	    •	Build vector store
	    •	Query results


Technologies Used:
	•	Unstructured.io
	•	LangChain
	•	OpenAI GPT-4o
	•	ChromaDB
	•	Python
	•	PDF, Table, and Image Processing
