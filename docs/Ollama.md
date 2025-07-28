[Ollama](https://ollama.com/) is an open-source framework for running language models on the local machine.

## Run Ollama as a chatbot on your local machine

1. On your local machine.
    *   Make a virtual environment for [Open WebUI](https://docs.openwebui.com/): `python -m venv openwebui`. The virtual environment will be made in the current directory. You can also create a conda environment.
    *   Activate the virtual environment: `source openwebui/bin/activate`.
    *   Install Open WebUI: `pip install open-webui`.

2. On TReNDS cluster. 
    *   Start Ollama by submitting the following SLURM job script. Check the status of the job using the command `squeue -u <username>`, where `<username>` is your username. Check the node that Ollama is running on in the output of the command. The node name is under `NODELIST(REASON)` in the format `arctrdagnXXX`, where `XXX` is a number. Let's use `OLLAMA_NODE` to call the node that Ollama is running on.

```bash
#!/bin/bash
#SBATCH -p qTRDGPU
#SBATCH -A trends53c17
#SBATCH -t 00:30:00
#SBATCH -c 24
#SBATCH --mem=100g
#SBATCH --gres=gpu:A40:2

# Ensure both GPUs are visible to Ollama
export CUDA_VISIBLE_DEVICES=0,1

# Set environment variables for large context RAG optimization
export OLLAMA_HOST_MEMORY=false
export OLLAMA_KEEP_ALIVE=-1
export OLLAMA_MMAP=true
export GGML_CUDA_FORCE_CUBLAS=1
export GGML_CUDA_FORCE_MMQ=1
export OLLAMA_HOST=0.0.0.0
export OLLAMA_FLASH_ATTENTION=1
export OLLAMA_MODELS=/data/users4/splis/ollama/models/
# Force GPU backend
export OLLAMA_BACKEND=gpu

# Run ollama serve
ollama serve
```

3. On your local machine. 
    *   Run this command in the terminal: `ssh -L 8081:localhost:11434 -J <username>@arctrdagn019 <username>@<OLLAMA_NODE> -fN`.
    *   Run this command subsequently: `OLLAMA_BASE_URL="http://localhost:8081" open-webui serve`.
    *   Open your browser and `http://localhost:8080`. Also read the output from the above command in case it shows a different local address.
    *   Create a user and start chatting.

## Run Ollama models in Python on TReNDS cluster

Run the step 2 above to submit a SLURM job script and start Ollama. See the following Python example to use an Ollama model. Remember to change the variable `OLLAMA_NODE`.

```python
import json
import requests

OLLAMA_NODE = "arctrdagnXXX" # TODO: Change it to the node where Ollama is running
BASE_URL = f"http://{OLLAMA_NODE}:11434/api/chat"

model = "gemma3-optimized:27b" # TODO: Change it to the model you want to use
message = "What is the capital of France?" # TODO: Change it to the message you want to ask the model

response = requests.post(
  BASE_URL,
  json = {
    "model": model,
    "messages": [{"role": "user", "content": message}],
    "stream": False
  }
)

print(json.dumps(response.json(), indent=2))
```