🔎 TruthLens AI

TruthLens AI is an AI-powered fact-checking system that verifies claims using a Retrieval-Augmented Generation (RAG) pipeline. Instead of relying only on the language model's internal knowledge, the system retrieves relevant information from trusted web sources, performs semantic search to find the most relevant evidence, and then asks Gemini AI to generate an explainable verdict.

---

🛠️ Technologies Used

1. Retrieval-Augmented Generation (RAG)

The core of this project is based on the RAG (Retrieval-Augmented Generation) architecture.

Traditional Large Language Models (LLMs) generate responses only from the knowledge learned during training. In contrast, RAG first retrieves external information related to the user's claim, then provides this information to the language model before generating the final response.

Our RAG pipeline follows these steps:

1. Receive the user's claim.
2. Search the web for trusted sources.
3. Extract textual content from the retrieved websites.
4. Split the text into smaller chunks.
5. Convert the chunks into vector embeddings.
6. Store the embeddings in a FAISS vector database.
7. Retrieve the most relevant chunks using semantic similarity.
8. Send both the claim and the retrieved context to Gemini AI.
9. Generate an explainable fact-checking report.

This approach allows the model to reason using fresh information from the web instead of relying only on its pre-trained knowledge.

---

2. Google Gemini 3.5 Flash Lite

The project uses Google Gemini 3.5 Flash Lite as the Large Language Model (LLM).

Gemini is responsible for analyzing the retrieved evidence and producing the final fact-checking report.

Instead of simply answering "True" or "False", Gemini generates:

- Verdict
- Confidence Score
- Bullshit Index
- Detailed Reasoning
- Supporting Evidence
- Final Summary

Using Gemini after the retrieval step significantly improves the reliability of the generated answers because it reasons over real evidence rather than answering from memory alone.

---

3. Serper API

The system retrieves real-time information using Serper API, which provides Google Search results through an API.

For every claim submitted by the user, Serper searches the web and returns relevant pages from trusted websites.

These search results become the knowledge source used by the RAG pipeline.

---

4. BeautifulSoup

After obtaining website links from Serper, the project downloads each webpage and extracts its textual content using BeautifulSoup.

This removes unnecessary HTML elements and keeps only the readable text required for analysis.

---

5. RecursiveCharacterTextSplitter

Large webpages cannot be processed efficiently as a single block of text.

The project therefore uses RecursiveCharacterTextSplitter to divide the extracted content into smaller overlapping chunks.

This improves semantic retrieval accuracy because embeddings are generated from meaningful text segments rather than entire documents.

Current configuration:

- Chunk Size: 500
- Chunk Overlap: 100

---

6. Sentence Transformers

To perform semantic search, the project converts text into dense vector representations using the model:

sentence-transformers/all-MiniLM-L6-v2

These embeddings capture the semantic meaning of the text, allowing similar information to be retrieved even if different words are used.

Both the document chunks and the user's claim are converted into embeddings before similarity search.

---

7. FAISS

The generated embeddings are stored inside FAISS (Facebook AI Similarity Search).

Specifically, the project uses IndexFlatL2 for nearest-neighbor search.

When a user submits a claim, its embedding is compared with all stored embeddings, and FAISS retrieves the most semantically relevant text chunks.

These retrieved chunks become the context passed to Gemini AI.

---

8. Gradio

The project provides an interactive web interface using Gradio.

The interface allows users to:

- Enter a claim.
- Run the fact-checking pipeline.
- View the generated verdict.
- Read the explanation.
- - See the confidence score and retrieved evidence.

Gradio makes the system easy to test without interacting directly with the source code.

---

📌 Overall Workflow

The complete pipeline can be summarized as follows:

User Claim
     │
     ▼
Serper API Search
     │
     ▼
Download Web Pages
     │
     ▼
BeautifulSoup Text Extraction
     │
     ▼
RecursiveCharacterTextSplitter
     │
     ▼
SentenceTransformer Embeddings
     │
     ▼
FAISS Similarity Search
     │
     ▼
Relevant Context
     │
     ▼
Gemini 3.5 Flash Lite
     │
     ▼
Fact-Checking Report
✨ Features

TruthLens AI provides an intelligent and explainable fact-checking pipeline with the following capabilities:

- 🔍 Search the web for relevant information using Serper API.
- 🌐 Retrieve evidence from trusted online sources.
- 📄 Extract clean textual content from web pages.
- 🧩 Split long documents into semantic chunks.
- 🧠 Generate text embeddings using Sentence Transformers.
- ⚡ Perform semantic similarity search using FAISS.
- 🤖 Analyze claims with Google Gemini 3.5 Flash Lite.
- 📊 Produce an explainable fact-checking report including:
  - Verdict
  - Confidence Score
  - Bullshit Index
  - Reasoning
  - Supporting Evidence
  - Source Links

---

📂 Project Structure

TruthLens-AI/
│
├── TruthLens AI.ipynb      # Main notebook
├── README.md               # Project documentation
├── requirements.txt        # Required libraries
└── assets/                 # Images (optional)

---

🚀 How It Works

Step 1 – User Input

The user enters a claim that needs to be verified.

Example:

«"Coffee causes dehydration."»

---

Step 2 – Web Search

The system sends the claim to Serper API, which performs a Google search and returns relevant web pages from trusted sources.

---

Step 3 – Content Extraction

Each webpage is downloaded, and BeautifulSoup extracts the readable text while removing unnecessary HTML elements.

---

Step 4 – Text Chunking

The extracted content is divided into smaller overlapping chunks using RecursiveCharacterTextSplitter.

This improves retrieval quality by ensuring each chunk contains meaningful information.

---

Step 5 – Embedding Generation

Each text chunk is converted into a numerical vector using the Sentence Transformers (all-MiniLM-L6-v2) embedding model.

The user's claim is also converted into an embedding.

---

Step 6 – Semantic Retrieval

All document embeddings are stored inside FAISS.

The embedding of the user's claim is compared against all stored vectors, and the most semantically relevant chunks are retrieved.

---

Step 7 – AI Reasoning

The retrieved context and the original claim are sent to Google Gemini 3.5 Flash Lite.

Gemini analyzes the evidence and determines whether the claim is true, false, misleading, partially true, or unverified.

---

Step 8 – Final Report

The system generates a structured response containing:

- Claim
- Verdict
- Confidence Score
- Bullshit Index
- Explanation
- Supporting Evidence
- References
🔑 Required API Keys
Create a .env file and add your API keys:
GOOGLE_API_KEY=your_gemini_api_key SERPER_API_KEY=your_serper_api_key HF_TOKEN=your_huggingface_token 
