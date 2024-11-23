# Identity and Access Management in LLM apps with Python, LangChain, and Pangea

> This tutorial is also available on the [Pangea Documentation](https://pangea.cloud/docs/ai-security/langchain-python-rag-iam) website, where you can learn more about Pangea's services.

In this tutorial, we will demonstrate how to implement Identity and Access Management (IAM) in a retrieval-augmented generation (RAG) application built with LangChain and Python, using Pangea security services.

Integrating enterprise data into your generative AI app adds significant value. To use this information effectively, it must be embedded in vectors for semantic comparison. However, without clearly defined, deterministic security boundaries in the vectorized data and robust authorization controls, sensitive or restricted information may be inadvertently exposed. This can lead to risks outlined in OWASP's Top 10 for LLMs and Generative AI Apps, including [LLM06: Sensitive Information Disclosure](https://genai.owasp.org/llmrisk/llm06-sensitive-information-disclosure/) and [LLM10: Model Theft](https://genai.owasp.org/llmrisk/llm10-model-theft/). Additionally, a lack of user authentication can hinder tracking, analyzing, and preventing malicious attempts to manipulate LLM behavior through unregulated and unaccountable queries, as described in [LLM01: Prompt Injection](https://genai.owasp.org/llmrisk/llm01-prompt-injection/).

You will add authentication and authorization to a LangChain app, enabling the following capabilities:

- Identify users and restrict access to the app and its resources.
- Implement access control in a retrieval system by tagging vectors with resource-specific metadata at ingestion time and enforcing authorization policies aligned with this metadata.
- Apply filtering logic to ensure only vectors matching the user’s permissions are retrieved at inference time.

This, in turn, provides the following controls:

- Enables tracking of user activity for monitoring, auditing, compliance, and forensic analysis (OWASP LLM01, LLM10)
- Enhances privacy and prevents accidental data leakage (OWASP LLM06)

## Prerequisites

### Python

- Python v3.10 or greater
- pip v23.0.1 or greater

### OpenAI API key

In this tutorial, we use OpenAI models. Get your [OpenAI API key](https://platform.openai.com/api-keys) to run the examples.

## Setup

1. Clone this repository.

   ```bash title="Create project folder"
   git clone https://github.com/pangeacyber/langchain-python-rag-iam.git
   cd langchain-python-rag-iam
   ```

1. Create and activate a Python virtual environment in your project folder. For example:

   ```bash
   python -m venv .venv
   source .venv/bin/activate
   ```

1. Install the required packages.

   ```bash
   pip install -r requirements.txt
   ```

1. Save credentials and environment-specific settings as environment variables.

   Create a `.env` file and add your OpenAI API key. Use the [.env.example](.env.example) file included in this repository as a template.

   ```bash title=".env file"
   # OpenAI
   OPENAI_API_KEY="sk-proj-54bgCI...vG0g1M-GWlU99...3Prt1j-V1-4r0MOL...X6GMA"
   ```

1. Open the provided Jupyter notebook, [langchain-python-rag-iam.ipynb](langchain-python-rag-iam.ipynb), and run the code examples in your Python environment.

   [Jupyter notebooks](https://jupyter.org/) provide a popular way to execute Python code interactively. You can [install Jupyter](https://jupyter.org/install) on your system or use an IDE extension.

   > Be sure to select the kernel in your local `.venv` environment if it is not automatically set by your IDE.
