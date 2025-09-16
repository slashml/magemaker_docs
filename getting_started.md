# Getting Started with Magemaker

Magemaker is a Python toolkit that lets you **deploy, query, and fine-tune open-source AI models on your own cloud** (AWS SageMaker, GCP Vertex AI, or Azure ML) in minutes—not hours.

• **Deploy** from an interactive TUI or a declarative YAML file.  
• **Query** directly from the CLI *or* through an OpenAI-compatible proxy server.  
• **Fine-tune** models with a single `--train` command.

---

## Supported Providers
✅ AWS SageMaker   ✅ GCP Vertex AI   ✅ Azure ML

<Note>
Python 3.11 is required (3.12 is not yet supported due to upstream SDK issues).
</Note>

---

## 1 – Prerequisites

1. Cloud account (AWS / GCP / Azure) with sufficient **instance quotas**.
2. Corresponding cloud **CLI** installed (<code>aws</code>, <code>gcloud</code>, or <code>az</code>).
3. (Optional) **Hugging Face token** for gated models like Llama 3.

---

## 2 – Installation
```bash
pip install magemaker
```

---

## 3 – Initial Configuration
Run the built-in wizard once per provider:

```bash
magemaker --cloud [aws|gcp|azure|all]
```
The wizard:
• Validates your CLI credentials  
• Writes a project-local **.env** with the required keys  
• Confirms region and default settings

---

## 4 – Typical Workflows

### a) Interactive Deployment
```bash
magemaker --cloud aws   # opens an interactive menu
```
Pick a model, choose an instance type, and watch the progress bar 🚀.

### b) YAML-based Deployment (CI-friendly)
```bash
magemaker --deploy .magemaker_config/bert.yaml
```
See the <a href="/concepts/deployment">Deployment</a> and <a href="/concepts/cli-reference">CLI Reference</a> pages for all available options.

### c) Fine-tuning
```bash
magemaker --train .magemaker_config/train-bert.yaml
```

### d) OpenAI-Compatible Proxy
Spin up a local FastAPI server that makes your endpoints accessible via `/chat/completions`:
```bash
uvicorn server:app --reload
```
Full details on the <a href="/concepts/api-proxy">API Proxy</a> page.

---

## 5 – Cleaning Up
Endpoints keep running until you delete them:
```bash
magemaker --delete my-endpoint
```
<Warning>Remember to delete endpoints you no longer need to avoid cloud charges.</Warning>

---

## Next Steps
1. Dive into the <a href="/quick-start">Quick Start</a> for hands-on examples.  
2. Browse the <a href="/concepts/cli-reference">full CLI reference</a>.  
3. Read about <a href="/concepts/fine-tuning">fine-tuning</a> and <a href="/concepts/models">supported models</a>.
