# Getting Started with Magemaker

Magemaker is a Python tool that simplifies the process of deploying an open source AI model to your own cloud. 

Deploy from an interactive menu in the terminal or from a simple YAML file.

Instead of spending hours digging through documentation to figure out how to get AWS working, Magemaker lets you deploy Hugging Face models directly to AWS SageMaker, Google Cloud Vertex AI, or Azure Machine Learning, from the command line or a simple YAML file.

Choose a model from Hugging Face, and Magemaker will spin up an instance with a ready-to-query endpoint of the model in minutes.

## Getting Started

Magemaker works with the three major cloud providers AWS, Azure and GCP!

To get a local copy up and running follow these simple steps.

### Prerequisites

* Python 3.11+ (Python 3.12 is currently not supported due to an Azure SDK issue)
* Cloud Configuration
    * An account to your preferred cloud provider, AWS, GCP and Azure.
        * Each cloud requires slightly different accesses, Magemaker will guide you through getting the necessary credentials to the selected cloud provider
        * Here's a guide on how to configure AWS and get the credentials [Google Doc](https://docs.google.com/document/d/1NvA6uZmppsYzaOdkcgNTRl7Nb4LbpP9Koc4H_t5xNSg/edit?tab=t.0#heading=h.farbxuv3zrzm)
    * Quota approval for instances you require for the AI model 
        * By default, you get some free instances, example with AWS you are pre-approved for 2 ml.m5.xlarge instances with 16gb of RAM each

    * An installation and configuration of your selected cloud CLI tool(s)
        * Magemaker will prompt you to install the CLI of the selected cloud provider, if not installed already.
        * Magemaker will prompt you to add the necesssary credentials.

* Certain Hugging Face models (e.g. Llama2) require an access token ([hf docs](https://huggingface.co/docs/hub/en/models-gated#access-gated-models-as-a-user))


## Installation

1. Install Magemaker using pip:

   ```sh
   pip install magemaker
   ```

2. Run Magemaker:

   ```sh
   magemaker --cloud [aws|gcp|azure|all]
   ```

   If this is your first time running this command, It will configure the selected cloud so you’re ready to start deploying models. 

   In the case of AWS, it’ll prompt you to enter your Access Key and Secret. You can also specify your AWS region. The default is us-east-1. You only need to change this if your SageMaker instance quota is in a different region.

   Once configured, it will create a `.env` file and save the credentials there. You can also add your Hugging Face Hub Token to this file if you have one. 

   ```sh
   HUGGING_FACE_HUB_KEY="KeyValueHere"
   ```


<br>

## Using Magemaker

### Interactive deployment

Run `magemaker --cloud [gcp|azure|aws|all]` to access an interactive menu where you can:

* Choose your cloud provider
* Select from available models
* Configure deployment settings
* Monitor deployment progress

#### YAML-based Deployment
For reproducible deployments, use YAML configuration:

```
magemaker --deploy .magemaker_config/bert-base-uncased.yaml
```

Following is a sample yaml file for deploying a model the same google bert model mentioned above to AWS:

```yaml
deployment: !Deployment
  destination: aws
  # Endpoint name matches model_id for querying atm.
  endpoint_name: test-bert-uncased
  instance_count: 1
  instance_type: ml.m5.xlarge

models:
- !Model
  id: google-bert/bert-base-uncased
  source: huggingface
```

Following is a yaml file for deploying a facebook model to GCP Vertex AI:
```yaml
deployment: !Deployment
  destination: gcp
  endpoint_name: test-endpoint-12
  accelerator_count: 1
  instance_type: g2-standard-12
  accelerator_type: NVIDIA_L4
  num_gpus: null
  quantization: null

models:
- !Model
  id: facebook/opt-125m
  location: null
  predict: null
  source: huggingface
  task: null
  version: null

```
For Azure ML:
```yaml
deployment: !Deployment
  destination: azure
  endpoint_name: facebook--opt-125m-202410251736
  instance_count: 1
  instance_type: Standard_DS3_v2
models:
- !Model
  id: facebook-opt-125m
  location: null
  predict: null
  source: huggingface
  task: text-generation
  version: null
```

#### Fine-tuning a model using a yaml file

You can also fine-tune a model using a yaml file, by using the `train` option in the command and passing path to the yaml file

`
magemaker --train .magemaker_config/train-bert.yaml
`

Here is an example yaml file for fine-tuning a hugging-face model:

```yaml
training: !Training
  destination: aws  # or gcp, azure
  instance_type: ml.p3.2xlarge  # varies by cloud provider
  instance_count: 1
  training_input_path: s3://your-bucket/data.csv
  hyperparameters: !Hyperparameters
    epochs: 3
    per_device_train_batch_size: 32
    learning_rate: 2e-5

```


<br>
<br>

If you’re using the `ml.m5.xlarge` instance type, here are some small Hugging Face models that work great:
<br>
<br>

**Model: [google-bert/bert-base-uncased](https://huggingface.co/google-bert/bert-base-uncased)**

- **Type:** Fill Mask: tries to complete your sentence like Madlibs
- **Query format:** text string with `[MASK]` somewhere in it that you wish for the transformer to fill
- 
<br>
<br>

**Model: [sentence-transformers/all-MiniLM-L6-v2](https://huggingface.co/sentence-transformers/all-MiniLM-L6-v2)**

- **Type:** Feature extraction: turns text into a 384d vector embedding for semantic search / clustering
- **Query format:** "*type out a sentence like this one.*"

<br>
<br>


## Deactivating Models

Any model endpoints you spin up will run continuously unless you deactivate them! Make sure to delete endpoints you’re no longer using so you don’t keep getting charged for your SageMaker instance.
