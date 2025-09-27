<a name="readme-top"></a>

<!-- PROJECT LOGO -->
<br />
<div align="center">
  <h3 align="center">Magemaker by SlashML</h3>

  <p align="center">
    Deploy open-source AI models to AWS, GCP, and Azure in minutes.
    <br />
  </p>
</div>



<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li>
      <a href="#about-magemaker">About Magemaker</a>
    </li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#using-magemaker">Using Magemaker</a></li>
    <li><a href="#advanced-features">Advanced Features</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#known-issues">Known Issues</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
  </ol>
</details>

<!-- ABOUT THE PROJECT -->
## About Magemaker

Magemaker is a Python CLI and SDK that lets you deploy Hugging Face (and SageMaker JumpStart) models to **AWS SageMaker, Google Cloud Vertex AI, or Azure Machine Learning** with a single command or YAML file. Skip hours of provider-specific setup—Magemaker provisions infrastructure, uploads your model, and returns a ready-to-query endpoint in minutes.

---

## Getting Started

Magemaker supports **all three major cloud providers**. You can configure one, two, or all three at any time.

### Prerequisites

* Python 3.11+ (Python 3.12 is currently unsupported; Python 3.13 unsupported for Azure, see Azure SDK issue)
* At least one cloud account:
  * AWS account + AWS CLI (for SageMaker)
  * GCP project + Google Cloud SDK (for Vertex AI)
  * Azure subscription + Azure CLI (for Azure ML)
* Sufficient quotas for the instance types/GPU types you plan to use
* (Optional) Hugging Face token for gated models such as Llama 3

### Installation

```bash
pip install magemaker
```

### First-Time Configuration

Run the CLI with your desired provider—Magemaker will guide you through credential setup and generate a `.env` file automatically:

```bash
# Configure one provider
magemaker --cloud aws       # or gcp | azure

# Or configure everything at once
magemaker --cloud all
```

The generated `.env` contains keys such as `AWS_ACCESS_KEY_ID`, `PROJECT_ID`, `AZURE_SUBSCRIPTION_ID`, etc. **Never commit this file to version control.**

If you have a Hugging Face token add it here as well:

```dotenv
HUGGING_FACE_HUB_KEY="hf_..."
```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## Using Magemaker

### Interactive Menu

```bash
magemaker --cloud [aws|gcp|azure|all]
```

The interactive menu lets you:
* Deploy new endpoints
* List active endpoints
* Query or delete endpoints

### YAML-Driven Deployment (CI/CD Friendly)

```bash
magemaker --deploy .magemaker_config/bert-uncased.yaml
```

Example AWS deployment file:

```yaml
deployment: !Deployment
  destination: aws
  endpoint_name: bert-uncased-aws
  instance_count: 1
  instance_type: ml.m5.xlarge

models:
- !Model
  id: google-bert/bert-base-uncased
  source: huggingface
```

GCP example:

```yaml
deployment: !Deployment
  destination: gcp
  endpoint_name: bert-uncased-gcp
  instance_type: n1-standard-8
  accelerator_type: NVIDIA_TESLA_T4
  accelerator_count: 1

models:
- !Model
  id: google-bert/bert-base-uncased
  source: huggingface
```

Azure example:

```yaml
deployment: !Deployment
  destination: azure
  endpoint_name: bert-uncased-azure
  instance_count: 1
  instance_type: Standard_DS3_v2

models:
- !Model
  id: google-bert-bert-base-uncased   # Azure IDs differ—check Azure Model Catalog
  source: huggingface
```

### Fine-Tuning

```bash
magemaker --train .magemaker_config/train-bert.yaml
```
(See docs/fine-tuning for full YAML schema.)

### Cleaning Up

Endpoints accrue cloud charges until deleted. Use the interactive menu or:

```bash
magemaker --cloud aws   # select "Delete a Model Endpoint"
```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## Advanced Features

* **Multi-Cloud YAML** – Deploy the same model to multiple clouds from one config
* **SageMaker JumpStart Support** – Use `source: sagemaker` to deploy marketplace models
* **OpenAI-Compatible Proxy** – Run `python server.py` to expose any SageMaker endpoint via the OpenAI chat/completions API (see docs/tutorials/openai-compatible-proxy)
* **Config Directory Override** – Set `CONFIG_DIR` env var to change where Magemaker writes YAMLs

---

## Roadmap

- [ ] Enhanced error handling and verbose logging
- [ ] Autoscaling enable/disable flags
- [ ] Additional quantization options
- [ ] Expanded fine-tuning support on GCP & Azure

---

## Known Issues

- Query utility currently supports text-based models only
- Deleting an endpoint may take a few minutes to propagate
- Deploying the exact same model within one minute can fail due to name collisions

---

## Contributing

We love contributions! See the [CONTRIBUTING.md](CONTRIBUTING.md) guide for details.

---

## License

Distributed under the Apache 2.0 License. See `LICENSE` for details.

---

## Contact

Questions or feedback? [support@slashml.com](mailto:support@slashml.com) or join our [Discord](https://discord.gg/SBQsD63d).

<p align="right">(<a href="#readme-top">back to top</a>)</p>