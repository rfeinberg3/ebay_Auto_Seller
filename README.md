# eBay_Auto_Seller

## Project Overview

eBay_Auto_Seller is a tool designed to generate descriptions for images of items that users would like to sell or resell on eBay. Leveraging eBay's extensive API support, this project aims to streamline the listing process by providing high-quality, autogenerated item descriptions. This not only saves time for sellers but also ensures that listings are detailed and appealing to potential buyers.

### Key Aspects
- **Microservice Architecture**
- **Docker Containerization**
- **REST APIs**
- **Retrieval-Augmented Generation (RAG)**
- **Data-pipeline**

## Micro-service Graph
![project_graph](https://github.com/rfeinberg3/ebay_Auto_Seller/assets/95943957/a0a61ac8-52f8-4a5b-b588-9d5fa1e9c21d)

## Why Choose eBay

With numerous e-commerce websites available, why choose eBay? While it may not be everyone's favorite e-commerce platform, I believe eBay is the best choice for this application for several important reasons.

1. **Open-Source API Support:** eBay is the most well-known e-commerce website that supports open-source RESTful API calls. Although more popular services like Facebook Marketplace and OfferUp exist, they don’t offer public APIs.

2. **Extensive Developer Support:** eBay has extensive developer support, evident through consistent updates, maintenance, and community engagement events. This robust support ensures a reliable and up-to-date API service.

3. **Vast and High-Quality Data:** eBay provides a vast quantity and quality of data, superior to other e-commerce sites like Etsy or Shopify. High-quality data is crucial for training a model to generate descriptions of everyday items people may wish to resell. Unlike Shopify and Etsy, which cater more to entrepreneurial startups, eBay's data is well-suited for this purpose.

## Why RAG?

- Significantly fights against "hallucinations".
- Allows for users of RAG based models to essentially communicate with data repositories.

[2023 Nvidia, "What is Retrieval-Augmented Generation, aka RAG?"](https://blogs.nvidia.com/blog/what-is-retrieval-augmented-generation/)

### Basic Flow of a RAG Model

1. **Knowledge Base Development**: 
   - Before the model is ready for deployment, a knowledge base must be developed.
   - The knowledge base will be embedded to create a Vector Database.
   - The database being vectorized allows for efficient lookups later on.
   - The database will essentially be machine-readable at this point.
  
2. **Querying the RAG Service**: 
   - A user can now query the RAG service.
   - The query is passed to an embedding model (tokenizer, image processor, or some other form of vectorization) which embeds the query.
   - The embedded query can now be handled by a retrieval model, which will compare the embedded query to the vectorized database and retrieve similar data to the query.
   - The retrieved data will then be decoded (into text or images) and sent along with the original query to an LLM (potentially fine-tuned) to generate a response for the user.

### Ideas

#### Use ColBERT as a Retrieval Model
- [ColBERT on GitHub](https://github.com/stanford-futuredata/ColBERT?tab=readme-ov-file)
- [ColBERTv2.0 on Hugging Face](https://huggingface.co/colbert-ir/colbertv2.0)
- This model is fast, lightweight, and can produce state-of-the-art results.
  - Param count = 110M
  - Uses PyTorch and Safetensors
  - Model size is 438MB

#### Generative Model Options
- [GPT-2 for text generation](https://huggingface.co/openai-community/gpt2/tree/main)
- BERT for fill-in-mask generation or question-answer generation? The masked part could be the item descriptions!
  - [BERT-base-uncased on Hugging Face](https://huggingface.co/google-bert/bert-base-uncased/tree/main)
- Mistral for text generation
  - [Mistral-7B-v0.1 on Hugging Face](https://huggingface.co/mistralai/Mistral-7B-v0.1?text=My+name+is+Julien+and+I+like+to)
- Phi-3 mini for text generation
  - [Phi-3 mini on Hugging Face](https://huggingface.co/microsoft/Phi-3-mini-4k-instruct?text=Give+a+seller+description+for+the+following+item+‘Apple+Watch’)

#### Use the RAGatouille Library
- [RAGatouille on GitHub](https://github.com/bclavie/ragatouille)
- This library is designed to work with ColBERT, provide modularity and ease-of-use, and is backed by research.

#### Other Models
- There are other open-source models for RAG architecture out there that could be used as well.
- One such example is Facebook's RAG-Token Model, a neat tokenizer-retriever-model pipeline. However, this pipeline would require lots of reconstruction to set up for our use case and doesn't have much supporting documentation (any really) to aid in this endeavor.
- Constructing a pipeline from scratch with the RAGatouille library seems to be a much more efficient process, provided the large amount of resources present in their framework.





