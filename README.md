# MLX-LM Benchmark Tool

The MLX-LM Benchmark Tool is a Python utility that evaluates the inference performance of MLX-LM models. It offers functionality similar to [llama-bench](https://github.com/ggml-org/llama.cpp/tree/master/examples/llama-bench), providing an easy way to benchmark your models.


## Requirements

This tool leverages the MLX-LM framework and associated dependencies. Ensure you have the following installed:

- **Python 3.7+**
- **MLX-LM Dependencies:**
  - `mlx-core`
  - `mlx-nn`
  - `mlx-lm`

All required packages are listed in the requirements.txt file.

## Installation

1. **Clone the Repository:**

   ```
   git clone https://github.com/gauri-nagavkar/mlxlm_bench.git
   cd mlxlm-benchmark
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
- A single value for Input Sequence Length (ISL) (`128`) is tested.
- Three different values for Output Sequence Length (OSL) (`128`, `256`, and `512`) are tested.

## Command-Line Options
- **`-m, --model`**
Specify the path to an MLX-LM model. Can be used multiple times for benchmarking several models.
Example: `-m models/7B/model1 -m models/13B/model2`

- **`-p, --n-prompt`**
Input Sequence Length (ISL). Specify one or more values (or comma-separated lists) for synthetic prompt tokens. Default: `128`
Example: `-p 0,128`

- **`-n, --n-gen`**
Output Sequence Length (OSL). Specify one or more values (or comma-separated lists) for generation tokens. Default: `512`
Example: `-n 128,256,512`

- **`-o, --output`**
Output format for the benchmark results. Supported formats: csv, json, jsonl, md. Default: `csv`
Example: `- o json`

- **`-r, --repetitions`**
Number of iterations per configuration to average out performance results. Default: `5`
Example: `-r 10`

## Contributing
Contributions to enhance the MLX-LM Benchmark Tool are welcome.

## Contact
For questions, support, or feedback, please open an issue in the repository or contact the maintainer at gauri.nagavkar@gmail.com.
