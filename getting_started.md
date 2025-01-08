# Getting Started with Magemaker

Magemaker is a Python tool that simplifies the process of deploying an open source AI model to your own cloud. Instead of spending hours digging through documentation to figure out how to get AWS working, Magemaker lets you deploy open source AI models directly from the command line.

## Prerequisites

- Python
- Cloud provider accounts (AWS, GCP, or Azure)
- Cloud provider CLI tools
- Quota for cloud AI/ML instances
- Certain Hugging Face models (e.g. Llama2) require an access token ([hf docs](https://huggingface.co/docs/hub/en/models-gated#access-gated-models-as-a-user))

## Installation

1. Install Magemaker using pip:

   ```sh
   pip install magemaker
   ```

2. Run Magemaker:

   ```sh
   magemaker --cloud [aws|gcp|azure|all]
   ```

   When you first run the command, Magemaker will help you configure cloud provider credentials. You'll be guided through:
   Entering access credentials
   Specifying cloud region
   For AWS, the default region is us-east-1. You can change this if your SageMaker instance quota is in a different region. Similar configuration steps apply for GCP and Azure cloud providers.
   The configuration process creates a .env file to securely store your cloud credentials for future use.

3. Once configured, it will create a `.env` file and save the credentials there. You can also add your Hugging Face Hub Token to this file if you have one.

   ```sh
   HUGGING_FACE_HUB_KEY="KeyValueHere"
   ```

## Deploying Models

Magemaker supports multi-cloud model deployment across AWS, GCP, and Azure. The tool provides an interactive menu and flexible deployment options.

```sh
magemaker --cloud [aws|gcp|azure]
```

### Deploying Hugging Face Models

If you're deploying with Hugging Face, copy/paste the full model name from Hugging Face. For example, `google-bert/bert-base-uncased`. Note that you’ll need larger, more expensive instance types in order to run bigger models. It takes anywhere from 2 minutes (for smaller models) to 10+ minutes (for large models) to spin up the instance with your model.

### Deploying Sagemaker Models

If you are deploying a Sagemaker model, select a framework and search from a model. If you a deploying a custom model, provide either a valid S3 path or a local path (and the tool will automatically upload it for you). Once deployed, we will generate a YAML file with the deployment and model in the `CONFIG_DIR=.magemaker_config` folder. You can modify the path to this folder by setting the `CONFIG_DIR` environment variable.

### Deploy Using a YAML File

We recommend deploying through a yaml file for reproducability and IAC. From the cli, you can deploy a model without going through all the menus. You can even integrate us with your Github Actions to deploy on PR merge. Deploy via YAML files simply by passing the `--deploy` option with local path like so:

```sh
magemaker --deploy .magemaker_config/bert-base-uncased.yaml
```

## Deactivating Models

Any model endpoints you spin up will run continuously unless you deactivate them! Make sure to delete endpoints you’re no longer using so you don’t keep getting charged for your SageMaker instance.
