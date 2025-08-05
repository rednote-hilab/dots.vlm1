# dots.vlm1
The official repository of the dots.vlm1 instruct models proposed by rednote-hilab.

## Usage

### Environment Setup

You have two options to set up the environment:

#### Option 1: Using Base Image + Manual Installation
```bash
# Use the base SGLang image
docker run -it --gpus all lmsysorg/sglang:v0.4.9.post1-cu126

# Clone and install our custom SGLang branch
git clone https://github.com/rednote-hilab/sglang -b dots.vlm1 sglang
pip install -e sglang/python
```

#### Option 2: Using Pre-built Image (Recommended)
```bash
# Use our pre-built image with dots.vlm1 support
docker run -it --gpus all rednotehilab/dots1_sglang:v0.4.9.post1-cu126
```

### Multi-Node Deployment

Our model supports distributed deployment across multiple machines. Here's how to set up a 2-node cluster:

**Prerequisites:**
- Model: `rednote-hilab/dots.vlm1.inst`
- Node 1 IP: `10.0.0.1` (master node)
- Node 2 IP: `10.0.0.2` (worker node)

#### Node 1 (Master - rank 0):
```bash
export HF_MODEL_PATH="rednote-hilab/dots.vlm1.inst"

python3 -m sglang.launch_server \
    --model-path $HF_MODEL_PATH \
    --tp 16 \
    --dist-init-addr 10.0.0.1:23456 \
    --nnodes 2 \
    --node-rank 0 \
    --trust-remote-code \
    --host 0.0.0.0 \
    --port 15553 \
    --context-length 65536 \
    --max-running-requests 64 \
    --disable-radix-cache \
    --mem-fraction-static 0.8 \
    --chunked-prefill-size -1 \
    --chat-template dots-vlm \
    --cuda-graph-max-bs 64 \
    --quantization fp8
```

#### Node 2 (Worker - rank 1):
```bash
export HF_MODEL_PATH="rednote-hilab/dots.vlm1.inst"

python3 -m sglang.launch_server \
    --model-path $HF_MODEL_PATH \
    --tp 16 \
    --dist-init-addr 10.0.0.1:23456 \
    --nnodes 2 \
    --node-rank 1 \
    --trust-remote-code \
    --host 0.0.0.0 \
    --port 15553 \
    --context-length 65536 \
    --max-running-requests 64 \
    --disable-radix-cache \
    --mem-fraction-static 0.8 \
    --chunked-prefill-size -1 \
    --chat-template dots-vlm \
    --cuda-graph-max-bs 64 \
    --quantization fp8
```

### API Usage

Once the servers are launched, you can access the model through OpenAI-compatible API:

```bash
curl -X POST http://10.0.0.1:15553/v1/chat/completions \
    -H "Content-Type: application/json" \
    -d '{
        "model": "model", 
        "messages": [
            {
                "role": "user", 
                "content": [
                    {
                        "type": "text", 
                        "text": "Hello, how are you?"
                    }
                ]
            }
        ], 
        "temperature": 0.1, 
        "max_tokens": 32768
    }'
```

### Benchmarking

For benchmarking examples and advanced usage, please refer to: https://github.com/sgl-project/sglang/tree/main/benchmark/deepseek_v3

### Configuration Parameters

Key parameters explanation:
- `--tp 16`: Tensor parallelism across 16 GPUs per node
- `--nnodes 2`: Total number of nodes in the cluster
- `--node-rank`: Node identifier (0 for master, 1+ for workers)
- `--context-length 65536`: Maximum context length
- `--quantization fp8`: Use FP8 quantization for efficiency
- `--chat-template dots-vlm`: Use custom chat template for dots.vlm model
