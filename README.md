Intellexa: Multi-Format Content Analysis AI


Project Overview

Intellexa is an advanced Retrieval-Augmented Generation (RAG) application designed to deliver intelligent, context-aware analysis of diverse digital content formats. It leverages a self-hosted vector database (Chroma) for efficient knowledge retrieval, external Large Language Models (Groq's Llama-3.3-70b) for rapid inference, and a modern, interactive user interface built with Streamlit.

This project demonstrates expertise in combining modern AI orchestration (LangGraph, multi-format processing) with full-stack development to solve real-world information fragmentation challenges.

Key Technical Highlights 

Multi-Source RAG Architecture: Implements sophisticated RAG pipelines for YouTube videos, research papers, PDF documents, and web content with specialized processing for each format.


Intelligent Query Routing: Uses LangGraph state machines with multi-layer classification (regex patterns, keyword analysis, LLM intent detection) to route queries to appropriate handlers.


Temporal Video Analysis: Processes YouTube transcripts with minute-based chunking and timestamp preservation for precise video content referencing.


Vector Database: Utilizes ChromaDB for storing and indexing multi-format content embeddings, enabling fast semantic search with MMR (Maximal Marginal Relevance).


LLM Integration: Integrates the high-speed Groq API (using llama-3.3-70b-versatile) for low-latency response generation across diverse content types.


Multi-Modal Interface: Features voice input, text-to-speech responses, and a responsive Streamlit UI for seamless user interaction.

Tech Stack & Dependencies

The project is built using Python 3.10.11  with the following key libraries:

Frontend Framework	-> Streamlit ->	Interactive web interface and real-time updates

LLM Inference -> Groq (llama-3.3-70b-versatile) ->	High-speed content analysis and response generation

Vector Database	-> Chroma ->	Local vector storage for semantic search

AI Orchestration ->	LangGraph	-> Stateful workflow management and query routing

Embeddings	-> HuggingFaceEmbeddings (paraphrase-multilingual-mpnet-base-v2)	-> Multilingual text representations (768-dim)

Content Processing	-> YouTubeTranscriptApi, PyPDF2, arXiv, Trafilatura, BeautifulSoup ->	Multi-format content extraction and parsing

Audio Services ->	Edge-TTS, streamlit-mic-recorder ->	Text-to-speech and voice input capabilities

AI Framework n ->	LangChain ->	RAG pipeline management and tool integration

Dependencies are listed in requirements.txt

📂 Project Structure

The codebase follows a modular structure for clarity and maintainability:


Intellexa-Content-Analysis-AI/

├── frontend.py                 # Streamlit web interface and UI components

├── backend.py                  # Core AI orchestration, LangGraph workflows, handlers

├── web_loader.py              # Multi-format content processor (PDF, arXiv, web, news)

├── requirements.txt           # Project dependencies and libraries

├── .env.example              # Environment variables template

└── output/                   # Generated audio files storage

    └── audio_*.mp3

### Core Modules:

- **frontend.py**: User interface, session management, voice input/output
  
- **backend.py**: LangGraph state machine, query routing, specialized handlers

-  **web_loader.py**: Universal content processor with format detection
-  
   Setup and Installation Guide
   
1. Prerequisites:
   
Python 3.9 or higher installed

A Groq API Key (Get one here)

Basic familiarity with environment variables

2. Environment Setup:
   
Clone the repository and set up the environment:


python -m venv venv

source venv/bin/activate  # On Windows: venv\Scripts\activate

# Install dependencies

pip install -r requirements.txt

3. API Key Configuration:
   
Create a .env file in the root directory and add your Groq API key:


GROQ_API_KEY="your_groq_api_key_here"

4. Content Processing Setup:
   
The system automatically handles content processing - no manual indexing required!

YouTube Videos: Transcripts are processed on-demand when URLs are loaded

Web Content: PDFs, research papers, and articles are processed in real-time

Vector Storage: ChromaDB collections are created automatically per content source

5. Running the Application:
   
Start the Streamlit application:


streamlit run frontend.py

Access the application: Open your web browser and navigate to: http://localhost:8501

Core Logic Explanation

backend.py - AI Orchestration & Workflows

This file contains the core intelligence of the system:


State Management : State(TypedDict) class manages conversation history, audio preferences, and current content source

Query Routing :	enhanced_route_query() uses multi-layer classification (content source → regex → keywords → LLM)

Specialized Handlers : handle_video_qa(), handle_web_content(), handle_general_query() process different query types

RAG Implementation	: ChromaDB retrievers with MMR search for diverse, relevant context retrieval

web_loader.py - Multi-Format Content Processing

Universal content processor with intelligent format detection:

Function & Description

process_url(url) :	Main entry point that auto-detects content type and routes to appropriate processor

_detect_content_type() :	Identifies PDF, arXiv, news, or general webpage from URL patterns

_process_pdf()	: Extracts text with page-level metadata using PyPDF2

_process_arxiv() : Fetches research paper metadata and abstracts via arXiv API

_process_news() :	Uses newspaper3k for clean article extraction with NLP features

_process_webpage() :	Implements fallback strategy (trafilatura → BeautifulSoup)

frontend.py - User Interface & Interaction

Modern Streamlit interface with advanced features

