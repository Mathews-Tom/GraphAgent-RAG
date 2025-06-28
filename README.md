# 🤖 🧠 GraphAgent-RAG 🕸️ 🔗

GraphAgent-RAG is an advanced agentic knowledge retrieval framework that seamlessly fuses Retrieval-Augmented Generation (RAG) with knowledge graph intelligence.
It leverages an AI agent system that orchestrates semantic vector search with structured graph reasoning to deliver deep, contextual insights on big tech companies and their AI initiatives.

![GraphAgent-RAG](assets/GraphAgent-RAG.png)

## 🎯 Core Capabilities

- **Semantic Search**: Uses PostgreSQL with pgvector to perform high-dimensional vector similarity searches over textual and unstructured data.
- **Temporal Knowledge Graphs**: Powered by Neo4j and Graphiti, capturing evolving relationships, events, and timelines within the tech ecosystem.
- **Agentic Orchestration**: Intelligent agents dynamically decide when to query the vector index versus traverse the knowledge graph, enabling more nuanced, multi-hop question answering and analytics.

The goal of GraphAgent-RAG is to push the boundaries of traditional RAG by integrating rich graph-based reasoning, creating a system capable of not just retrieval but deeper synthesis and storytelling around complex corporate and AI landscapes.

## 🚀 Key Features

- **Hybrid Search Architecture**: Seamlessly combines vector similarity search with graph traversal for comprehensive information retrieval
- **Temporal Knowledge Graphs**: Tracks how information evolves over time using Graphiti's temporal capabilities
- **Intelligent Agent System**: Pydantic AI-powered agent that automatically selects optimal search strategies
- **Streaming API**: Real-time responses with Server-Sent Events for interactive experiences
- **Semantic Chunking**: LLM-powered document splitting that preserves context and meaning
- **Multi-Provider Support**: Compatible with OpenAI, Ollama, OpenRouter, Gemini, and other LLM providers
- **Production Ready**: Comprehensive testing, logging, error handling, and monitoring

## 🏛️ System Architecture

The GraphAgent RAG system implements a sophisticated hybrid architecture that combines traditional vector-based RAG with temporal knowledge graphs to provide comprehensive and intelligent information retrieval. The system is designed around three core components that work together to process documents, extract knowledge, and serve intelligent responses.

### Core Components

**1. Ingestion Pipeline**: Processes raw documents through semantic chunking, embedding generation, and knowledge graph construction, storing the results in both PostgreSQL (for vector search) and Neo4j (for graph traversal).

**2. RAG Agent**: An intelligent Pydantic AI agent that automatically selects and combines multiple search strategies (vector, graph, hybrid) based on query characteristics, providing contextually relevant responses with proper source attribution.

**3. API & CLI Interfaces**: FastAPI-based streaming API with real-time Server-Sent Events and an interactive CLI that provides direct access to the agent's capabilities with full tool visibility.

### Data Flow Architecture

The system processes information through a carefully orchestrated pipeline that transforms raw documents into a queryable knowledge base accessible through multiple search modalities.

### 📊 System Architecture Diagram

```mermaid
graph TD
    %% Input Layer
    A[📄 Raw Documents<br/>Markdown Files] --> B[🔄 Document Ingestion Pipeline]
    
    %% Ingestion Pipeline Components
    B --> C[📝 Semantic Chunker<br/>LLM-powered splitting]
    C --> D[🧠 Embedding Generator<br/>Vector representations]
    C --> E[🕸️ Knowledge Graph Builder<br/>Entity & relationship extraction]
    
    %% Storage Layer
    D --> F[(🗄️ PostgreSQL + pgvector<br/>Vector Database)]
    E --> G[(🌐 Neo4j + Graphiti<br/>Temporal Knowledge Graph)]
    
    %% Agent Layer
    H[🤖 Pydantic AI Agent<br/>Intelligent orchestrator] --> I[🔍 Vector Search Tool<br/>Semantic similarity]
    H --> J[🕸️ Graph Search Tool<br/>Relationship traversal]
    H --> K[🔀 Hybrid Search Tool<br/>Combined approach]
    H --> L[📋 Document Tools<br/>Full text retrieval]
    H --> M[🔗 Entity Tools<br/>Relationship analysis]
    
    %% Tool Connections to Storage
    I --> F
    J --> G
    K --> F
    K --> G
    L --> F
    M --> G
    
    %% Interface Layer
    N[💬 User Query] --> O[🌐 FastAPI Server<br/>Streaming endpoints]
    O --> H
    H --> P[📤 Intelligent Response<br/>Multi-source synthesis]
    P --> O
    O --> Q[🖥️ CLI Interface<br/>Interactive terminal]
    O --> R[🔗 HTTP API<br/>REST endpoints]
    
    %% Session Management
    O --> S[(💾 Session Storage<br/>Conversation context)]
    
    %% Styling
    classDef input fill:#e1f5fe,stroke:#01579b,stroke-width:2px
    classDef processing fill:#f3e5f5,stroke:#4a148c,stroke-width:2px
    classDef storage fill:#e8f5e8,stroke:#1b5e20,stroke-width:2px
    classDef agent fill:#fff3e0,stroke:#e65100,stroke-width:2px
    classDef interface fill:#fce4ec,stroke:#880e4f,stroke-width:2px
    
    class A input
    class B,C,D,E processing
    class F,G,S storage
    class H,I,J,K,L,M agent
    class N,O,P,Q,R interface
```

</details>

### Component Details

**Ingestion Pipeline (`ingestion/`)**:

- [`chunker.py`](ingestion/chunker.py): Implements semantic chunking using LLM analysis to preserve document context and meaning
- [`embedder.py`](ingestion/embedder.py): Generates vector embeddings using configurable providers (OpenAI, Ollama, etc.)
- [`graph_builder.py`](ingestion/graph_builder.py): Extracts entities, relationships, and temporal information using Graphiti
- [`ingest.py`](ingestion/ingest.py): Orchestrates the complete ingestion pipeline with progress tracking and error handling

**RAG Agent (`agent/`)**:

- [`agent.py`](agent/agent.py): Main Pydantic AI agent with intelligent tool selection and context management
- [`tools.py`](agent/tools.py): Implements search tools for vector, graph, hybrid, and document retrieval
- [`api.py`](agent/api.py): FastAPI server with streaming endpoints and session management
- [`db_utils.py`](agent/db_utils.py): PostgreSQL operations for vector search and document storage
- [`graph_utils.py`](agent/graph_utils.py): Neo4j and Graphiti integration for knowledge graph operations

**Storage Systems**:

- **PostgreSQL + pgvector**: Stores document chunks with vector embeddings for semantic similarity search
- **Neo4j + Graphiti**: Maintains temporal knowledge graph with entities, relationships, and time-based facts
- **Session Storage**: Preserves conversation context and user interactions

### Search Strategy Selection

The agent intelligently selects search strategies based on query characteristics:

- **Vector Search**: For semantic and conceptual queries (*"AI research at Meta"*)
- **Graph Search**: For relationship and temporal queries (*"Microsoft OpenAI partnership timeline"*)
- **Hybrid Search**: For comprehensive analysis requiring both semantic and exact matching
- **Entity Analysis**: For exploring connections and relationships between specific entities
- **Document Retrieval**: For accessing complete source documents and detailed context

This architecture enables the system to provide comprehensive, contextually relevant responses by leveraging the strengths of both vector similarity search and graph-based relationship analysis.

## 📋 Prerequisites

- **Python**: 3.12 or higher
- **PostgreSQL**: Database with pgvector extension (e.g., Neon, local PostgreSQL)
- **Neo4j**: Graph database instance (local or cloud)
- **LLM Provider**: API access to OpenAI, Ollama, Gemini, or compatible service
- **uv**: Modern Python package manager

## 🛠️ Installation

### 1. Install uv Package Manager

If you don't have `uv` installed:

```bash
# macOS/Linux
curl -LsSf https://astral.sh/uv/install.sh | sh

# Windows
powershell -c "irm https://astral.sh/uv/install.ps1 | iex"

# Or via pip
pip install uv
```

### 2. Set Up Project Environment

```bash
# Clone the repository
git clone <repository-url>
cd GraphAgent-RAG

# Create virtual environment and install dependencies
uv venv
source .venv/bin/activate  # On Linux/macOS
# or
.venv\Scripts\activate     # On Windows

# Install all dependencies
uv sync
```

### 3. Database Setup

#### Option A: PostgreSQL with pgvector

Execute the SQL schema to create required tables:

```bash
# Apply database schema
psql -d "$DATABASE_URL" -f sql/schema.sql
```

**Important**: Adjust embedding dimensions in `sql/schema.sql` (lines 31, 67, 100) based on your embedding model:

- OpenAI `text-embedding-3-small`: 1536 dimensions
- Ollama `nomic-embed-text`: 768 dimensions

#### Option B: Using a Cloud Service (e.g., Neon)

If you prefer using a managed cloud database service, you can set up PostgreSQL with a provider like [Neon](https://neon.tech/).

**Steps to use Neon's SQL Editor:**

1. Open the Neon Console at [console.neon.tech](https://console.neon.tech/) and select your project.
2. Navigate to the **SQL Editor**.
3. Paste the entire content of `sql/schema.sql` into the editor.
4. Click **Run**.

The editor supports executing multiple statements at once. You can verify the table creation by using meta-commands like `\dt` or `\d <table>` after execution.

#### Neo4j Setup

##### Option A: Neo4j Desktop (Recommended)

1. Download [Neo4j Desktop](https://neo4j.com/download/)
2. Create new project and local DBMS
3. Start DBMS and set password
4. Note connection details (URI: `bolt://localhost:7687`)

##### Option B: Neo4j Cloud

1. Create account at [Neo4j AuraDB](https://neo4j.com/cloud/aura/)
2. Create new instance
3. Download connection credentials

### 4. Environment Configuration

Create `.env` file in project root:

```bash
# Database Configuration
DATABASE_URL=postgresql://username:password@host:port/database

# Neo4j Configuration
NEO4J_URI=bolt://localhost:7687
NEO4J_USER=neo4j
NEO4J_PASSWORD=your_password

# LLM Provider Configuration
LLM_PROVIDER=openai
LLM_BASE_URL=https://api.openai.com/v1
LLM_API_KEY=sk-your-api-key
LLM_CHOICE=gpt-4o-mini

# Embedding Configuration
EMBEDDING_PROVIDER=openai
EMBEDDING_BASE_URL=https://api.openai.com/v1
EMBEDDING_API_KEY=sk-your-api-key
EMBEDDING_MODEL=text-embedding-3-small

# Ingestion Configuration
INGESTION_LLM_CHOICE=gpt-4o-mini

# Application Configuration
APP_ENV=development
LOG_LEVEL=INFO
APP_PORT=8058
```

#### Alternative LLM Providers

**Ollama (Local)**:

```bash
LLM_PROVIDER=ollama
LLM_BASE_URL=http://localhost:11434/v1
LLM_API_KEY=ollama
LLM_CHOICE=qwen2.5:14b-instruct
```

**OpenRouter**:

```bash
LLM_PROVIDER=openrouter
LLM_BASE_URL=https://openrouter.ai/api/v1
LLM_API_KEY=your-openrouter-key
LLM_CHOICE=anthropic/claude-3-5-sonnet
```

**Google Gemini**:

```bash
LLM_PROVIDER=gemini
LLM_BASE_URL=https://generativelanguage.googleapis.com/v1beta
LLM_API_KEY=your-gemini-key
LLM_CHOICE=gemini-2.0-flash-exp
```

## 🚀 Quick Start Guide

### 1. Prepare Documents

Add your markdown documents to the `documents/` directory:

```bash
mkdir -p documents
# Add your markdown files
# Example: documents/company_analysis.md
#          documents/market_research.md
```

The system includes sample documents in `docs_example/` covering major tech companies and AI initiatives.

### 2. Run Document Ingestion

**Critical**: Run ingestion before starting the agent to populate databases.

```bash
# Basic ingestion with semantic chunking
uv run -m ingestion.ingest

# Clean existing data and re-ingest
uv run -m ingestion.ingest --clean

# Track time taken for complete ingestion
time uv run -m ingestion.ingest --clean

# Fast processing without knowledge graph
uv run -m ingestion.ingest --chunk-size 800 --no-semantic --verbose
```

**Processing Overview**:

- Semantic chunking preserves document context
- Vector embeddings enable similarity search
- Knowledge graph extraction identifies entities and relationships
- Temporal information tracks changes over time

**Note**: Knowledge graph construction is computationally intensive and may take 30+ minutes for large document sets.

### 3. Start the API Server

```bash
# Launch FastAPI server
uv run -m agent.api

# Server available at http://localhost:8058
# API documentation at http://localhost:8058/docs
```

### 4. Interactive CLI Interface

Open a new terminal and start the CLI:

```bash
# Start interactive CLI
uv run python cli.py

# Connect to custom URL/port
uv run python cli.py --url http://localhost:8058
uv run python cli.py --port 8080
```

#### CLI Features

- **Real-time Streaming**: See responses as they're generated
- **Tool Visibility**: Understand which search strategies the agent uses
- **Session Management**: Maintains conversation context
- **Color-coded Output**: Enhanced readability

#### Example CLI Session

```
🤖 Agentic RAG with Knowledge Graph CLI
============================================================
Connected to: http://localhost:8058

You: What are the latest AI developments at Google?

🤖 Assistant:
Google has been making significant advances in AI across multiple areas...

🛠 Tools Used:
  1. vector_search (query='Google AI developments', limit=10)
  2. graph_search (query='Google AI projects timeline')

────────────────────────────────────────────────────────────

You: How does Google's AI strategy compare to Microsoft's?

🤖 Assistant:
Comparing Google and Microsoft's AI strategies reveals distinct approaches...

🛠 Tools Used:
  1. hybrid_search (query='Google Microsoft AI strategy comparison', limit=15)
  2. get_entity_relationships (entity='Google')
  3. get_entity_relationships (entity='Microsoft')
```

## 🔧 API Usage

### Health Check

```bash
curl http://localhost:8058/health
```

### Non-streaming Chat

```bash
curl -X POST "http://localhost:8058/chat" \
  -H "Content-Type: application/json" \
  -d '{
    "message": "Explain the competitive landscape in AI"
  }'
```

### Streaming Chat

```bash
curl -X POST "http://localhost:8058/chat/stream" \
  -H "Content-Type: application/json" \
  -d '{
    "message": "What are the key partnerships in the AI industry?"
  }'
```

### Direct Search Endpoints

**Vector Search**:

```bash
curl -X POST "http://localhost:8058/search/vector" \
  -H "Content-Type: application/json" \
  -d '{"query": "machine learning innovations", "limit": 5}'
```

**Graph Search**:

```bash
curl -X POST "http://localhost:8058/search/graph" \
  -H "Content-Type: application/json" \
  -d '{"query": "OpenAI Microsoft partnership"}'
```

**Hybrid Search**:

```bash
curl -X POST "http://localhost:8058/search/hybrid" \
  -H "Content-Type: application/json" \
  -d '{"query": "AI startup acquisitions", "limit": 10}'
```

## 🧠 How It Works

### The Power of Hybrid RAG + Knowledge Graph

**Vector Database (PostgreSQL + pgvector)**:

- Semantic similarity search across document chunks
- Fast retrieval of contextually relevant information
- Excellent for finding documents about similar topics
- Handles fuzzy matching and conceptual queries

**Knowledge Graph (Neo4j + Graphiti)**:

- Temporal relationships between entities (companies, people, technologies)
- Graph traversal for discovering hidden connections
- Perfect for understanding partnerships, acquisitions, and evolution
- Tracks how facts change over time

**Intelligent Agent Orchestration**:

- Automatically selects optimal search strategy based on query type
- Combines results from multiple sources for comprehensive answers
- Provides context-aware responses with proper source attribution
- Learns from conversation history to improve relevance

### Query Types and Strategies

**Semantic Queries**: *"What AI research is happening at Meta?"*

- Uses vector search to find relevant document chunks
- Leverages embedding similarity for conceptual matching

**Relationship Queries**: *"How are Microsoft and OpenAI connected?"*

- Uses knowledge graph traversal to explore partnerships
- Reveals direct and indirect connections between entities

**Temporal Queries**: *"Show me the timeline of Google's AI announcements"*

- Leverages Graphiti's temporal capabilities
- Tracks evolution and changes over time

**Complex Analysis**: *"Compare the AI strategies of major tech companies"*

- Combines vector search for strategy documents
- Uses graph traversal for competitive analysis
- Synthesizes information from multiple sources

## 📁 Project Structure

```
GraphAgent-RAG/
├── agent/                    # AI agent and API components
│   ├── __init__.py
│   ├── agent.py              # Main Pydantic AI agent with tools
│   ├── api.py                # FastAPI application and endpoints
│   ├── db_utils.py           # PostgreSQL database utilities
│   ├── graph_utils.py        # Neo4j and Graphiti integration
│   ├── models.py             # Pydantic data models
│   ├── prompts.py            # System prompts and templates
│   ├── providers.py          # LLM provider abstractions
│   └── tools.py              # Agent tool implementations
├── ingestion/                # Document processing pipeline
│   ├── __init__.py
│   ├── ingest.py             # Main ingestion orchestrator
│   ├── chunker.py            # Semantic document chunking
│   ├── embedder.py           # Embedding generation
│   └── graph_builder.py      # Knowledge graph construction
├── sql/
│   └── schema.sql            # PostgreSQL database schema
├── documents/                # Your markdown documents
├── docs_example/             # Sample documents (tech industry)
├── tests/                    # Comprehensive test suite
│   ├── agent/
│   └── ingestion/
├── cli.py                    # Interactive command-line interface
├── pyproject.toml            # Project configuration and dependencies
└── README.md                 # This file
```

## 🧪 Testing

Run the comprehensive test suite:

```bash
# Run all tests
pytest

# Run with coverage report
pytest --cov=agent --cov=ingestion --cov-report=html

# Run specific test modules
pytest tests/agent/
pytest tests/ingestion/

# Run with verbose output
pytest -v --tb=short
```

## 🔍 Troubleshooting

### Database Connection Issues

**PostgreSQL**:

```bash
# Test connection
psql -d "$DATABASE_URL" -c "SELECT 1;"

# Check pgvector extension
psql -d "$DATABASE_URL" -c "SELECT * FROM pg_extension WHERE extname = 'vector';"
```

**Neo4j**:

```bash
# Test Neo4j connection (adjust URL/credentials)
curl -u neo4j:password http://localhost:7474/db/data/
```

### Common Issues

**No Results from Agent**:

- Ensure ingestion pipeline has been run: `uv run -m ingestion.ingest --verbose`
- Check database connections and data presence
- Verify embedding model dimensions match schema

**LLM API Errors**:

- Validate API keys and provider configuration in `.env`
- Check rate limits and quota usage
- Test with different models if available

**Performance Issues**:

- Use `--no-semantic` flag for faster ingestion without knowledge graph
- Adjust chunk sizes and batch processing parameters
- Consider using local models (Ollama) for development

**Memory Issues**:

- Reduce batch sizes in embedding generation
- Use streaming responses for large queries
- Monitor PostgreSQL and Neo4j memory usage

### Logging and Debugging

Enable detailed logging:

```bash
# Set environment variable
export LOG_LEVEL=DEBUG

# Or in .env file
LOG_LEVEL=DEBUG
```

Check application logs for detailed error information and performance metrics.

## 🤝 Contributing

1. Fork the repository
2. Create a feature branch: `git checkout -b feature-name`
3. Make changes and add tests
4. Run test suite: `pytest`
5. Submit a pull request

## 📄 License

This project is licensed under the MIT License. See the [LICENSE](LICENSE) file for details.

## 🙏 Acknowledgments

Built with powerful open-source technologies:

- **[Pydantic AI](https://github.com/pydantic/pydantic-ai)**: Modern AI agent framework
- **[Graphiti](https://github.com/getzep/graphiti)**: Temporal knowledge graph library
- **[FastAPI](https://fastapi.tiangolo.com/)**: High-performance web framework
- **[PostgreSQL](https://www.postgresql.org/)** + **[pgvector](https://github.com/pgvector/pgvector)**: Vector database
- **[Neo4j](https://neo4j.com/)**: Graph database platform

---

**GraphAgent RAG** - Redefining knowledge retrieval through intelligent agent orchestration and hybrid search architectures.
