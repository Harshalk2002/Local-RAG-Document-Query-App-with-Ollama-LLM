# Local RAG Document Query App with Ollama LLM

This project implements a document retrieval and question-answering system that uses a combination of vector databases and language models. The system enables users to upload PDF documents, split them into chunks, store these chunks in a vector database, and perform Question Answering (Q&A) based on the content of the document.

## Key Technologies and Libraries

- **Streamlit**: Used to build the interactive web application interface.
- **chromadb**: A vector database that stores document embeddings for fast similarity search.
- **ollama**: A conversational AI model used for embedding and answering questions.
- **Langchain**: A framework used for document loading and processing.
- **PyMuPDF**: A library used for loading content from PDF files.
- **CrossEncoder**: A model used for re-ranking the documents based on relevance to a query.
- **hydralit_components**: Provides custom loading animations for Streamlit.

## Features

### 1. Document Upload and Processing
- Users can upload PDF files, which are then processed into smaller chunks using **PyMuPDFLoader** and **RecursiveCharacterTextSplitter**.
  
### 2. Vector Collection Management
- **OllamaEmbeddingFunction** is used to convert text into embeddings, which are stored in a **chromadb** vector collection. This enables fast and efficient retrieval of relevant documents based on a query.

### 3. Adding Document Chunks to the Vector Store
- After splitting the document, the chunks along with metadata are added to the vector collection. The system provides feedback once the data is successfully added to the database.

### 4. Querying and Answering Questions
- Users can submit questions related to the uploaded document. The system queries the vector store for relevant document chunks and ranks them using **CrossEncoder**.
- **Ollama's chat model** is then used to generate a detailed response based on the retrieved context.

### 5. Answer Generation
- The system analyzes the relevant document content and formulates a structured, readable answer, adhering to a system prompt that ensures clarity and completeness.

## Workflow

1. **Upload PDF**: The user uploads a PDF through the Streamlit interface.
2. **Process Document**: The uploaded document is split into chunks, which are stored in the vector database.
3. **Query the Database**: The user submits a question, and the system retrieves the most relevant documents from the database.
4. **Rank and Respond**: The system re-ranks the documents based on relevance and uses the LLM to generate an answer.
5. **Display Results**: The answer and relevant documents are displayed to the user.

## System Architecture

- **PDF Upload**: The user uploads PDF files through the Streamlit interface.
- **Document Splitting**: PDF documents are split into smaller chunks for easier management and retrieval.
- **Embedding**: Text chunks are embedded using Ollama's embedding function.
- **Vector Database**: Embeddings are stored in **chromadb**, a persistent vector database.
- **Query Handling**: User queries are processed by retrieving relevant documents from the vector store.
- **Answer Generation**: Relevant documents are passed through Ollama's LLM to generate a comprehensive answer.

## User Interface

- **Sidebar**: Contains options for uploading files and initiating document processing.
- **Main Area**: Displays the Q&A interface, where users can type their questions and view results.
- **Results Expansion**: Users can expand sections to view the retrieved documents and relevant document IDs.

## Example Use Case

1. **Upload**: A user uploads a PDF document containing product features.
2. **Ask a Question**: The user asks, "What are the features of the product?"
3. **Answer Generation**: The system retrieves the relevant document chunks, ranks them based on relevance, and uses the LLM to generate a response.

## Code Walkthrough

### 1. Document Processing (`process_document`)
- This function processes the uploaded PDF into document chunks, making it easier to store and retrieve content efficiently.

### 2. Vector Collection (`get_vector_collection` & `add_to_vector_collection`)
- Manages the vector collection, creating or retrieving it and adding document chunks to it using **chromadb** and **OllamaEmbeddingFunction**.

### 3. Query Handling (`query_collection`)
- Queries the vector store to retrieve the most relevant documents based on the user's query.

### 4. Answer Generation (`call_llm`)
- Uses **Ollama's chat model** to generate an answer based on the context of the retrieved documents.

### 5. Re-ranking (`re_rank_cross_encoders`)
- Uses **CrossEncoder** to re-rank the retrieved documents based on how relevant they are to the user's query.

## Installation

1. Install the necessary libraries:

```bash
pip install streamlit chromadb ollama langchain sentence-transformers hydralit-components
