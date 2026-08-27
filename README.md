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

Architecture

