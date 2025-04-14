## Overview

The given changes in the codebase are related to an addition of a new command-line argument supporting YAML query configuration files in the MageMaker CLI tool. This will enhance its functionality to allow users to query deployed models using the path of a YAML configuration file.

## Detailed Changes

There's a single, but significant change in the `runner.py` file. A new command-line argument `--query` has been added to the CLI parsing script. 

### Addition of `--query` argument

A new argument called `--query` has been added to the MageMaker runner parser. This argument expects a string input which should be a path to a YAML query configuration file. Users can pass their YAML file path in the command line, which will then be used by the MageMaker to query the deployed models.

The `--query` argument is defined with the following attributes:
- `action='query'`: The 'query' action may dictate the behavior of the tool when `--query` argument is used.
- `help`: A helpful description indicating its usage i.e., "Path to YAML query configuration file" 
- `type=str`: The input for this argument should be a string type.

Thus, the new command-line interface will process the `--query` argument when it is present.

## Usage

With the addition of this `--query` argument, users can now use the MageMaker tool to query deployed models using a YAML configuration file. Here's how you can use this new functionality:

### Command Structure

```bash
magemaker --query /path/to/your/queryconfig.yaml
```

Where `/path/to/your/queryconfig.yaml` should be replaced by the actual path of your YAML query configuration file. The provided YAML file should be properly formatted as per the specifications needed by the `--query` command in the MageMaker tool.