flowchart TD

    subgraph Client["Frontend (Next.js)"]
        UI["React UI<br/>ShadCN Components"]
        AuthClient["Auth Client (Clerk / Supabase Auth)"]
        APIClient["API Calls / SWR / React Query"]
    end

    subgraph Edge["Edge Layer (Vercel / Cloudflare Workers)"]
        EdgeRouter["Edge Router"]
        EdgeFunctions["Edge Functions<br/>Request Pre-processing"]
    end

    subgraph Backend["Backend API (FastAPI / Node.js)"]
        APIRouter["REST / GraphQL Routes"]
        BusinessLogic["Business Logic Layer"]
        RAG["RAG Pipeline<br/>Chunking + Embeddings + Retrieval"]
    end

    subgraph DB["Storage Layer"]
        SQLDB["Supabase Postgres"]
        VectorDB["Vector Store (Supabase Vector / Pinecone)"]
        FileStore["Object Storage<br/>(Supabase Storage / S3)"]
    end

    subgraph AI["AI Providers"]
        OpenAI["OpenAI GPT-5 / Embeddings"]
        Anthropic["Anthropic Claude"]
        Groq["Groq Llama 3.2 Inference"]
    end

    %% Connections
    UI --> AuthClient
    UI --> APIClient --> EdgeRouter --> EdgeFunctions --> APIRouter

    APIRouter --> BusinessLogic
    BusinessLogic --> SQLDB
    BusinessLogic --> FileStore
    BusinessLogic --> VectorDB

    BusinessLogic --> RAG --> VectorDB
    RAG --> OpenAI
    RAG --> Anthropic
    RAG --> Groq

    APIClient --> UI
