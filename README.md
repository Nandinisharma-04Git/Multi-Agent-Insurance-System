# Multi-Agent Insurance System

## Project Overview

A collaborative multi-agent system for researching and synthesizing insurance policy information. The system features specialized agents (Researcher and Writer) that work together through orchestrated hand-off protocols to deliver structured, high-quality outputs.

## Documentation

- **[ARCHITECTURE.md](./ARCHITECTURE.md)**: System architecture, component diagrams, and data flow
- **[LLD.md](./LLD.md)**: Low-Level Design document with detailed component specifications

## Key Features

- **Researcher Agent**: Sources policy coverage information from LLM and external APIs
- **Writer Agent**: Synthesizes and formats research data into structured outputs
- **Workflow Orchestration**: Manages agent lifecycle and hand-off protocols
- **State Management**: Persistent state across agent transitions
- **Multi-Database Support**: MongoDB, PostgreSQL, or ChromaDB

## Technology Stack

- **Framework**: CrewAI, LangChain
- **LLM**: Ollama
- **Database**: MongoDB / PostgreSQL / ChromaDB
- **External API**: Crawl API
- **Language**: Python

## Architecture Highlights

- Agent specialization with clear responsibilities
- Loose coupling through orchestration layer
- State persistence for workflow continuity
- Scalable and fault-tolerant design

