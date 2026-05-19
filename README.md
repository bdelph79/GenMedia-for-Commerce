# 👗🔄🎥 GenMedia for Commerce Agent (ADK + Veo + Gemini)

[![Python](https://img.shields.io/badge/Python-3.11+-blue.svg)](https://www.python.org/)
[![Framework](https://img.shields.io/badge/Framework-ADK-4285F4.svg)](https://github.com/google/adk-python)
[![License](https://img.shields.io/badge/License-Apache_2.0-blue.svg)](LICENSE)

## 🎯 Executive Summary
The **GenMedia for Commerce Agent** is a production-ready creative orchestrator designed for the retail and e-commerce sectors. It automates the generation of high-fidelity retail media, including **Virtual Try-On (VTO)** videos and **360° product spins**. 

By integrating Google's **Veo 3.1** (video generation) and **Gemini 2.5** (reasoning/vision) via the **Agent Development Kit (ADK)**, it allows brands to transform static product catalogs into immersive, interactive video content at scale, significantly reducing production costs and time-to-market.

---

## 🏗️ Technical Architecture
The system employs a sophisticated workflow-based orchestration where Gemini acts as the "creative director" and Veo acts as the "production studio."

### Core Components:
- **Clothes Video VTO Pipeline**: Uses Veo 3.1 R2V (Reference-to-Video) to animate models in specific garments.
- **Shoe Spinning (R2V) Pipeline**: Generates seamless 360° rotations from a handful of static shoe images.
- **Automated Validation Loops**: Built-in rotation consistency and glitch detection to ensure commercial-grade output.
- **Infrastructure**: Optimized for **Cloud Run** and **Vertex AI Agent Runtime**.

---

## 🔄 Workflow Logic
1.  **Ingestion**: Receives product images and optional textual style prompts.
2.  **Scene Framing**: The agent automatically crops and frames images (e.g., lower body vs. face) to optimize for the video generation model's aspect ratios.
3.  **Generation (Veo)**: Calls the Veo API in parallel to generate high-resolution video clips based on the framed references.
4.  **Verification**: A dedicated validation step uses Gemini's vision capabilities to score the generated video against the original product for consistency.
5.  **Delivery**: Outputs the finalized video for use in web storefronts or marketing campaigns.

---

## 🤝 Platform Integrations

### **Gemini Enterprise Integration**
This agent can be registered as a custom application within **Gemini Enterprise**. This enables marketing teams to generate creative assets through a conversational interface while maintaining enterprise-level security and access controls.

### **Vertex AI Reasoning Engine**
Deploys as a managed service, providing:
- **High Concurrency**: Handles multiple video generation requests simultaneously.
- **Observability**: Full tracing of the creative decision-making process.

---

## 🔌 API Integration
The backend is powered by **FastAPI**, exposing REST endpoints that can be integrated into any e-commerce CMS (e.g., Shopify, BigCommerce).

### **Example: Video Generation Request**
```bash
# Trigger a 360 spin generation
curl -X POST https://genmedia-api.example.com/generate/spin      -d '{"product_id": "shoe_123", "images": ["front.jpg", "side.jpg"]}'
```

---

## 🚀 Getting Started

### **1. Installation**
```bash
# Clone and enter
git clone https://github.com/bdelph79/GenMedia-for-Commerce.git
cd GenMedia-for-Commerce

# Install Python and Frontend dependencies
make install
```

### **2. Configuration**
Edit `config.env` (see `config.env.example`):
```env
PROJECT_ID=gemini-enterprise-496008
DEFAULT_REGION=us-east1
```

---

## 📝 Prerequisites Checklist
- [ ] **Google Cloud Project**: With Veo and Vertex AI APIs enabled.
- [ ] **Terraform**: For automated infrastructure setup (`make setup-infra`).
- [ ] **Node.js 20+**: Required for the React-based management dashboard.

---
## Disclaimer
This agent sample is provided for illustrative purposes only. Users are responsible for any further development, testing, security hardening, and deployment of agents based on this sample.

---

## Global Prerequisites for All Projects

To deploy and run these agents, ensure you have the following set up:

1.  **Google Cloud Project**: An active GCP project with billing enabled.
2.  **Authentication**: 
    - Install the [Google Cloud SDK](https://cloud.google.com/sdk/docs/install).
    - Run `gcloud auth application-default login` to authenticate locally.
3.  **APIs Enabled**:
    - Vertex AI API (`aiplatform.googleapis.com`)
    - Cloud Storage API (`storage.googleapis.com`)
4.  **Environment Variables**: Create a `.env` file in the root of each project with the following:
    ```env
    GOOGLE_CLOUD_PROJECT=your-project-id
    GOOGLE_CLOUD_LOCATION=us-central1
    GOOGLE_CLOUD_STORAGE_BUCKET=your-bucket-name
    ```
5.  **Python Environment**: Python 3.10+ and [uv](https://docs.astral.sh/uv/getting-started/installation/) installed for dependency management.
