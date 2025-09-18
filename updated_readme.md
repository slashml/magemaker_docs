<a name="readme-top"></a>

<!-- PROJECT LOGO -->
<br />
<div align="center">
  <h3 align="center">Magemaker by SlashML</h3>

  <p align="center">
    Deploy open-source AI models to AWS SageMaker, GCP Vertex AI and Azure ML in minutes.
    <br />
    <a href="https://magemaker.slashml.com"><strong>📚 Full Documentation »</strong></a>
  </p>
</div>


<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about">About Magemaker</a>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#usage">Usage</a></li>
    <li><a href="#examples">Example YAML Files</a></li>
    <li><a href="#fine-tuning">Fine-tuning</a></li>
    <li><a href="#deactivating-models">Deactivating Models</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#known-issues">Known Issues</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
  </ol>
</details>

## About
Magemaker is a Python CLI + library that abstracts away the boiler-plate of standing up inference endpoints for open-source models. Pick a Hugging Face model (or SageMaker JumpStart / custom S3 artefact) and Magemaker will deploy it to:

* **AWS SageMaker**
* **Google Cloud Vertex AI**
* **Azure Machine Learning**

It also ships with a FastAPI server that exposes the deployed endpoints through an **OpenAI-compatible proxy API** allowing you to drop-in replace `openai` calls in existing apps.

---

## Getting Started

### Prerequisites {#prerequisites}

* **Python 3.11+** (3.12 not yet supported; 3.13 blocked by Azure SDK)
* Account & basic quotas on at least one cloud provider
  * AWS ➜ SageMaker
  * GCP ➜ Vertex AI
  * Azure ➜ Azure ML Studio
* Corresponding CLI installed (`aws`, `gcloud`, `az`) – Magemaker will guide you if missing
* (Optional) **Hugging Face access token** for gated models such as Llama-3

### Installation {#installation}

```bash
pip install magemaker
```

Initialise Magemaker for your cloud(s):

```bash
# one provider
magemaker --cloud aws

# or configure several at once
magemaker --cloud all
```

The wizard collects credentials, writes them to a local `.env`, and creates any required execution roles (see docs for details).

---

## Usage {#usage}

### Interactive mode

```bash
magemaker --cloud [aws|gcp|azure|all]
```

Use the dropdown UI to:
1. Deploy a model (HF, JumpStart or custom S3)
2. List active endpoints
3. Query an endpoint
4. Delete endpoints you no longer need

### YAML-based mode (CI / reproducibility)

```bash
magemaker --deploy path/to/your-deployment.yaml
```

---

## Examples {#examples}

Deploy **BERT** to each cloud:

AWS SageMaker
```yaml
deployment: !Deployment
  destination: aws
  endpoint_name: bert-aws
  instance_type: ml.m5.xlarge
  instance_count: 1
models:
- !Model
  id: google-bert/bert-base-uncased
  source: huggingface
```

GCP Vertex AI
```yaml
deployment: !Deployment
  destination: gcp
  endpoint_name: bert-gcp
  instance_type: g2-standard-12
  accelerator_type: NVIDIA_L4
  accelerator_count: 1
models:
- !Model
  id: google-bert/bert-base-uncased
  source: huggingface
```

Azure ML
```yaml
deployment: !Deployment
  destination: azure
  endpoint_name: bert-azure
  instance_type: Standard_DS3_v2
  instance_count: 1
models:
- !Model
  id: google-bert-bert-base-uncased   # Azure uses different IDs – see docs
  source: huggingface
```

More examples (JumpStart, custom S3, quantisation, multi-model endpoints) are available in the [docs](https://magemaker.slashml.com).

---

## Fine-tuning {#fine-tuning}

```bash
magemaker --train path/to/train-config.yaml
```

See the Fine-tuning guide for supported hyper-parameters and cloud limitations.

---

## Deactivating Models {#deactivating-models}
Endpoints keep running – and billing – until deleted. Always remove endpoints you no longer need:

```bash
magemaker --cloud aws   # open the UI
# → Delete a Model Endpoint
```

Or call the deletion helpers programmatically.

---

## Roadmap {#roadmap}
- [ ] Auto-scaling controls
- [ ] Rich logging & observability
- [ ] Additional quantisation back-ends
- [ ] Automated cost optimisation recommendations

---

## Known Issues {#known-issues}
1. Query helper currently text-only (multimodal WIP)
2. Deleting endpoints can take a few minutes to propagate
3. Deploying identical endpoint names within the same minute causes conflicts

---

## Contributing {#contributing}
Want to help? Read the [Contributing Guide](https://magemaker.slashml.com/contributing) and check open issues.

---

## License {#license}
Apache 2.0 – see `LICENSE`.

---

## Contact {#contact}
Questions or feedback?  
📧 support@slashml.com  
💬 Join us on [Discord](https://discord.gg/SBQsD63d)
