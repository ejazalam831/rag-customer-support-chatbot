# RAG-Powered Customer Support Chatbot

A comprehensive implementation of a Retrieval Augmented Generation (RAG) system for customer support using LangChain, LangGraph, and Mistral AI. This project demonstrates how to build an intelligent chatbot that grounds all responses in the sample knowledge base while maintaining conversation context.

![Python](https://img.shields.io/badge/python-3.8+-blue?logo=python&logoColor=white)
![RAG](https://img.shields.io/badge/technique-RAG-red)
![LangChain](https://img.shields.io/badge/powered%20by-LangChain-blue)
![LangGraph](https://img.shields.io/badge/orchestrated%20with-LangGraph-green)
![Mistral AI](https://img.shields.io/badge/LLM-Mistral%20AI-orange)
![Chroma](https://img.shields.io/badge/vector%20db-Chroma-purple)
![Gradio](https://img.shields.io/badge/interface-Gradio-orange?logo=gradio&logoColor=white)


## 🚀 Features

- **Knowledge Base Integration**: Load and process customer support documentation from JSON files
- **Semantic Search**: Use vector embeddings for intelligent document retrieval
- **Conversation Memory**: Maintain context across multi-turn conversations
- **Response Generation**: Ensure all responses are grounded in official documentation
- **Web Interface**: User-friendly Gradio interface for easy interaction
- **Session Management**: Handle multiple concurrent conversations
- **Real-time Responses**: Powered by Mistral AI's small model with 131k token context window

## 🏗️ Architecture

The system implements a two-phase RAG architecture:

### Indexing Phase
1. **Document Loading**: Parse JSON knowledge base into structured documents
2. **Text Processing**: Split documents into manageable chunks
3. **Embedding**: Convert text to vector representations using sentence-transformers
4. **Storage**: Store embeddings in Chroma vector database

### Query Phase
1. **Retrieval**: Find semantically similar documents for user queries
2. **Context Assembly**: Combine retrieved information with conversation history
3. **Generation**: Generate responses using Mistral AI 
4. **Memory Persistence**: Maintain conversation state across interactions

## 📋 Prerequisites

- Mistral AI API key ([Get one here](https://docs.mistral.ai/getting-started/quickstart/))

## 📁 Project Structure

```
rag-customer-support-chatbot/
├── rag_customer_support_chatbot.ipynb    # Main implementation notebook
├── knowledge_base.json                   # Sample customer support FAQ
└── README.md                             # This file
```

## 🚀 Quick Start

1. **Clone the repository**
   ```bash
   git clone https://github.com/ejazalam831/rag-customer-support-chatbot.git
   cd rag-customer-support-chatbot
   ```

2. **Set up your API key**

   **Option A: Environment Variable**
   ```bash
   export MISTRAL_API_KEY="your-api-key-here"
   ```

   **Option B: Google Colab Secrets** (if using Colab)
   - Go to the secrets panel in Colab
   - Add `MISTRAL_API_KEY` with your API key

   **Option C: Manual Entry**
   - The notebook will prompt you to enter your API key if not found

3. **Run the notebook**
   - Open `rag_customer_support_chatbot.ipynb` in Jupyter or Google Colab
   - Run all cells sequentially
   - The Gradio interface will launch automatically

## 📝 Usage Examples

### Basic Q&A
```
User: What are the benefits of becoming a member?
Assistant: Being a member provides several benefits including guidance from our experts, access to member-only experiences, special offers, and free shipping on eligible orders...

User: How do I sign up?
Assistant: To sign up for membership, you can visit our website and create an account...
```

### Multi-turn Conversation
```
User: What payment methods do you accept?
Assistant: We accept various payment methods including credit cards, debit cards, PayPal, and gift cards...

User: Are there any fees for using PayPal?
Assistant: Based on our payment information, there are no additional fees for using PayPal as a payment method...
```

## 🔧 Configuration

### Model Settings
```python
llm = ChatMistralAI(
    model="mistral-small-latest",
    temperature=0.5,      # Controls response randomness
    max_tokens=512        # Maximum response length
)
```

### Retrieval Settings
```python
# Number of documents to retrieve
retrieved_docs = vector_store.similarity_search(query, k=2)

# Embedding model configuration
embeddings = HuggingFaceEmbeddings(
    model_name="sentence-transformers/all-MiniLM-L6-v2"
)
```

## 📊 Knowledge Base Format

The system expects a JSON file with the following structure:

```json
{
  "knowledge_base": [
    {
      "category": "MEMBERSHIP & ACCOUNT",
      "questions": [
        {
          "question": "How do I create an account?",
          "answer": "To create an account, visit our website..."
        }
      ]
    }
  ]
}
```

## 🔍 Key Components

### 1. Document Processing
- Loads FAQ data from JSON format
- Creates LangChain `Document` objects with metadata
- Preserves category and source information

### 2. Vector Storage
- Uses Chroma for local vector database
- Stores document embeddings for semantic search

### 3. Conversation Management
- Implements LangGraph's `MessagesState` for conversation tracking
- Uses `MemorySaver` for session persistence
- Supports multiple concurrent conversations

### 4. Response Generation
- Grounds all responses in knowledge base
- Maintains conversation context

## 🙏 Acknowledgments

- [LangChain](https://python.langchain.com/) for the RAG framework
- [LangGraph](https://langchain-ai.github.io/langgraph/) for workflow orchestration
- [Mistral AI](https://docs.mistral.ai/getting-started/quickstart/) for the language model
- [Gradio](https://www.gradio.app/docs/) for the web interface

---

⭐ If this project helped you, please give it a star! It helps others discover the project.
