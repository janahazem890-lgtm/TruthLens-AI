🔎 TruthLens AI

TruthLens AI is an AI-powered fact-checking system that helps users verify whether a claim is true or false. Instead of relying only on the AI model's knowledge, the system searches trusted online sources, retrieves the most relevant information, and then uses Gemini AI to generate a clear and explainable verdict.

---

🛠️ Technologies Used

Retrieval-Augmented Generation (RAG)

This project is built using a Web-based RAG pipeline.

When a user submits a claim, the system searches trusted websites, extracts useful content, converts it into embeddings, retrieves the most relevant information, and passes that context to Gemini AI before generating the final answer.

Using RAG helps the model rely on up-to-date information instead of only its pre-trained knowledge.

---

Google Gemini 3.5 Flash Lite

Gemini is the main language model used to analyze the retrieved information and generate the final fact-checking result.

The response includes:

- Verdict
- Confidence Score
- Bullshit Index
- Reasoning
- Supporting Evidence
- Summary

---

Serper API

Serper API is used to perform Google searches and retrieve relevant pages related to the user's claim.

---

BeautifulSoup

BeautifulSoup extracts the readable text from the retrieved web pages while removing unnecessary HTML content.

---

RecursiveCharacterTextSplitter

The extracted text is split into smaller overlapping chunks before generating embeddings, making semantic retrieval more accurate.

- Chunk Size: 500
- Chunk Overlap: 100

---

Sentence Transformers

The project uses the all-MiniLM-L6-v2 model to convert both the document chunks and the user's claim into vector embeddings for semantic search.

---

FAISS

FAISS is used as the vector database to store embeddings and retrieve the most relevant text chunks based on semantic similarity.

---

Output Parsing

Gemini returns the result in a structured JSON format. The system parses this output to extract the required fields before displaying them in the interface.

The parsed output includes:

- Verdict
- Confidence Score
- Bullshit Index
- Reasoning
- Supporting Evidence
- References

---

Gradio

Gradio provides a simple web interface where users can enter a claim and instantly receive the fact-checking result.

---

📌 Workflow

User Claim
      │
      ▼
Serper API Search
      │
      ▼
Extract Web Content
      │
      ▼
Text Splitting
      │
      ▼
SentenceTransformer Embeddings
      │
      ▼
FAISS Retrieval
      │
      ▼
Gemini 3.5 Flash Lite
      │
      ▼
Output Parsing
      │
      ▼
Fact-Checking Report

---

✨ Features

- Search trusted web sources.
- Extract and process webpage content.
- Perform semantic search using embeddings.
- Retrieve the most relevant evidence with FAISS.
- Analyze claims using Gemini AI.
- Parse the AI response into a structured report.
- Display the final verdict with supporting evidence.

---

🚀 How It Works

1. The user enters a claim.
2. The system searches the web using Serper API.
3. Relevant webpage content is extracted using BeautifulSoup.
4. The text is split into smaller chunks.
5. Embeddings are generated using Sentence Transformers.
6. FAISS retrieves the most relevant chunks.
7. Gemini analyzes the retrieved context.
8. The output is parsed into a structured format.
9. The final fact-checking report is displayed.

---

🔑 Required API Keys

Create a ".env" file and add your API keys.

GOOGLE_API_KEY=your_gemini_api_key
SERPER_API_KEY=your_serper_api_key
HF_TOKEN=your_huggingface_token