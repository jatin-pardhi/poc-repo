Proposed change: add a new article to the repository

File: articles/microsoft-foundry.md
Commit message: add article: overview and getting started guide for Microsoft Azure AI Foundry

Content:

Microsoft Azure AI Foundry: Overview and Getting Started

Summary
Microsoft Azure AI Foundry (the evolution of Azure AI Studio announced in 2024) is Microsoft’s end‑to‑end platform for building, evaluating, deploying, and governing generative AI applications. It brings together a catalog of frontier and open models, tools for prompt and workflow orchestration, retrieval-augmented generation (RAG) with enterprise data, safety and compliance services, and managed deployment options on Azure.

This article provides a high‑level, public‑information overview, plus practical guidance on how to start building with Azure AI Foundry.

What Azure AI Foundry is
- A unified developer environment: A web and API experience (ai.azure.com) for creating “projects” that connect to Azure AI resources and help teams iterate from prototype to production.
- Model access in one place: A catalog that includes Azure OpenAI models (for example GPT‑4 family including GPT‑4o where available), Microsoft’s small language models (Phi‑3 family), and select open models from partners such as Meta and Mistral available as managed “model as a service” endpoints.
- Orchestration and evaluation: Tools to design and version prompts and multi‑step flows, connect tools and data, run experiments, evaluate quality, and promote versions to production.
- Enterprise‑grade guardrails: Built‑in content safety, responsible AI checks, monitoring, and governance integrated with Azure security, identity, and networking.

Key capabilities
- Model catalog and endpoints
  - Choose from curated foundation and small language models hosted by Azure.
  - Consume via standardized REST/SDK endpoints; pay as you go without managing GPUs when using model‑as‑a‑service.
- Azure OpenAI integration
  - Access OpenAI models hosted in Azure regions, with enterprise security and data residency controls.
  - Support for features like tool/function calling, embeddings, image understanding (where supported), and streaming responses.
- Prompt and workflow orchestration
  - Design prompt templates, chain steps, call tools and APIs, and manage variables.
  - Version prompts and flows; compare variants with A/B evaluation.
- Retrieval‑augmented generation (RAG)
  - Bring enterprise data to your AI app using Azure AI Search for indexing, vector search, and hybrid retrieval.
  - Ingest from common Azure data sources (for example Azure Blob Storage, Azure Data Lake, SQL) and other sources through connectors and pipelines.
  - Manage embeddings and chunking strategies from within your project.
- Evaluation and safety
  - Automated and human‑in‑the‑loop evaluation for relevance, groundedness, and harmful content.
  - Azure AI Content Safety for classification, redaction, jailbreak detection, and configurable thresholds.
  - Prompt shields and system instructions to reduce prompt injection and data leakage risks.
- Deployment and operations
  - One‑click deployment of flows and models to managed online endpoints.
  - Private networking options (private endpoints, managed VNets) and Azure RBAC with Microsoft Entra ID.
  - Integration with Application Insights and logging for latency, cost, and quality telemetry.
- Fine‑tuning and adapters
  - Fine‑tune select models and/or apply parameter‑efficient techniques (for example LoRA) where supported by the specific model offering.
- SDKs and frameworks
  - Use Python or .NET SDKs and integrate with Microsoft orchestration libraries such as Semantic Kernel; many teams also pair Foundry with agent frameworks (for example AutoGen) and popular OSS libraries.

Typical solution architecture
- Data ingestion and indexing
  - Prepare content in storage; index and chunk with Azure AI Search; generate embeddings using a supported model.
- Orchestration
  - Author a prompt flow that accepts a user question, retrieves relevant documents, calls the chosen model with a grounded prompt, and optionally invokes tools/APIs for actions.
- Evaluation
  - Create test sets and run automated evaluations for relevance, groundedness, and safety; iterate on prompts and retrieval parameters.
- Deployment
  - Deploy the flow to a managed endpoint behind a private or public front door; integrate with your app via REST; monitor usage and errors.
- Governance
  - Apply role‑based access, secrets in Key Vault, private networking, and data retention policies; enable content safety filters and monitoring dashboards.

Common use cases
- Enterprise Q&A over internal knowledge bases and documents.
- Copilots for employees (for example HR/IT self‑service, sales enablement, policy guidance).
- Customer support assistants and case deflection.
- Document intelligence and summarization with citations.
- Code and data assistants in specialized domains using smaller, efficient models.
- Agentic workflows that combine retrieval with tool execution for task automation.

Getting started
1) Set up your Azure environment
- You need an Azure subscription and appropriate role assignments (for example Owner or Contributor).
- Confirm regional availability and quotas for the models you intend to use (Azure OpenAI requires approval and quotas).

2) Create an Azure AI Foundry project
- Go to ai.azure.com and create a new project (also known as a hub/workspace in earlier materials).
- Link or provision supporting resources: Azure OpenAI, Azure AI Search, Storage (Blob), Application Insights/Log Analytics, and Content Safety depending on your scenario.

3) Choose a model
- Browse the model catalog to select a suitable model for your task and constraints.
- Consider latency, capability, cost, and compliance needs. For RAG and tool use, ensure the model supports function calling and streaming if needed.

4) Connect your data (for RAG scenarios)
- Create an Azure AI Search index; configure chunking and embeddings.
- Use indexers or pipelines to ingest from storage and databases; set schedules as needed.
- Validate retrieval quality with sample queries.

5) Build a prompt flow
- Compose a system prompt, user prompt template, retrieval step, and tool calls.
- Parameterize temperature, top‑p, max tokens, and retrieval settings for experimentation.
- Store secrets in Key Vault and use managed identity for resource access.

6) Evaluate quality and safety
- Create a test set with representative questions and expected facts.
- Run automated evaluations for relevance and groundedness; perform red‑teaming for safety.
- Iterate on prompts, chunking, and retrieval parameters based on evaluation results.

7) Deploy and integrate
- Deploy the flow to a managed online endpoint with the desired network configuration.
- Integrate from your application using the REST endpoint and API keys or managed identity.
- Set up monitoring dashboards for latency, cost per request, safety events, and user feedback.

Pricing overview
- Model usage: Charged per token or per unit (varies by model and whether using Azure OpenAI or model‑as‑a‑service).
- Azure AI Search: Indexing and query units are billed based on SKU and capacity; vector search may require specific SKUs.
- Storage and networking: Standard Azure charges for Blob/Data Lake and egress apply.
- Content Safety and evaluations: Metered per request where applicable.
- Managed endpoints: Compute and hosting costs if dedicated capacity is used.
Pricing varies by region and model. Always consult the official Azure pricing pages for the most current details.

Security, compliance, and governance
- Data isolation: Customer prompts and completions for Azure OpenAI and model‑as‑a‑service offerings are not used to train the underlying foundation models.
- Identity and access: Use Microsoft Entra ID and Azure RBAC for least‑privilege access to projects and resources.
- Network isolation: Use private endpoints and VNets for production workloads where feasible.
- Key management: Store secrets in Azure Key Vault and use customer‑managed keys for supported services if required by policy.
- Responsible AI: Apply content safety filters, jailbreak detection, and evaluation workflows; maintain human oversight for high‑impact decisions.

Model selection guidance
- Start with the smallest model that meets your quality bar to control cost and latency.
- For knowledge‑heavy tasks over your own data, invest in retrieval quality (chunking, embeddings, hybrid search) before jumping to larger models.
- Consider small language models (for example Phi‑3 family) for on‑device or constrained scenarios; for complex reasoning or multimodal tasks, evaluate larger models like GPT‑4 class where available.

Best practices
- Grounding and citations: Provide sources with responses to build trust; penalize ungrounded answers during evaluation.
- Prompt hygiene: Use clear system instructions; explicitly constrain scope; add content filters; protect tool invocation with guardrails.
- Retrieval tuning: Balance chunk size and overlap; combine keyword and vector search; deduplicate and rerank results.
- Evaluation: Maintain a golden dataset; use both automated and human evaluation; track regressions with versioned prompts and flows.
- Cost control: Set rate limits and budgets; cache intermediate results where appropriate; measure cost per task and optimize.
- Observability: Log prompts, retrieved documents (or hashes), model versions, and latency; monitor safety events and user feedback loops.

How Azure AI Foundry compares
- Versus using Azure OpenAI alone: Foundry adds a full environment for data grounding, orchestration, evaluation, deployment, and governance across many models—not just Azure OpenAI.
- Versus other clouds’ gen‑AI platforms: It is similar in scope to services like AWS Bedrock or Google Vertex AI for gen‑AI, while integrating deeply with Azure security, networking, and data services, and providing access to both OpenAI and a range of open models.

Limitations and considerations
- Regional availability and quotas vary by model; plan capacity early for production launches.
- Some features (for example specific models, fine‑tuning options, or safety tools) may be in preview in certain regions.
- Latency and cost can grow with retrieval size and tool complexity; profile and optimize before scaling.
- Always validate outputs for safety and correctness; keep humans in the loop where required by policy or regulation.

Further reading and official resources
- Azure AI Foundry (portal): https://ai.azure.com
- Azure AI documentation: https://learn.microsoft.com/azure/ai/
- Azure OpenAI Service overview: https://learn.microsoft.com/azure/ai-services/openai/overview
- Azure AI Search overview: https://learn.microsoft.com/azure/search/search-what-is-azure-search
- Azure AI Content Safety: https://learn.microsoft.com/azure/ai-services/content-safety/overview
- Semantic Kernel: https://aka.ms/semantic-kernel
- Responsible AI at Microsoft: https://aka.ms/raiguidelines

Notes
- This article is based on publicly available information as of late 2024. Features and availability change frequently; consult Microsoft’s official documentation for the latest updates.

If you’d like this added in a different location (for example docs/ or linked from README), tell me where you prefer and I’ll adjust the path and cross‑links.