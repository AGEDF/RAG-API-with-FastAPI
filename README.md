<img src="https://cdn.prod.website-files.com/677c400686e724409a5a7409/6790ad949cf622dc8dcd9fe4_nextwork-logo-leather.svg" alt="NextWork" width="300" />

# Build a RAG API with FastAPI

**Project Link:** [View Project](http://nextwork.ai/projects/ai-devops-api)

**Author:** Aadam Gandhi  
**Email:** try.aadam52@gmail.com

---

---

## Introducing Today's Project!

In this project, I'm going to learn about RAG and how implement a fast api using ollama This will help me get started with rag and fast api I'm interested in this because this is  what future is.                                          

### Key tools and concepts

The key tools I used include python, fastapi - for creating apis, pydantic- for validating input request data, ollama - nomic-embed-text, qwen2.5:0.5b , chromadb Key concepts I learnt include embeddings, vectors, prompts context, About RAG how retrieval works, augementation works and Generation works.

### Challenges and wins

This project took me approximately 2 hours because I was trying to deep dive into each code line and know how the things works. The most challenging part was understanding how chromdb stores embedding and retrieves it via semantic search.

---

## Performing RAG Manually

In this step, I'm going to See RAG in action with a manual demo but manually and RAG stands for Retrieval Augmentation and Generation

![Image](http://nextwork.ai/thankful_turquoise_clever_wombat/uploads/ai-devops-api_v3j7x5b9)

### Understanding the three parts of RAG

I performed RAG manually by retreiving i.e finding relevant text, augmentation gave that text via prompt, and then ai generated to create an accurate answer based on my prompt

### Comparing the two AI models

The key difference I noticed is that nomic-embed-text convert our text to vectors i.e numbres for it to work with our vector db (chromadb) using semantic search. 

---

## Building a Personal Knowledge Base

In this step, I will create a personal profile document, convert it into vector embeddings, and store it in a local database. This is the "Retrieval" part of RAG.

![Image](http://nextwork.ai/thankful_turquoise_clever_wombat/uploads/ai-devops-api_g3h7m2r5)

### Creating the profile document

I included information about me and Now when we pass it to RAG the model will have enough knowledge about me and it can generate grounded answers.

### How semantic search finds relevant chunks

When I ask a question, that question is converted into chunks. Now chromaDB finds chunks whose vectors are closest in that high-dimensional space. This is semantic search by chromaDB.

---

## Creating the RAG API with FastAPI

In this step, I'm going to build an API that will take user input and it will automatically retrieve context, augment the prompt, and generate a grounded answer.

![Image](http://nextwork.ai/thankful_turquoise_clever_wombat/uploads/ai-devops-api_j5m1r8t2)

### How the /ask endpoint works

When a question comes in my api. First it retrieves top 2 matching result from chromaDb and adds those matching chunks to a single string i.e chunks. Secondly it creates a prompt for model where we pass context and question . Third it sends that augmented prompt to our local LLm and returns the response to user.

### Testing with Swagger UI

I tested my API by asking what is my name and yes AI did use the chunk that i had passed earlier with profile.txt and used it as a context and give me the answer which was correct.

---

## Extending to a Multi-User AI Directory

In this project extension, I'm adding multi-user support because...Real-world RAG systems almost always serve multiple users or data sources. Adding multi-user support teaches you dynamic document ingestion, metadata filtering in vector databases, and basic multi-tenancy patterns.

![Image](http://nextwork.ai/thankful_turquoise_clever_wombat/uploads/ai-devops-api_d5g9k3n7)

### Adding the POST /documents endpoint

In this project extension, I added a POST endpoint that stores user specific data to chromadb using chromadb metadatas varaible user_name . Metadata filtering allows me to retreive that user specific context also from chromadb using     query_params = {
        "query_texts": [question],
        "n_results": 2,
    }

    # If a user name was provided, only search that user's chunks
    if user:
        query_params["where"] = {"user_name": user}  # ChromaDB metadata filter

    # Step 1: RETRIEVE - search ChromaDB for the most relevant chunks
    results = collection.query(**query_params)

![Image](http://nextwork.ai/thankful_turquoise_clever_wombat/uploads/ai-devops-api_r8t2w6y1)

### Verifying multi-user filtering

In this project extension, I tested multi-user queries by inputing user name and the question. The rag filtered username through chroma db and retrived chunks of data which was used as context for my final prompt to ai.

---

## Wrapping Up

I did this project today to learn how to create a simple RAG application which takes user profile as our ai context and whenever user asks a question I retrive that data from chromadb related to the user and generate the result via ollama model . Next what I want to learn is more deep dive context for RAG and how major companies use this and to master it.

---

---
