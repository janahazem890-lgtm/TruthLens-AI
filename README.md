# 🔎 TruthLens AI

TruthLens AI is a web-based AI fact-checking system that verifies claims using a Retrieval-Augmented Generation (RAG) pipeline. It searches trusted online sources, retrieves the most relevant information, and uses Gemini AI to generate an explainable verdict.

## 🛠️ Technologies

- **Web-based RAG** – Retrieves relevant information before generating the response.
- **Gemini 3.5 Flash Lite** – Generates the final fact-checking result.
- **Serper API** – Searches Google for trusted sources.
- **BeautifulSoup** – Extracts text from web pages.
- **RecursiveCharacterTextSplitter** – Splits long documents into chunks.
- **Sentence Transformers (all-MiniLM-L6-v2)** – Creates text embeddings.
- **FAISS** – Stores and retrieves embeddings using semantic search.
- **Output Parsing** – Converts Gemini's JSON response into a structured result.
- **Gradio** – Provides a simple user interface.

## ⚙️ Workflow

```text
Claim
   ↓
Serper Search
   ↓
Extract Web Content
   ↓
Text Splitting
   ↓
Embeddings
   ↓
FAISS Retrieval
   ↓
Gemini AI
   ↓
Output Parsing
   ↓
Final Report
```

## ✨ Features

- Verify claims using trusted online sources.
- Perform semantic search with embeddings.
- Generate explainable AI-powered verdicts.
- Display confidence scores and supporting evidence.
- Simple and interactive Gradio interface.

---

## 🚀 How It Works

1. Enter a claim.
2. Search trusted sources using Serper API.
3. Extract webpage content.
4. Split the text into chunks.
5. Generate embeddings.
6. Retrieve the most relevant context using FAISS.
7. Analyze the context with Gemini AI.
8. Parse the output.
9. Display the final fact-checking result.

---

## 📊 Example Output

```json
{
  "claim": "Coffee causes dehydration.",
  "verdict": "Mostly False",
  "confidence": 92,
  "bullshit_index": 14,
  "reasoning": "Moderate coffee consumption does not cause dehydration in healthy adults."
}
```
---

## 🔑 API Keys

```env
GOOGLE_API_KEY=your_gemini_api_key
SERPER_API_KEY=your_serper_api_key
HF_TOKEN=your_huggingface_token
```

---

## ▶️ Run

```bash
jupyter notebook
```

Open:

```text
TruthLens AI.ipynb
```

---

## 🔮 Future Improvements

- Support more languages.
- Add document and image fact-checking.
- Improve source credibility analysis.
- Deploy as a web application.

---

