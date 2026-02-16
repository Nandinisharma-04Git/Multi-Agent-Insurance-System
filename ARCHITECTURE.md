# Multi-Agent Insurance System - Architecture Design

## 1. System Overview

The Multi-Agent Insurance System is a collaborative agent-based architecture that leverages specialized AI agents to research and synthesize insurance policy information. The system employs a hand-off protocol between agents to ensure efficient workflow orchestration.

## 2. High-Level Architecture

```mermaid
graph TB
    Client[Client Application] --> API[API Gateway]
    API --> Orchestrator[Workflow Orchestrator]
    Orchestrator --> Researcher[Researcher Agent]
    Orchestrator --> Writer[Writer Agent]
    Researcher --> LLM[Ollama LLM]
    Writer --> LLM
    Researcher --> CrawlAPI[Crawl API]
    Researcher --> DB[(Database<br/>MongoDB/PostgreSQL/ChromaDB)]
    Writer --> DB
    Orchestrator --> StateManager[State Manager]
    StateManager --> DB
```

## 3. Component Architecture

```mermaid
graph LR
    subgraph "Agent Layer"
        RA[Researcher Agent<br/>LangChain/CrewAI]
        WA[Writer Agent<br/>LangChain/CrewAI]
    end
    
    subgraph "Orchestration Layer"
        WO[Workflow Orchestrator]
        SM[State Manager]
        HP[Hand-off Protocol]
    end
    
    subgraph "Data Layer"
        DB[(Database)]
        Cache[(Cache)]
    end
    
    subgraph "External Services"
        LLM[Ollama LLM]
        CA[Crawl API]
    end
    
    RA --> WO
    WA --> WO
    WO --> SM
    WO --> HP
    RA --> LLM
    WA --> LLM
    RA --> CA
    RA --> DB
    WA --> DB
    SM --> Cache
```

## 4. Agent Communication Flow

```mermaid
sequenceDiagram
    participant Client
    participant Orchestrator
    participant Researcher
    participant Writer
    participant DB
    participant LLM

    Client->>Orchestrator: Submit Research Request
    Orchestrator->>StateManager: Initialize Workflow State
    Orchestrator->>Researcher: Assign Research Task
    Researcher->>LLM: Query Policy Coverage Info
    Researcher->>CrawlAPI: Fetch External Data
    Researcher->>DB: Store Research Findings
    Researcher->>Orchestrator: Research Complete + Hand-off
    Orchestrator->>Writer: Assign Synthesis Task
    Writer->>DB: Retrieve Research Data
    Writer->>LLM: Synthesize & Format
    Writer->>DB: Store Final Output
    Writer->>Orchestrator: Task Complete
    Orchestrator->>Client: Return Structured Output
```

## 5. Data Flow Architecture

```mermaid
flowchart TD
    Start[User Request] --> Parse[Parse Request]
    Parse --> Validate[Validate Input]
    Validate --> InitState[Initialize State]
    InitState --> Research[Researcher Agent]
    Research --> Gather[Gather Information]
    Gather --> StoreRaw[Store Raw Data]
    StoreRaw --> Handoff[Hand-off Protocol]
    Handoff --> Synthesize[Writer Agent]
    Synthesize --> Format[Format Output]
    Format --> StoreFinal[Store Final Output]
    StoreFinal --> Return[Return to Client]
```

## 6. Technology Stack

| Layer | Technology |
|-------|-----------|
| Framework | CrewAI, LangChain |
| LLM | Ollama |
| Database | MongoDB / PostgreSQL / ChromaDB |
| External API | Crawl API |
| Language | Python |
| State Management | Custom State Manager |

## 7. Key Design Principles

1. **Agent Specialization**: Each agent has a distinct role and responsibility
2. **Loose Coupling**: Agents communicate through orchestration layer
3. **State Persistence**: Workflow state is maintained across agent hand-offs
4. **Scalability**: Architecture supports horizontal scaling of agents
5. **Fault Tolerance**: Error handling and retry mechanisms at each layer

