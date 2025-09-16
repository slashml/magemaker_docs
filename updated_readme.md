<a name="readme-top"></a>

<!-- PROJECT LOGO -->
<br />
<div align="center">
  <h3 align="center">Magemaker v0.1, by SlashML</h3>

  <p align="center">
    Deploy open source AI models to AWS, GCP, and Azure in minutes.
    <br />
  </p>
</div>



<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-model-manager">About Magemaker</a>
    </li>
    <li><a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#using-model-manager">Using Magemaker</a></li>
    <li><a href="#what-were-working-on-next">What we're working on next</a></li>
    <li><a href="#known-issues">Known issues</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
  </ol>
</details>

<!-- ABOUT THE PROJECT -->
## About Magemaker
Magemaker is a Python tool that simplifies the process of deploying an open-source AI model to **your** cloud. Instead of spending hours digging through platform-specific docs, Magemaker spins up production-ready endpoints on AWS SageMaker, Google Cloud Vertex AI, or Azure Machine Learning from a single CLI command.

Choose a model from Hugging Face, AWS JumpStart, or point Magemaker at your own model artefacts—an endpoint will be online in minutes.

<!-- GETTING STARTED -->
<br>

## Getting Started

Magemaker currently supports **AWS, GCP and Azure**. The first run guides you through the minimal configuration required for your chosen provider(s).

### Prerequisites

* Python 3.11 + (3.12 currently unsupported due to Azure SDK issue)
* Cloud account(s) & sufficient quota:
  * AWS for SageMaker
  * GCP for Vertex AI
  * Azure for Azure ML
* CLI tools (optional but recommended):
  * AWS CLI, Google Cloud SDK, Azure CLI
* Hugging Face account & token for gated models (e.g. Llama-3)

### Installation

```sh
pip install magemaker
```

### First-time configuration
Run Magemaker with your desired cloud flag. The wizard collects credentials (or points you to the relevant CLI login command), writes them to a local `.env`, and verifies quota.

```sh
magemaker --cloud [aws|gcp|azure|all]
```

Typical `.env` variables (auto-generated):
```bash
AWS_ACCESS_KEY_ID="..."      # if aws selected
AWS_SECRET_ACCESS_KEY="..."
AWS_REGION="us-east-1"
PROJECT_ID="my-gcp-project"  # if gcp selected
GCLOUD_REGION="us-central1"
AZURE_SUBSCRIPTION_ID="..."  # if azure selected
AZURE_RESOURCE_GROUP="ml-resources"
AZURE_WORKSPACE_NAME="ml-workspace"
AZURE_REGION="eastus"
HUGGING_FACE_HUB_KEY="hf_..." # optional
```

<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- USAGE -->
<br>

## Using Magemaker

### Interactive dropdown
`magemaker --cloud ...` opens an interactive menu where you can:
* Deploy a new model
* List / delete active endpoints
* Query an endpoint directly from the terminal

### YAML-based deployment (recommended)
For CI/CD or reproducibility, pass a YAML config:

```sh
magemaker --deploy .magemaker_config/bert-aws.yaml
```

Example ­– **AWS SageMaker (Hugging Face)**
```yaml
deployment: !Deployment
  destination: aws
  endpoint_name: bert-uncased-dev
  instance_count: 1
  instance_type: ml.m5.xlarge

models:
- !Model
  id: google-bert/bert-base-uncased
  source: huggingface
```

Example ­– **GCP Vertex AI**
```yaml
deployment: !Deployment
  destination: gcp
  endpoint_name: llama3-gcp
  accelerator_count: 1
  instance_type: n1-standard-8
  accelerator_type: NVIDIA_T4

models:
- !Model
  id: meta-llama/Meta-Llama-3-8B-Instruct
  source: huggingface
```

Example ­– **Azure ML**
```yaml
deployment: !Deployment
  destination: azure
  endpoint_name: llama3-azure
  instance_count: 1
  instance_type: Standard_NC24ads_A100_v4

models:
- !Model
  id: meta-llama-meta-llama-3-8b-instruct   # Azure model-catalog id
  source: huggingface
```

### AWS JumpStart & Custom models
Deploy marketplace models or your own artefacts stored locally/S3—see the [JumpStart & Custom Models](docs/concepts/jumpstart-custom-models.mdx) guide.

### Fine-tuning
```sh
magemaker --train .magemaker_config/train-bert.yaml
```
YAML follows the `!Training` schema; only AWS is supported for training today.

### Deactivating endpoints
Endpoints accrue cloud charges until deleted. Use the menu option **Delete a Model Endpoint** or run your cloud console cleanup.

<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- ROADMAP -->
<br>

## What we're working on next
- [ ] Enhanced error handling & verbose logging
- [ ] Autoscaling controls
- [ ] Streaming support in OpenAI-compatible proxy
- [ ] Additional cloud-specific optimisations

<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- ISSUES -->
<br>

## Known issues
- Query helper currently supports text-based pipelines only
- Endpoint deletion is asynchronous—may appear active for a short time after request
- Deploying the same model repeatedly within ~60 seconds can fail due to name collision (timestamp workaround in progress)

<p align="right">(<a href="#readme-top">back to top</a>)</p>


<!-- LICENSE -->
<br>

## License

Distributed under the Apache 2.0 License. See `LICENSE` for more information.

<!-- CONTACT -->
<br>

## Contact

Questions, bugs, ideas? Reach us (Faizan & Jneid) at [support@slashml.com](mailto:support@slashml.com).

We’d love your feedback!
