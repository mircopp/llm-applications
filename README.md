# README

## Overview

This notebook demonstrates how to build a multitier architecture for LLM-enabled applications. It covers the following key aspects:

1. **Environment Setup**: Loading environment variables from a `.env` file and verifying their presence.
2. **OpenAI API Integration**: Setting up a connector to interact with OpenAI's GPT models.
3. **Use Case Implementation**: Classifying text descriptions using a predefined taxonomy.
4. **Monitoring and Guardrails**: Using Langfuse for monitoring and LLM Guard for input validation to ensure security and detect prompt injections.
5. **REST API Integration**: Exposing the functionality as REST endpoints using FastAPI.
6. **Storage Layer**: Adding a storage layer for result reporting and traceability.

## Prerequisites

- Python 3.8 or higher
- `pip` package manager
- `.env` file with the following variables:
  - `ORGANIZATION_ID`
  - `API_KEY`
  - `LANGFUSE_PUBLIC_KEY`
  - `LANGFUSE_SECRET_KEY`
  - `LANGFUSE_HOST`

## Setup Instructions

1. **Clone the Repository**:
   ```bash
   git clone git@github.com:mircopp/llm-applications.git
   cd llm-applications
   ```

2. **Create a Virtual Environment**:
   ```bash
   python3 -m pip install venv
   python3 -m venv ./.venv
   source ./.venv/bin/activate
   ```

3. **Install Dependencies**:
   ```bash
   cd textclassification
   pip install -r requirements.txt
   ```

4. **Prepare the Environment**:
   - Create a `.env` file in the current directory with the required variables.
   - Example `.env` file:
     ```env
     ORGANIZATION_ID=your_organization_id
     API_KEY=your_api_key
     LANGFUSE_PUBLIC_KEY=your_langfuse_public_key
     LANGFUSE_SECRET_KEY=your_langfuse_secret_key
     LANGFUSE_HOST=your_langfuse_host
     ```

5. **Run the Notebook**:
   - Start Jupyter Notebook:
     ```bash
     pip3 install jupyter
     jupyter notebook
     ```
   - Open the notebook `llmapplication.ipynb` in the browser.
   - Execute the cells sequentially to:
     - Load environment variables.
     - Test the OpenAI API connection.
     - Classify text descriptions.
     - Set up monitoring and guardrails.
     - Test the REST API endpoints.

6. **Test the REST API**:
      - Visit `http://127.0.0.1:8000/docs` to test the endpoints.
      - Alternatively, you can test the API using `curl` from the command line:
        ```bash
        curl -X POST "http://127.0.0.1:8000/classify" \
        -H "Content-Type: application/json" \
        -d '{"description": "The sun is shining today, so we decided to go to the museum."}'
        ```
        This will send a request to classify the provided description.

## Key Features

- **Monitoring**: Tracks LLM interactions using Langfuse.
- **Guardrails**: Detects and blocks malicious inputs using LLM Guard.
- **REST API**: Provides endpoints for text classification and result reporting.

## Testing

- Test the guardrails by providing various prompts to detect prompt injections.
- Use the `/classify` and `/convert` endpoints to classify descriptions and update trace scores.

## Notes

- Ensure the `iab_taxonomy.json` file is present in the working directory for taxonomy-based classification.
- The first use of LLM Guard may require downloading models automatically.