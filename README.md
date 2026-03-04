# 📄 resume-screening-rag-faiss-groq

A lightweight **Retrieval-Augmented Generation (RAG)** pipeline that screens PDF resumes by embedding them with `all-MiniLM-L6-v2`, indexing with **FAISS**, and answering recruiter queries using **LLaMA 3.1 (8B)** via **Groq API**.

> Just ask *"Who is suitable for an AI Engineer position?"* — and get an intelligent, reasoned answer.

---

## 🚀 Features

- 📂 Loads and parses multiple PDF resumes from a folder
- 🧠 Embeds resumes using `sentence-transformers` (`all-MiniLM-L6-v2`)
- ⚡ Fast similarity search using **FAISS** (Flat L2 index)
- 🤖 Top-k matching resumes passed as context to **LLaMA 3.1 8B** via Groq
- 💬 Natural language query → ranked candidate recommendation

---

## 🛠️ Tech Stack

| Tool | Purpose |
|---|---|
| `pypdf` | Extract text from PDF resumes |
| `sentence-transformers` | Embed resume text (`all-MiniLM-L6-v2`) |
| `faiss-cpu` | Vector indexing & similarity search |
| `groq` | LLM inference (LLaMA 3.1 8B Instant) |
| `python-dotenv` | Manage API keys via `.env` |

---

## 📁 Project Structure

```
resume-screening-rag-faiss-groq/
│
├── RAG.ipynb           # Main notebook
├── .env                # Your Groq API key (not committed)
├── requirements.txt    # Dependencies
└── README.md
```

---

## ⚙️ Setup & Installation

### 1. Clone the repo
```bash
git clone https://github.com/your-username/resume-screening-rag-faiss-groq.git
cd resume-screening-rag-faiss-groq
```

### 2. Install dependencies
```bash
pip install faiss-cpu sentence-transformers groq pypdf python-dotenv
```

### 3. Set up your Groq API key
Create a `.env` file in the root directory:
```
GROQ_API_KEY=your_groq_api_key_here
```
> Get your free API key at [console.groq.com](https://console.groq.com)

### 4. Add your resumes
Update the folder path in the notebook:
```python
folder = "path/to/your/resumes/folder"  # folder containing PDF resumes
```

### 5. Run the notebook
```bash
jupyter notebook RAG.ipynb
```

---

## 🔍 How It Works

```
PDF Resumes
    ↓
Extract text (pypdf)
    ↓
Embed with all-MiniLM-L6-v2
    ↓
Store in FAISS Index
    ↓
Query: "Who is suitable for AI Engineer?"
    ↓
Top-3 similar resumes retrieved
    ↓
LLaMA 3.1 8B (via Groq) generates recommendation
    ↓
✅ Best candidate with reasoning
```

---

## 💡 Example Query & Output

**Query:**
```
Which candidate is suitable for an AI Engineer position?
```

**Output:**
```
Based on the resumes, I recommend Poojasri M for the AI Engineer position.

1. Experience: Internship experience in machine learning and MLOps across 3 companies.
2. Skills: Proficient in Python, TensorFlow, Keras, Scikit-learn, and Pandas.
3. Projects: Built and deployed ML models across multiple domains.
4. Certifications: Python for Data Science, Machine Learning, Business Analyst.
5. GPA: 8.91/10 — strong academic foundation in AI & Data Science.
...
```

---

## 📌 Notes

- The FAISS index is built **in-memory** — it resets every run. For persistence, save/load the index using `faiss.write_index()` / `faiss.read_index()`.
- Works best with text-based PDFs. Scanned image PDFs may not extract correctly.
- You can change `top_k` to retrieve more or fewer candidates before passing to the LLM.

---

## 📄 License

MIT License — feel free to use, modify, and distribute.

---

## 🙌 Acknowledgements

- [Groq](https://groq.com) for blazing fast LLM inference
- [FAISS by Meta AI](https://github.com/facebookresearch/faiss) for vector search
- [Sentence Transformers](https://www.sbert.net/) for embedding models
