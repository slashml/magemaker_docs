# Getting Started with Magemaker

Magemaker is a Python tool that simplifies the process of deploying an open-source AI model to your own cloud.

Deploy from an interactive menu in the terminal or from a simple YAML file.

Instead of spending hours digging through documentation, Magemaker lets you deploy models directly to AWS SageMaker, Google Cloud Vertex AI, or Azure ML— all from the command line or a YAML file.

Choose a model from Hugging Face, SageMaker JumpStart, or even an S3 path, and Magemaker will spin up an instance with a ready-to-query endpoint in minutes.

## Getting Started

Magemaker works with the three major cloud providers—AWS, Azure and GCP!

To get a local copy up and running follow these simple steps.

### Prerequisites

* Python 3.11+ (Python 3.12 is not supported; Python 3.13 is not supported for Azure)
* Cloud Configuration
    * An account on your preferred cloud provider (AWS, GCP, Azure)
    * Appropriate instance quotas for the models you plan to run (e.g., AWS gives 2 × `ml.m5.xlarge` for free by default)
    * Installation of the relevant cloud CLI tool(s) — Magemaker will prompt you to install or configure them if missing
* Certain Hugging Face models (e.g., Llama 2/3) require an access token ([HF docs](https://huggingface.co/docs/hub/en/models-gated#access-gated-models-as-a-user))

### Installation

1. Install Magemaker using pip:

   ```sh
   pip install magemaker
   ```

2. Run Magemaker for initial configuration:

   ```sh
   magemaker --cloud [aws|gcp|azure|all]
   ```

   If this is your first time running the command, Magemaker will configure the selected cloud(s) so you’re ready to start deploying models.

   *AWS example*: you’ll be prompted for your Access Key and Secret Key and, optionally, your region (default `us-east-1`).  
   Once complete, Magemaker creates a `.env` file with your credentials.  You can also add your Hugging Face Hub Token here:

   ```bash
   HUGGING_FACE_HUB_KEY="your-hf-token"
   ```

<br>

## Using Magemaker

### Interactive Deployment

Run `magemaker --cloud [gcp|azure|aws|all]` to access an interactive menu where you can:

* Choose your cloud provider
* Select from available models
  * **Hugging Face** — paste the full model ID (e.g., `google-bert/bert-base-uncased`)
  * **SageMaker JumpStart** — search and pick a JumpStart model
  * **Custom** — provide a local path or S3 URI to a model
* Configure deployment settings (instance type, GPU count, etc.)
* Monitor deployment progress in real time

### YAML-based Deployment (recommended for CI/CD)

Deploy reproducibly by passing a YAML file:

```sh
magemaker --deploy .magemaker_config/bert-base-uncased.yaml
```

Sample YAML for deploying a Hugging Face model to AWS:

```yaml
deployment: !Deployment
  destination: aws
  endpoint_name: test-bert-uncased
  instance_count: 1
  instance_type: ml.m5.xlarge

models:
- !Model
  id: google-bert/bert-base-uncased
  source: huggingface
```

Sample YAML for deploying a SageMaker JumpStart model:

```yaml
deployment: !Deployment
  destination: aws
  endpoint_name: jumpstart-llm
  instance_count: 1
  instance_type: ml.g5.2xlarge

models:
- !Model
  id: huggingface-llm/amazon-llama2-7b
  source: sagemaker  # JumpStart models use the "sagemaker" source
```

Sample YAML for GCP Vertex AI:

```yaml
deployment: !Deployment
  destination: gcp
  endpoint_name: test-endpoint-12
  accelerator_count: 1
  instance_type: g2-standard-12
  accelerator_type: NVIDIA_L4

models:
- !Model
  id: facebook/opt-125m
  source: huggingface
```

Sample YAML for Azure ML:

```yaml
deployment: !Deployment
  destination: azure
  endpoint_name: facebook--opt-125m-202410251736
  instance_count: 1
  instance_type: Standard_DS3_v2
models:
- !Model
  id: facebook-opt-125m
  source: huggingface
  task: text-generation
```

### Fine-tuning a Model

Fine-tune via YAML with the `--train` flag:

```sh
magemaker --train .magemaker_config/train-bert.yaml
```

```yaml
training: !Training
  destination: aws  # or gcp, azure
  instance_type: ml.p3.2xlarge
  instance_count: 1
  training_input_path: s3://your-bucket/data.csv
  hyperparameters: !Hyperparameters
    epochs: 3
    per_device_train_batch_size: 32
    learning_rate: 2e-5

models:
- !Model
  id: google-bert/bert-base-uncased
  source: huggingface
```

<br>

If you’re using the `ml.m5.xlarge` instance type, here are some small Hugging Face models that work great:

**Model:** [google-bert/bert-base-uncased](https://huggingface.co/google-bert/bert-base-uncased)

- **Type:** Fill Mask
- **Query format:** sentence containing `[MASK]`

**Model:** [sentence-transformers/all-MiniLM-L6-v2](https://huggingface.co/sentence-transformers/all-MiniLM-L6-v2)

- **Type:** Feature extraction
- **Query format:** plain sentence

<br>

## Deactivating Models

Any endpoints you spin up will continue running until deleted. Be sure to remove unused endpoints to avoid unexpected charges.
