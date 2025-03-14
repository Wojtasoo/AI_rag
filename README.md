# Document Analysis Workflow

This Python script implements a document analysis workflow using LangChain and LangGraph. It processes a PDF document, retrieves relevant information based on a user's prompt, classifies the retrieved content as either technical or scientific, and then generates an answer based on the classified context.

## Features

-   **PDF Document Loading and Splitting:** Loads a PDF document from a specified path and splits it into smaller chunks for processing.
-   **Vector Database Creation:** Creates a Chroma vector database from the document chunks using specified embeddings (OpenAI or Ollama).
-   **Document Retrieval:** Retrieves relevant document chunks based on a user's prompt using similarity search.
-   **Content Classification:** Classifies the retrieved document chunks as either technical or scientific using a language model.
-   **Answer Generation:** Generates an answer based on the classified context using a language model.
-   **Prompt Rewriting:** Rewrites the user's prompt to optimize it for keyword document search.
-   **Language Model Flexibility:** Supports OpenAI, Groq, and Ollama language models.
-   **Langsmith Tracing:** Integrates with Langsmith for tracing and debugging.
-   **Interactive Input:** Takes file path, file name, and user prompt as input.
-   **Visual Graph Representation:** Generates a Mermaid graph representation of the workflow.

## Prerequisites

-   Python 3.7+
-   `pip` installed
-   An OpenAI API key or a local Ollama setup or a Groq API Key.
-   Langsmith API key (optional, for tracing)
-   `.env` file with necessary environment variables.

## Installation

1.  Clone the repository:

    ```bash
    git clone <repository_url>
    cd <repository_directory>
    ```

2.  Create a virtual environment (recommended):

    ```bash
    python3 -m venv venv
    source venv/bin/activate  # On macOS and Linux
    venv\Scripts\activate  # On Windows
    ```

3.  Install dependencies:

    ```bash
    pip install -r requirements.txt
    ```

4.  Set up environment variables:

    Create a `.env` file in the root directory and add your API keys and LLM type:

    ```plaintext
    OPENAI_API_KEY=your_openai_api_key
    # or
    OLLAMA_BASE_URL=http://localhost:11434 # default ollama url
    # or
    GROQ_API_KEY=your_groq_api_key
    LLM_TYPE=openai # or ollama or groq
    LANGSMITH_API_KEY=your_langsmith_api_key #optional
    ```

## Usage

1.  Run the script:

    ```bash
    python main.py
    ```

2.  Enter the path to the directory containing the PDF file when prompted.
3.  Enter the name of the PDF file when prompted.
4.  Enter your prompt when prompted.
5.  The script will process the PDF, retrieve relevant information, classify it, generate an answer, and print the result to the console.

## Workflow Overview

1.  **Load PDF:** The `load_pdf` function loads the PDF document.
2.  **Split Text:** The `split_text` function splits the document into smaller chunks.
3.  **Create Vector Database:** The `Chroma.from_documents` function creates a vector database from the document chunks.
4.  **Retrieve Documents:** The `retrieve_docs` function retrieves relevant document chunks based on the user's prompt.
5.  **Classify Content:** The `prompt_classifier` function classifies the retrieved document chunks as technical or scientific.
6.  **Generate Answer:** The `generate_answer` function generates an answer based on the classified context.
7.  **Prompt Rewriting:** Before retrieving documents, the `rewriter` function optimizes the user's prompt.
8.  **Output:** The generated answer is printed to the console.
9. **Graph Visualization:** A mermaid graph of the workflow is displayed if IPython is available.

## Customization

-   **LLM Selection:** Change the `LLM_TYPE` environment variable to switch between OpenAI, Ollama, and Groq language models.
-   **Embedding Selection:** Change the embedding function in `get_embeddings` to use different embeddings.
-   **Chunk Size and Overlap:** Modify the `chunk_size` and `chunk_overlap` parameters in the `split_text` function to adjust text splitting.
-   **Retrieval Parameters:** Modify the `search_kwargs` in `db.as_retriever` to adjust retrieval parameters.
-   **Prompt Templates:** Modify the prompt templates in `prompt_classifier` and `generate_answer` to customize the analysis.
-   **Vector Database:** Switch the vector database from Chroma to another supported vector database.

## Error Handling

The script includes basic error handling for file loading and API calls. Additional error handling can be added as needed.

## Langsmith Tracing

If you have a Langsmith API key, the script will automatically trace the execution, providing insights into the performance and behavior of the agents and the workflow.
