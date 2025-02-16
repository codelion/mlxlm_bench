# MLX-LM Benchmark Tool

## Overview

The MLX-LM Benchmark Tool is a high-performance, extensible Python utility designed to rigorously evaluate MLX-LM models. This tool is engineered for technical users and researchers who require detailed performance metrics for language models. By generating synthetic prompt tokens and invoking the model’s generation pipeline, the benchmark records key metrics such as tokens-per-second (TPS), execution time, and peak memory usage. The tool supports multiple models and flexible configuration of prompt and generation token lengths, allowing for comprehensive cross-model comparisons and performance tuning.

## Features

- **Multi-Model Benchmarking:**  
  Benchmark one or more MLX-LM models in a single run by specifying multiple model paths with repeated `-m/--model` options.

- **Flexible Token Configuration:**  
  Accept multiple values for synthetic prompt tokens (`-p/--n-prompt`) and generation tokens (`-n/--n-gen`) (including comma-separated lists) to simulate a wide range of input sizes.

- **Performance Metrics:**  
  Parse detailed output logs from the model’s `generate()` function to extract:
  - Prompt token count and TPS.
  - Generation token count and TPS.
  - Estimated execution time.
  - Peak memory (RAM) usage in GB.

- **Repetition & Averaging:**  
  Execute multiple benchmark iterations per configuration to provide statistically meaningful averages and mitigate performance variability.

- **Multi-Format Output:**  
  Save aggregated results in CSV, JSON, JSONL, or Markdown formats for easy integration into CI pipelines or further analysis.

## macOS Minimum Requirements

- **Operating System:** macOS Mojave (10.14) or later.
- **Processor:** 64-bit Intel or Apple Silicon.
- **Memory:** Minimum 8GB RAM (16GB or more recommended for heavier models).
- **Python:** Version 3.7 or newer is required.

## Requirements

This tool leverages the MLX-LM framework and associated dependencies. Ensure you have the following installed:

- **Python 3.7+**
- **MLX-LM Dependencies:**
  - `mlx-core`
  - `mlx-nn`
  - `mlx-lm`

All required packages are listed in the [requirements.txt](requirements.txt) file.

## Installation

1. **Clone the Repository:**

   ```
   bash
   git clone https://github.com/your-repo/mlx-lm-benchmark.git
   cd mlx-lm-benchmark
   ```

2. **Create and Activate a Virtual Environment (Recommended):**
    ```
    python3 -m venv venv
    source venv/bin/activate
    ```

3. **Install Dependencies:**
    ```
    pip install -r requirements.txt
    ```

## Usage
Run the benchmark script from the command line, specifying your desired models and token configurations. For example:

    ```
    python benchmark.py -m models/7B/ggml-model-q4_0.gguf -m models/13B/ggml-model-q4_0.gguf -p 128 -n 128,256,512

    ```
In this example:
- Two models are benchmarked.
- A single prompt token configuration (`128`) is used.
- Three different generation token configurations (`128`, `256`, and `512`) are tested.

## Command-Line Options
- **`-m, --model`**
Specify the path to an MLX-LM model. Can be used multiple times for benchmarking several models. Default: `mlx-community/llama2-7b-mlx`
Example: `-m models/7B/model1 -m models/13B/model2`

- **`-p, --n-prompt`**
Specify one or more values (or comma-separated lists) for synthetic prompt tokens. Default: `512`
Example: `-p 0,128`

- **`-n, --n-gen`**
Specify one or more values (or comma-separated lists) for generation tokens. Default: `512`
Example: `-n 128,256,512`

- **`-o, --output`**
Output format for the benchmark results. Supported formats: csv, json, jsonl, md. Default: `md`
Example: `- o json`

- **`-r, --repetitions`**
Number of iterations per configuration to average out performance results. Default: `5`
Example: `-r 10`

## Benchmarking Methodology
1. **Warmup Phase:**
Each model configuration is first warmed up to ensure that any lazy initializations (e.g., JIT compilation, memory allocation) are complete before measurements begin.
2. **Benchmark Execution:**
For each combination of model, prompt token count, and generation token count, the tool runs a series of benchmark iterations. Synthetic tokens are generated using a random sampling of the model’s vocabulary, and the model's generate() function is invoked in verbose mode to capture detailed performance logs.
3. **Metric Aggregation:**
Captured logs are parsed to extract key metrics, which are then averaged over the specified repetitions to provide robust performance statistics.

## Converting Models to MLX Format
If you have a pretrained model in another format and need to convert it for use with MLX-LM, refer to the official model conversion guide. The conversion typically involves:
- Converting model weights and configurations to be compatible with MLX-LM.
- Ensuring that the tokenizer aligns with MLX-LM expectations.
- Validating the converted model using provided test scripts.
For full conversion instructions, please visit the MLX-LM Conversion Guide.

## Contributing
Contributions to enhance the MLX-LM Benchmark Tool are welcome.

## Contact
For questions, support, or feedback, please open an issue in the repository or contact the maintainer at gauri.nagavkar@gmail.com.