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
   cd mlxlm_bench
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

    python mlxlm_bench.py -m mlx-community/DeepSeek-R1-Distill-Qwen-7B-4bit -p 128 -n 256 -o csv -f benchmark_results_4bit --gen-args kv_group_size=64

In this example:
- The model 4-bit quantized version of DeepSeek-R1-Distill-Qwen-7B is benchmarked.
- A single value for Input Sequence Length (ISL) (`128`) is tested.
- A single value for Output Sequence Length (OSL) (`256`) is tested.
- The output is saved in a file called benchmark_results_4bit.csv
- Extra argument of kv_group_size is passed to the generate function as a key-value pair

We get the results:
| Model | Model Load Time (s) | Prompt Tokens | Prompt TPS | Response Tokens | Response TPS | Execution Time (s) | Memory Usage (GB) |
|---|---|---|---|---|---|---|---|
| mlx-community/DeepSeek-R1-Distill-Qwen-7B-4bit | 1.897 | 128 | 295.901 | 256 | 42.847 | 6.407 | 4.39 |


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

- **`-f, --output-filename`**
Name of the output file, without extension. Default: `benchmark_results`
Example: `-f results_7B_4b`

- **`--gen-args`**
Additional keyword arguments for generate() in key=value format
Example: `--gen-args kv_group_size=64`
  
## Contributing
Contributions to enhance the MLX-LM Benchmark Tool are welcome.

## Contact
For questions, support, or feedback, please open an issue in the repository or contact the maintainer at gauri.nagavkar@gmail.com.
