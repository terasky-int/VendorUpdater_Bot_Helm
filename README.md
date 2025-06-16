# AI Platform Helm Chart

This repository contains an umbrella Helm chart for deploying an AI-powered, containerized platform that includes:

- **Email Ingestor** – fetches and parses emails into structured and vector formats
- **ChromaDB** – stores semantic vectors for similarity search
- **Neo4j** – stores structured knowledge graph data
- **RAG API** – performs retrieval-augmented generation from ChromaDB and Neo4j
- **AI Agent** – intelligent interface that queries RAG API

---

## 📦 Repository Structure
ai-platform-helm/
├── Chart.yaml # Umbrella chart config
├── values.yaml # Global + subchart default values
└── charts/
├── chromadb/ # Vector database subchart
├── neo4j/ # Graph database subchart
├── email-ingestor/ # Email pipeline service
├── rag-api/ # Retrieval service
└── ai-agent/ # Final LLM-based agent service


---

## 🚀 Installation

> 📝 Ensure Helm is installed: https://helm.sh/docs/intro/install/

### 1. Clone the repository

```bash
git clone https://github.com/your-user/ai-platform-helm.git
cd ai-platform-helm```

### 2. Install dependencies

```bash
Copy
Edit
helm dependency update```

### 3. Deploy to Kubernetes

```bash
helm install ai-platform . --namespace ai-platform --create-namespace```


## ⚙️ Configuration
> All configurable values are in values.yaml. These include:
> Image tags and repositories for each service
> Service types and ports
> Environment variables for inter-service communication
> Resource requests and limits
> Storage sizes for ChromaDB and Neo4j

## 🧪 Local Testing
> To test locally with Kubernetes (e.g., via kind or minikube):

```bash
kubectl config use-context kind-kind
helm install ai-platform . --namespace dev --create-namespace```
> For dev-only workflows, consider using docker-compose for ChromaDB + Neo4j mockups.

## 🔐 Secrets
> Passwords and sensitive values should be stored using Kubernetes Secrets or Vault.
> For now, the default values include:

```yaml
neo4j:
  password: neo4jpassword

rag-api:
  env:
    NEO4J_PASS: neo4jpassword```
	

## 🛠️ Roadmap
> Add Ingress support with TLS
> Add liveness/readiness probes
> Add GitOps manifests (e.g., Argo CD Applications)
> Support Secrets via sealed-secrets or CSI driver

