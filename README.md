# 📘 Intelligent document analysis system
> An intelligent document analysis system that helps users extract knowledge, connect ideas across documents, and consume insights in multiple formats — including interactive text and AI-generated podcasts.

## 🧠 Our Approach

Our primary uproach to the problem statement is 

1. Use Heading logic from previous round to detect Headings

2. Divide the pdfs into sections of format [`Header`, `Page no`,`PDF name`,`Content`] for easy processing

3. Then text sections are embedded [ converted into numerical vectors using `SentenceTransformer` Model] as these vectors capture the semantic meaning of the text

4. The above vectors are stored in specialized database called a FAISS index. This index is highly optimized for finding closest vectors to given query vector

5. When the query is passed in the form of selected text it is converted into vector. FAISS effectively compares this query vector to all vectors in its index to find most relevant matches

6. Then the relevant sections are displayed

7. These relevant sections are passed to insight generator which generates insights using `Gemini AI`

8. The relevant sections are also passed to podcast generator which calls `Gemini AI` to generate podcast script. This script is generated into audio using `AZURE TTS`

## 🌟 Key Features

✅ Bulk + single PDF upload

✅ Smart text selection → related context retrieval

✅ Semantic search & snippet navigation

✅ AI insights for deeper understanding

✅ Podcast generation for accessibility & multitasking

✅ Clean UI with dedicated pages for each step

## 🔗 Workflow

#### Step 1 – Upload Knowledge PDFs (bulk)

User uploads previously read PDFs → stored & indexed

#### Step 2 – Upload Primary PDF (single)

User uploads the PDF they are about to read

#### Step 3 – Select Text

User highlights/chooses text from the new PDF

#### Step 4 – Related Context

System shows related sections from previously read PDFs

#### Step 5 – Insights

AI (Gemini) generates contextual insights from the selection

#### Step 6 – Podcast

Insights converted to podcast audio for accessibility 🎧

## 📂 System Overview

### 🖥️ Frontend (React + Vite)

Pages:

`KnowledgeUploadPage.jsx` → Upload bulk PDFs

`PrimaryDocumentUploadPage.jsx` → Upload primary doc

`InteractiveAnalysisPage.jsx` → Select text

`ResultsDisplayPage.jsx` → View related snippets, insights & podcast

Components:

`PDFViewer`, `InsightsPanel`, `SnippetNavigator`, `PodcastPlayer`,`Selected Text Display`

⚙️ Backend (FastAPI + AI Services)

Routers:

`ingest.py` → Upload & process PDFs

`search.py` → Retrieve related sections

`insights.py` → AI insights (Gemini)

`podcast.py` → Podcast audio (Google + Azure TTS)

Services:

`pdf_reader` → Extracts text and detects header using round 1 approach [ `fitz`]

`sectionizer` → Splits into sections

`embedder` → Embeddings for semantic search [ `Sentence transformers` ]

`indexer` → Vector DB indexing & retrieval [ `faiss` ]

## 🔗 API Summary

| Method | Endpoint                | Purpose                          |
| ------ | ----------------------- | -------------------------------- |
| `POST` | `/ingest/upload_single` | Upload primary PDF               |
| `POST` | `/ingest/upload_bulk`   | Upload knowledge PDFs            |
| `POST` | `/search/`              | Get related sections             |
| `POST` | `/insights/`            | Generate insights from selection |
| `POST` | `/podcast/`             | Generate podcast audio           |

## 🐳 How to Build and Run (Documentation Only)

### ✅ Step 1: Build Docker Image

```bash
docker build --platform linux/amd64 -t yourimageidentifier .
```

### ▶️ Step 2: Run the Container

```bash
docker run 
-e ADOBE_EMBED_API_KEY=<ADOBE_EMBED_API_KEY> 
-e LLM_PROVIDER=gemini 
-e GEMINI_API_KEY="<YOUR_ACTUAL_GEMINI_API_KEY>" 
-e GEMINI_MODEL=gemini-1.5-flash 
-e TTS_PROVIDER=azure 
-e AZURE_TTS_KEY="TTS_KEY" 
-e AZURE_TTS_ENDPOINT="TTS_ENDPOINT" 
-p 8080:8080 
yourimageidentifier
```

This will:

- Run both Frontend and backend on `port 8080`
- Implements the solution

# Note to the Judges

The text selctions work as follows

- Select the text and single click the input box, the text will be automatically dropped there.

- ADOBE_EMBED_API_KEY="0ad4e2cfee304a8d9d32232d3dd9729f"

- Please provide GEMINI_API_KEY in while running the docker image

- The docker image might take more time to create.

🙋 Author

M Uday Kumar Reddy

Y Rukmangar

Web Alchemists

B.Tech CSE (Data Science)
