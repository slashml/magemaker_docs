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
    <li><a href="#about-model-manager">About Magemaker</a></li>
    <li>
      <a href="#getting-started">Getting Started</a>
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
Magemaker is a Python CLI that lets you deploy Hugging Face models (and AWS SageMaker JumpStart models) directly to the three major cloud providers—AWS SageMaker, Google Cloud Vertex AI, and Azure Machine Learning—without writing any cloud-specific boilerplate. Choose a model, pick an instance, and Magemaker spins up an endpoint that’s ready to query or fine-tune in just a few minutes.

---

## Getting Started
Magemaker supports **AWS, GCP, and Azure**. You can configure one, two, or all three providers in the same project.

### Prerequisites
* Python 3.11 (3.12 + 3.13 not yet supported)
* At least one cloud-provider account (AWS, GCP, Azure)
* Corresponding cloud CLI tools installed locally  
  • aws cli  • gcloud SDK  • azure cli
* Quota for the instance/GPU types you plan to use
* (Optional) Hugging Face access token for gated models such as Llama 3

### Installation
```bash
pip install magemaker
```

### Initial Cloud Configuration
Run the CLI once with the `--cloud` flag to generate a _.env_ file and store your credentials (you can pass `all` to configure every provider in one go):
```bash
magemaker --cloud [aws|gcp|azure|all]
```
If you ever need to move the config directory, set `CONFIG_DIR=/path/to/dir` in your environment.

> **Never commit your .env file to version control!**

---

## Using Magemaker

### 1. Interactive menu (recommended for exploring)
```bash
magemaker --cloud aws   # or gcp / azure / all
```
The menu lets you:
* Search & deploy **Hugging Face** or **AWS JumpStart** models
* List active endpoints
* Query or delete endpoints

### 2. Infrastructure-as-Code via YAML
For reproducible deployments & CI/CD:
```bash
magemaker --deploy .magemaker_config/your-model.yaml
```
Example (AWS SageMaker):
```yaml
deployment: !Deployment
  destination: aws
  endpoint_name: bert-demo
  instance_count: 1
  instance_type: ml.m5.xlarge
models:
  - !Model
    id: google-bert/bert-base-uncased
    source: huggingface
```
Vertex AI and Azure use the same schema with their specific `instance_type` / `accelerator_type` fields.

### 3. Fine-tuning
```bash
magemaker --train .magemaker_config/train-bert.yaml
```
If you omit common hyper-parameters, Magemaker will auto-fill sensible defaults based on the model/task.

### 4. Programmatic or REST queries
* Use the interactive **Query a Model Endpoint** menu, **or**
* Call the cloud SDK directly (see docs for each provider), **or**
* Spin up the bundled **OpenAI-compatible FastAPI proxy** (`python server.py`) and hit `/v1/chat/completions` from any OpenAI client.

---

## Deactivating Endpoints
Endpoints accrue charges while running. Delete them from the interactive menu or via the appropriate `delete_*` command to avoid unexpected costs.

---

## What we're working on next
- [ ] Improved error handling & verbose logging
- [ ] Auto-/manual scaling controls
- [ ] Deeper multi-cloud orchestration
- [ ] Additional task types (vision, audio, multimodal)

---

## Known Issues
- Querying currently supports **text-based** models only
- Endpoint deletion is asynchronous and can take a few minutes to disappear
- Deploying the **same model** twice within the **same minute** can fail due to name collisions

---

## Contributing
We welcome issues & PRs! See the [Contributing Guide](concepts/contributing) for setup instructions, testing commands, and doc guidelines.

---

## License
Apache 2.0 — see `LICENSE` for details.

---

## Contact
Questions or feedback? Email [support@slashml.com](mailto:support@slashml.com) or join our Discord (link in repository README).

<p align="right">(<a href="#readme-top">back to top</a>)</p>