# Agentic AI E-Commerce Order Support & Resolution Platform

Objective: An AI-powered e-commerce support system that uses agentic workflows, LLM tool calling, REST APIs, Retrieval-Augmented Generation (RAG), and workflow state management to investigate and resolve common customer order issues.

Overview

Modern e-commerce support requests often require information from multiple systems such as order management, payments, shipping, customer support, and internal company policies.

This project explores how an LLM-powered agent can orchestrate these systems instead of acting as a simple chatbot.

The agent can:

Understand a customer's request
Determine which tools or APIs are required
Retrieve order, payment, and shipment information
Search internal policies using RAG
Maintain state across multi-step workflows
Decide the appropriate next action
Execute supported actions through tools
Escalate cases that require human intervention

The main idea is:

Business Data + Company Knowledge + Agent Reasoning → Context-Aware Resolution

Core Use Cases

The project focuses on five representative e-commerce support workflows.

1. Order Status & Tracking

Example

"Where is my order ORD-1045?"

The agent:

Identifies the order.
Retrieves order information.
Retrieves shipment information.
Returns the latest delivery status.

Demonstrates: LLM APIs, tool calling, REST APIs and LangGraph workflows.

2. Delayed Order & Policy Resolution

Example

"My order was supposed to arrive five days ago. What can I do?"

The agent:

Retrieves the order.
Checks shipment status.
Determines the delivery delay.
Searches the company's shipping/refund policies using RAG.
Generates a response grounded in the retrieved policy.

Demonstrates: RAG, embeddings, vector retrieval, pgvector and context-aware generation.

3. Refund Eligibility

Example

"I want a refund for ORD-1045."

The agent evaluates information such as:

Order status
Payment status
Shipment status
Delivery delay
Refund policy

The workflow then determines whether the request can continue automatically or requires another action.

Demonstrates: conditional routing, tool calling, workflow state and RAG.

4. Payment & Order Mismatch

Example

"My money was deducted but the order shows payment failed."

The agent:

Retrieves the order.
Retrieves payment information.
Compares both system states.
Detects inconsistencies.
Creates a support case when required.

Demonstrates: multi-step agent workflows, REST API orchestration and state management.

5. Human Escalation

Some workflows should not be completed autonomously.

For example:

"Refund €1,500 for this order."

A business rule may require human approval for high-value refunds.

The agent can:

Detect that approval is required.
Stop the autonomous execution path.
Create an escalation.
Persist the workflow state.
Continue after an approval decision.

Demonstrates: LangGraph conditional workflows, persistent state and human-in-the-loop design.

Architecture:

<img width="2816" height="1536" alt="Gemini_Generated_Image_c73yr5c73yr5c73y" src="https://github.com/user-attachments/assets/ca7085d9-a0c0-4cbb-b101-903b6d370710" />

Agent Tools

The initial version of the agent is designed around a small set of business tools.

get_order(order_id)

get_payment(order_id)

get_shipment(order_id)

search_policy(query)

create_refund_request(order_id)

create_support_ticket(order_id, reason)

escalate_to_human(order_id, reason)

The LLM determines which tools are required based on the customer request and the current workflow state.

RAG Knowledge Base

RAG is used for information that belongs to organizational knowledge rather than transactional systems.

Example documents include:

Refund Policy
Return Policy
Shipping Policy
Cancellation Policy
Payment Policy
Customer Support Procedures

The retrieval pipeline follows:

Policy Documents
      ↓
Document Processing
      ↓
Chunking
      ↓
Embeddings
      ↓
PostgreSQL / pgvector
      ↓
Semantic Retrieval
      ↓
Relevant Policy Context
      ↓
LLM
      ↓
Grounded Decision / Response

This keeps business rules separate from transactional information such as order and payment records.

Technology Stack
Technology	Purpose
Python	Core backend and AI logic
LangGraph	Agent orchestration and workflow state
LLM APIs	Intent understanding, reasoning and tool selection
RAG	Retrieval of internal policies and business knowledge
Embeddings	Semantic representation of policy documents
FastAPI	Backend and REST API layer
Tool Calling	Interaction between the agent and business services
PostgreSQL	Business and workflow data
pgvector	Vector storage and semantic retrieval
Docker	Containerized application environment
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
Planned Project Structure
agentic-ecommerce-order-resolution-platform/
│
├── app/
│   ├── main.py
│   │
│   ├── agents/
│   │   ├── graph.py
│   │   ├── nodes.py
│   │   └── state.py
│   │
│   ├── tools/
│   │   ├── order_tools.py
│   │   ├── payment_tools.py
│   │   ├── shipping_tools.py
│   │   └── support_tools.py
│   │
│   ├── rag/
│   │   ├── ingestion.py
│   │   ├── embeddings.py
│   │   └── retriever.py
│   │
│   ├── api/
│   │   └── routes.py
│   │
│   ├── database/
│   │   ├── connection.py
│   │   └── models.py
│   │
│   └── services/
│
├── data/
│   └── policies/
│
├── tests/
│
├── Dockerfile
├── docker-compose.yml
├── requirements.txt
├── .env.example
└── README.md
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
Development Roadmap
Phase 1 — Agent Foundation

Configure Python environment

Connect an LLM API

Define LangGraph workflow state

Create initial graph

Process a basic customer request

Phase 2 — Tool Calling

Implement order lookup tool

Implement payment lookup tool

Implement shipment lookup tool

Enable agent-driven tool selection

Phase 3 — REST API Integration

Build mock e-commerce services with FastAPI

Add order endpoint

Add payment endpoint

Add shipment endpoint

Connect agent tools to REST services

Phase 4 — RAG

Add sample business policies

Implement document ingestion

Generate embeddings

Configure PostgreSQL + pgvector

Implement semantic policy retrieval

Expose RAG retrieval as an agent tool

Phase 5 — Workflow State & Escalation

Persist workflow executions

Add conditional routing

Add support-ticket creation

Add refund workflow

Add human escalation path

Phase 6 — Containerization & Testing

Add Dockerfile

Add Docker Compose

Add workflow tests

Add API tests

Document sample requests and outputs

Example End-to-End Workflow
Customer Request
My order ORD-1045 is five days late and I want a refund.
Agent Workflow
Understand Request
        ↓
Detected:
Delayed Order + Refund Request
        ↓
get_order("ORD-1045")
        ↓
get_shipment("ORD-1045")
        ↓
get_payment("ORD-1045")
        ↓
search_policy("refund eligibility for delayed delivery")
        ↓
Evaluate Business Rules
        ↓
       Eligible?
       /      \
     YES       NO
      │         │
      ▼         ▼
Refund Tool   Explain Policy
      │
      ▼
Update Workflow State
      │
      ▼
Final Customer Response
Project Objective

The objective of this project is not to create another general-purpose chatbot.

It is to demonstrate how agentic AI can coordinate multiple enterprise services, retrieve organizational knowledge, maintain workflow context, and execute controlled multi-step business processes.
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
The project intentionally uses a limited set of e-commerce scenarios so that the focus remains on the underlying AI engineering architecture.

Key Concepts Demonstrated
Agentic AI workflows
Multi-step LLM orchestration
LangGraph state management
LLM tool calling
Conditional routing
REST API integration
Retrieval-Augmented Generation
Embeddings and vector search
PostgreSQL / pgvector
Human-in-the-loop workflows
Backend API development
Docker-based deployment
Disclaimer
-------------------------------------------------------------------------------------------------------------------------------------------------------------------
This is an educational portfolio project using fictional e-commerce data and mock services.

It is not affiliated with or connected to Amazon or any other e-commerce company.

