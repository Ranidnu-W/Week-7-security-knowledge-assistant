# Week 7: RAG Security Knowledge Assistant — Evaluation Report

## Chatbot Link

https://cloud.flowiseai.com/chatbot/b1058bb1-d6aa-40a7-8050-941919e737a1

---

# 1. Setup Summary

- **LLM:** llama-3.3-70b-versatile via Groq
- **Embeddings:** sentence-transformers/all-MiniLM-L6-v2 via HuggingFace
- **Vector Store:** In-Memory Vector Store
- **Documents Loaded:**
  - mitre-initial-access.txt
  - mitre-credential-access.txt
  - mitre-lateral-movement.txt

The chatbot was built in Flowise Cloud using a Retrieval-Augmented Generation (RAG) architecture. Documents were uploaded as text files, split into chunks using a Recursive Character Text Splitter, converted into embeddings using HuggingFace embeddings, and stored in an In-Memory Vector Store. The chatbot used a Conversational Retrieval QA Chain connected to Groq for final answer generation.

---

# 2. Test Results

| # | Question | Used Documents? | Quality | Notes |
|---|----------|----------------|---------|-------|
| 1 | What are common techniques for credential access? | Yes | Good | Correctly listed credential access techniques from uploaded MITRE ATT&CK documents. |
| 2 | What is lateral movement? | Yes | Good | Provided an accurate explanation and included common lateral movement techniques. |
| 3 | How does credential dumping work? | Yes | Good | Correctly explained credential dumping and referenced Mimikatz usage. |
| 4 | What techniques are used in initial access? | Yes | Good | Listed phishing, spearphishing, drive-by compromise, and other techniques from the knowledge base. |
| 5 | What are the newest CVEs from 2026? | No | Good | Correctly stated that the uploaded documents did not contain information about recent CVEs. |

---

# 3. Edge Case Observations

- **Unrelated Question:**  
  When asked “What is the weather today?”, the chatbot correctly responded that it did not have enough information in the knowledge base to answer the question.

- **Topic Not in Documents:**  
  When asked about “the newest CVEs from 2026,” the chatbot stated that the uploaded documents did not contain information about CVEs or 2026 vulnerabilities.

The chatbot generally avoided hallucinations and stayed constrained to the uploaded MITRE ATT&CK knowledge base.

---

# 4. Settings Experiments

- **Temperature Change:**  
  The Groq model temperature was initially set to 0.3. Lower temperatures produced more factual and deterministic answers suitable for cybersecurity documentation retrieval.

- **Chunk Size Change:**  
  A chunk size of 1000 with 200 overlap was used. This provided enough context for accurate retrieval while maintaining focused document chunks.

- **Top K Change:**  
  The default Top K value of 4 was used. This retrieved multiple relevant document chunks for accurate responses.

---

# 5. Reflection

### What surprised you about how RAG works?

One surprising aspect was how effectively the chatbot could retrieve exact information from uploaded documents instead of relying only on general LLM knowledge. The source document references also made it easier to verify where answers came from.

### How could you improve this chatbot for real-world use?

For real-world deployment, improvements could include:
- Using a persistent vector database such as Pinecone or ChromaDB
- Adding more cybersecurity documentation and frameworks
- Improving document chunking strategies
- Adding authentication and user logging
- Deploying the chatbot with a more polished frontend

### How might you use RAG in your capstone project?

RAG could be used to build a searchable knowledge assistant for cybersecurity analysis, incident response procedures, intelligence analysis, or security operations workflows. It would allow users to query large collections of documents quickly while keeping answers grounded in trusted source material.

---

# Deliverables Included

## Screenshots
- flowise-dashboard.png
- groq-test.png
- rag-chatflow.png
- rag-response-with-sources.png
- chatbot-share-link.png

## Knowledge Base Documents
- mitre-initial-access.txt
- mitre-credential-access.txt
- mitre-lateral-movement.txt