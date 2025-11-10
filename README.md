# VibeMatcher
AI bridges human creativity and data intelligence. By embedding fashion items and user “vibes” into a shared semantic space, this prototype shows how AI can understand emotion-driven aesthetics—helping users discover products that feel right, not just look right.
Vibe Matcher is a lightweight AI-powered recommendation prototype developed for Nexora, designed to align fashion products with a user’s aesthetic mood or vibe query.
It demonstrates how semantic embeddings can translate emotional intent (“cozy winter cabin vibes”) into relevant product matches.

#How It Works
Data Preparation
A curated dataset of 10 mock fashion products was created, each containing:
name: Product name
desc: Short description
vibes: Associated aesthetic tags (e.g., ["boho", "cozy"])

##Embeddings Generation
Initially, the project used Gemini 2.5 (gemini-embedding-001) via the Google Generative AI API to convert product descriptions and vibe queries into high-dimensional embeddings.
Due to API quota limitations, embeddings were automatically backed up using a local SentenceTransformer model (all-mpnet-base-v2).
This hybrid design ensured that the system worked both online and offline without breaking execution.

##Similarity Matching
Each query’s embedding is compared with all product embeddings using cosine similarity (sklearn.metrics.pairwise.cosine_similarity).
Top-3 items are recommended if their similarity score ≥ 0.74.
If no high-similarity results are found, the system gracefully switches to a fallback showing trending/random items.

#Evaluation & Metrics
3 test queries were evaluated with latency tracking (timeit).
Key metrics: Precision@3, average latency, and fallback rate.
Results and latency plots are generated using Matplotlib + Seaborn.

##Deployment Example
The notebook includes a deployment-ready function (vibe_match(query)) which can easily be connected to a Gradio UI or API endpoint for real-world demos.
This makes it a plug-and-play module for internal Nexora AI showcases.

##Privacy Note
The Gemini API key is intentionally hidden in the notebook for privacy and security reasons.
A local JSON cache (embedding_cache.json) was implemented to avoid re-calling the API on re-runs, improving speed and protecting credentials.

##Results Summary
Query Example	Result Type	Fallback Used	Latency (ms)
Energetic urban chic for a night out in Tokyo	SBERT Fallback	~1570
Cozy winter cabin weekend with books and fire	SBERT Fallback	~1260
Ethereal fairy princess garden party vibes	SBERT Fallback	~1310

Average Latency: ~1382 ms
Model Used: Gemini 2.5 (Primary) + SBERT (Fallback)

##Reflection
Hybrid architecture (Gemini + SBERT) ensures zero downtime.
Embedding cache drastically improves re-runs and cost efficiency.
The model handled low-similarity queries using a clear fallback message.
Future improvement: integrate Pinecone or FAISS for faster vector search and scalable deployment.

##Tech Stack
Python, Pandas, NumPy, scikit-learn, SentenceTransformers, Google Generative AI, Matplotlib, Seaborn, Tenacity

##Conclusion
The Vibe Matcher prototype showcases how Nexora can combine AI and fashion intelligence to create emotionally aware, aesthetic-driven recommendations. Even with quota restrictions, the system maintained reliability through fallback logic and demonstrated readiness for real-world deployment.
