Multi-Modal RAG Pipeline

This project implements an advanced Retrieval-Augmented Generation (RAG) pipeline capable of processing multimodal PDF documents containing text, tables, and images. It transforms unstructured documents into structured AI-searchable chunks, enriches them using an LLM, and stores them in a vector database for high-quality retrieval.

The system is designed for production-oriented document intelligence applications and demonstrates key concepts in multimodal ingestion, chunking, summarisation, and retrieval workflows.

Project Overview

The pipeline performs the following core tasks:
	1.	Document Parsing
Extracts text, tables, and images from PDFs using Unstructured.io. Tables are preserved as HTML, and images are captured as base64-encoded data.
	2.	Intelligent Chunking
Uses title-based chunking to split documents into logically coherent sections, with configurable character limits and rules for merging smaller chunks.
	3.	AI-Enhanced Chunk Summaries
Each chunk is enriched using GPT-4o, which analyses text, tables, and images to generate a highly searchable, semantically rich description. This improves retrieval accuracy and downstream question answering.
	4.	Vector Store Construction
Embeds the processed chunks using the OpenAI text-embedding-3-small model and stores them in ChromaDB with cosine similarity indexing.
	5.	Retrieval and Answer Generation
Allows querying the vector store using natural language. Retrieved chunks, along with their original text, tables, and images, are passed into the LLM to generate final answers.

Key Features
	•	End-to-end PDF to vector database processing
	•	Multimodal handling of text, tables, and images
	•	AI-generated enhanced summaries for improved retrieval
	•	Storage of raw and enriched content with detailed metadata
	•	High-quality question answering powered by GPT-4o
	•	Fully automated ingestion and retrieval pipeline

Requirements

This project depends on Python 3.10+ and the following system-level tools:
	•	poppler (for PDF parsing)
	•	tesseract (for OCR)
	•	libmagic (for file type detection)

Python dependencies include:
	•	unstructured
	•	langchain
	•	langchain-community
	•	langchain-openai
	•	langchain-chroma
	•	chromadb
	•	python-dotenv
	•	openai

How the Pipeline Works
	1.	Partitioning
partition_pdf extracts granular document elements including text blocks, titles, tables, and embedded images.
	2.	Chunking
chunk_by_title creates semantically meaningful chunks with a maximum character budget to optimize retrieval performance.
	3.	Content Separation
Each chunk is analysed to separate raw text, table HTML, and image content.
	4.	AI-Enriched Summary
Chunks containing tables or images are sent to GPT-4o, which produces a consolidated summary optimised for search. Pure text chunks preserve the content directly.
	5.	Vector Embedding
Summarised chunks are embedded and added to ChromaDB.
	6.	Retrieval
Queries use a k-nearest-neighbour search to return the top relevant chunks.
	7.	Answer Construction
Retrieved content is combined and provided to GPT-4o to generate a final, grounded answer.

Running the Project
	1.	Install system dependencies (poppler, tesseract, libmagic)
	2.	Create and activate a virtual environment
	3.	Install Python dependencies
	4.	Run the notebook or script to execute the ingestion pipeline
	5.	Query the vector store and generate answers

Example :
python -m venv venv
source venv/bin/activate

Use Cases
	•	Research document Q&A systems
	•	Enterprise document intelligence
	•	Financial reports analysis
	•	PDF-heavy knowledge retrieval
	•	Legal and technical document search
	•	Multimodal RAG experimentation

Summary

This project demonstrates a complete multimodal RAG workflow, from parsing complex PDF documents to generating AI-enhanced retrieval outputs. It highlights practical techniques for document preprocessing, chunking, metadata preservation, multimodal summarisation, vector search, and grounded question answering.

