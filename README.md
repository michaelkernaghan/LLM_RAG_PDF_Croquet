# Croquet Laws and Tactics Retrieval-Augmented Generation (RAG) with Question Answering

This repository contains code to build a question-answering system around the laws and tactics of croquet using Retrieval-Augmented Generation (RAG). The system processes PDF documents, indexes them for easy retrieval, and answers questions based on the content. It utilizes a combination of MistralAI for language modelling, OpenAI embeddings for vector storage, and LangChain for document splitting and retrieval.

## Table of Contents
- [Installation](#installation)
- [Environment Variables](#environment-variables)
- [Usage](#usage)
- [Code Overview](#code-overview)
- [FAQ](#faq)
- [License](#license)

---

## Installation

Ensure you have the following Python packages installed:

```bash
pip install -qU pypdf langchain_community langchain_chroma langchain_openai langchain-mistralai
```

---

## Environment Variables

Set up your `.env` file to manage your API keys. The following environment variables are required:
- `OPENAI_API_KEY`: Your OpenAI API key.
- `MISTRAL_API_KEY`: Your Mistral AI key.

You can create the `.env` file with the following content:

```bash
OPENAI_API_KEY=your_openai_api_key_here
MISTRAL_API_KEY=your_mistral_api_key_here
```

Load the environment variables with the following command in your script:

```python
from dotenv import load_dotenv
import os

load_dotenv()
```

---

## Usage

1. Place all your croquet-related PDF files in a directory called `croquet_pdfs`.
2. Run the script to process the PDFs, generate embeddings, and set up the RAG pipeline for question answering.
3. You can invoke the question-answering system by passing a query like this:

```python
results = rag_chain.invoke({"input": "Explain what a B Baulk Tice opening is and why it is used."})
print(results["context"][0].page_content)
print(results["context"][0].metadata)
```

The system will retrieve relevant information from the PDF documents and generate a concise answer.

---

## Code Overview

- **PDF Processing:** Uses `langchain_community.PyPDFLoader` to load and process all PDFs in the `croquet_pdfs` folder.
- **Document Splitting:** `RecursiveCharacterTextSplitter` breaks down the documents into manageable chunks.
- **Embeddings:** The OpenAI embeddings model converts text into vector embeddings.
- **Vector Storage:** `Chroma` is the vector storage engine to store and retrieve document embeddings.
- **RAG Pipeline:** Combines document retrieval and Mistral's LLM to provide relevant answers based on the retrieved context.

---

## FAQ

### What is a RAG model?

RAG (Retrieval-Augmented Generation) models combine traditional retrieval-based methods with generation capabilities to answer questions. The system first retrieves relevant documents, then uses a language model to generate an answer based on the retrieved information.

### How does this system process croquet PDFs?

The system processes croquet-related PDFs, splits them into smaller chunks for efficient retrieval, and stores embeddings in a vector database. This allows for fast question-answering based on the content of the documents.

---

## License

This project is licensed under the MIT License.
