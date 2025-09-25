<a name="readme-top"></a>

<!-- PROJECT LOGO -->
<br />
<div align="center">
  <h3 align="center">Magemaker by SlashML</h3>

  <p align="center">
    Deploy open-source AI models to AWS, GCP, and Azure in minutes.
    <br />
    <a href="https://magemaker.slashml.com"><strong>📚 Full Documentation »</strong></a>
  </p>
</div>


<!-- TABLE OF CONTENTS -->
<details>
  <summary>Table of Contents</summary>
  <ol>
    <li><a href="#about-magemaker">About Magemaker</a></li>
    <li>
      <a href="#getting-started">Getting Started</a>
      <ul>
        <li><a href="#prerequisites">Prerequisites</a></li>
        <li><a href="#installation">Installation</a></li>
      </ul>
    </li>
    <li><a href="#using-magemaker">Using Magemaker</a></li>
    <li><a href="#fine-tuning">Fine-tuning</a></li>
    <li><a href="#openai-compatible-proxy">OpenAI-compatible Proxy</a></li>
    <li><a href="#roadmap">Roadmap</a></li>
    <li><a href="#known-issues">Known Issues</a></li>
    <li><a href="#contributing">Contributing</a></li>
    <li><a href="#license">License</a></li>
    <li><a href="#contact">Contact</a></li>
  </ol>
</details>

<!-- ABOUT THE PROJECT -->
## About Magemaker
Magemaker is a Python CLI and SDK that removes the pain of deploying open-source AI models to your own cloud.

• Zero-to-production in minutes on **AWS SageMaker**, **GCP Vertex AI**, or **Azure ML**  
• Supports Hugging Face models and AWS **JumpStart** models  
• Interactive TUI for one-off deployments & management  
• YAML workflow for reproducible IaC-style deployments  
• Optional FastAPI **OpenAI-compatible proxy** for drop-in integration with existing OpenAI tooling

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## Getting Started
Magemaker works on macOS/Linux and supports Python 3.11 (3.12 currently blocked by Azure SDK).

### Prerequisites
* Python 3.11+
* At least one cloud account (AWS, GCP, or Azure)
* Corresponding cloud CLI installed (`aws`, `gcloud`, or `az`)
* For gated Hugging Face models (e.g. Llama 3) a Hugging Face access token

### Installation
```bash
pip install magemaker
```

Run the CLI and pick your cloud:
```bash
magemaker --cloud [aws|gcp|azure|all]
```
On first run, Magemaker walks you through credential setup and writes a `.env` file with the required variables (see [Environment Vars](https://magemaker.slashml.com/configuration/Environment)).

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## Using Magemaker
### 1. Interactive TUI
```bash
magemaker --cloud aws   # or gcp / azure / all
```
• Deploy models from dropdown  
• List / query / delete endpoints  
• Works cross-cloud

### 2. YAML-based Deployment (CI-friendly)
```bash
magemaker --deploy .magemaker_config/bert-base-uncased.yaml
```
Example YAML for AWS SageMaker:
```yaml
deployment: !Deployment
  destination: aws
  endpoint_name: bert-uncased-demo
  instance_type: ml.m5.xlarge
  instance_count: 1
models:
- !Model
  id: google-bert/bert-base-uncased
  source: huggingface
```
GCP & Azure use the same schema; just change `destination`, `instance_type`, and optional GPU fields (`accelerator_type`, `accelerator_count`, `num_gpus`).

### 3. Deploying JumpStart Models
JumpStart models set `source: sagemaker` and can be discovered via the TUI. See the [JumpStart guide](https://magemaker.slashml.com/concepts/jumpstart-models).

### 4. Deactivate / Delete
Endpoints accrue cost until deleted. Use the TUI option **Delete a Model Endpoint** or:
```bash
magemaker --delete my-endpoint-name
```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## Fine-tuning
Fine-tuning is currently supported on **AWS SageMaker**.
```bash
magemaker --train .magemaker_config/train-bert.yaml
```
YAML snippet:
```yaml
training: !Training
  destination: aws
  instance_type: ml.p3.2xlarge
  instance_count: 1
  training_input_path: s3://your-bucket/data.csv
  hyperparameters: !Hyperparameters
    epochs: 3
    learning_rate: 2e-5
models:
- !Model
  id: google-bert/bert-base-uncased
  source: huggingface
```

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## OpenAI-compatible Proxy
Spin up a local FastAPI server that forwards `/v1/chat/completions` to any Magemaker endpoint, enabling seamless use with the OpenAI Python SDK.
```bash
python server.py  # default port 8000
```
Set `PROXY_SERVER_PORT` in `.env` to override the port. Full docs: [OpenAI Proxy](https://magemaker.slashml.com/concepts/openai-proxy).

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## Roadmap
- ✔️ Multi-cloud deployment (AWS, GCP, Azure)  
- ✔️ JumpStart model support  
- ⏳ Autoscaling controls  
- ⏳ Enhanced logging & error handling  
- ⏳ One-click cost-monitoring dashboards  

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## Known Issues
- Query helper functions currently text-only (no image/multimodal support)
- Endpoint deletion can take several minutes to reflect in the AWS console
- Deploying the same endpoint name within a single minute may cause conflicts

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## Contributing
We 💜 contributions! Please read our [Contributing Guide](https://magemaker.slashml.com/concepts/contributing) for setup, coding standards, and docs preview with Mintlify.

<p align="right">(<a href="#readme-top">back to top</a>)</p>

---

## License
Distributed under the Apache 2.0 License. See `LICENSE` for details.

---

## Contact
Questions or feedback? Reach us at [support@slashml.com](mailto:support@slashml.com) or join our [Discord](https://discord.gg/SBQsD63d).

<p align="right">(<a href="#readme-top">back to top</a>)</p>