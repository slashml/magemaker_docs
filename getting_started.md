# Getting Started with Magemaker

Magemaker is a Python tool that simplifies the process of deploying an open source AI model to your own cloud. Instead of spending hours digging through documentation to figure out how to get AWS working, Magemaker lets you deploy open source AI models directly from the command line.

## Prerequisites

- Python
- An AWS account
- Quota for AWS SageMaker instances (by default, you get 2 instances of ml.m5.xlarge for free)
- Certain Hugging Face models (e.g. Llama2) require an access token ([hf docs](https://huggingface.co/docs/hub/en/models-gated#access-gated-models-as-a-user))

## Installation

1. Install Magemaker using pip:

   ```sh
   pip install magemaker
   ```

2. Run Magemaker:

   ```sh
   magemaker
   ```

   If this is your first time running this command, it will configure the AWS client so you’re ready to start deploying models. You’ll be prompted to enter your Access Key and Secret here. You can also specify your AWS region. The default is us-east-1. You only need to change this if your SageMaker instance quota is in a different region.

3. Once configured, it will create a `.env` file and save the credentials there. You can also add your Hugging Face Hub Token to this file if you have one.

   ```sh
   HUGGING_FACE_HUB_KEY="KeyValueHere"
   ```

## Deploying Models

Magemaker provides an interactive menu to deploy models. You can choose from a dropdown of models to deploy.

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
