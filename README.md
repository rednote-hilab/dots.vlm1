<div align="center">
<p align="center">
    <img src="https://raw.githubusercontent.com/rednote-hilab/dots.vlm1/master/assets/logo.png" width="300"/>
<p>



<h1 align="center">
dots.vlm1
</h1>

[![Blog](https://img.shields.io/badge/Blog-View_on_GitHub-333.svg?logo=github)](https://github.com/rednote-hilab/dots.vlm1/blob/main/assets/blog.md)
[![HuggingFace](https://img.shields.io/badge/HuggingFace%20Weights-black.svg?logo=HuggingFace)](https://huggingface.co/rednote-hilab/dots.vlm1)

<div align="center">
  <a href="https://huggingface.co/spaces/rednote-hilab/dots-vlm1-demo" target="_blank" rel="noopener noreferrer"><strong>🖥️ Live Demo</strong></a> | 
  <a href="https://raw.githubusercontent.com/rednote-hilab/dots.vlm1/master/assets/wechat.png" target="_blank" rel="noopener noreferrer"><strong>💬 WeChat</strong></a> | 
  <a href="https://www.xiaohongshu.com/user/profile/683ffe42000000001d021a4c" target="_blank" rel="noopener noreferrer"><strong>📕 rednote</strong></a>
</div>
</div>

## Introduction

We are excited to introduce **dots.vlm1**, the first vision-language model in the dots model family. Built upon a 1.2 billion-parameter vision encoder and the DeepSeek V3 large language model (LLM), **dots.vlm1** demonstrates strong multimodal understanding and reasoning capabilities.  

**Model Highlights**:
- **NaViT Vision Encoder**: Trained entirely from scratch rather than fine-tuning an existing vision backbone. It natively supports dynamic resolution and incorporates pure visual supervision in addition to traditional text supervision, thereby enhancing the upper bound of perceptual capacity. Beyond image captioning datasets, a large amount of structured image data was introduced during pretraining to improve the model’s perceptual capabilities—particularly for tasks such as OCR.  
- **Multimodal Training Data**: In addition to conventional approaches, dots.vlm1 leverages a wide range of synthetic data strategies to cover diverse image types (e.g., tables, charts, documents, graphics) and descriptions (e.g., alt text, dense captions, grounding annotations). Furthermore, a strong multimodal model was used to rewrite web page data with interleaved text and images, significantly improving the quality of the training corpus.


Through large-scale pretraining and carefully tuned post-training, **dots.vlm1 achieves near state-of-the-art performance in both visual perception and reasoning**, setting a new performance ceiling for open-source vision-language models—while still maintaining competitive capabilities in pure-text tasks.

*Special thanks to the DeepSeek team for the excellent DeepSeek V3 model.*

## 2. Performance

|  | | Qwen2.5VL-72B | **Gemini2.5 Pro** | **Seed-VL1.5 thinking** | dots.vlm1 |
|------|--------|----------------|--------------------|--------------------------|-----------|
| **STEM/Reasoning** | MMMU | 69.3 | **84.22** | 79.89 | <ins>80.11</ins> |
|  | MMMU_pro | 51.91 | **76.5** | 68.9 | <ins>70.11</ins> |
|  | MathVision | 39.4 | **72.34** | 68.77 | <ins>69.64</ins> |
|  | MathVista | 74.6 | 83.5 | **86.1** | <ins>85.0</ins> |
|  | ZeroBench | 2 | **5** | 2 | <ins>4</ins> |
|  | ZeroBench-sub | 20 | **30.24** | 25.75 | <ins>26.65</ins> |
|  | VisuLogic | 25.6 | 29.8 | **35.9** | <ins>32.2</ins> |
| **General Visual** | MMbench-CN | 88.2 | <ins>89</ins> | **89.78** | 88.24 |
|  | MMbench-EN | 89.2 | **89.55** | <ins>89.47</ins> | 89.32 |
|  | MMStar | 71.13 | **78.73** | <ins>78.33</ins> | 76.67 |
|  | RealWorldQA | 75.9 | 78.43 | <ins>78.69</ins> | **79.08** |
|  | Vibe(GPT4o) | 60.13 | **76.39** | 68.59 | <ins>69.24</ins> |
|  | m3gia(cn) | 88.24 | 89.54 | **91.2** | <ins>90.85</ins> |
|  | SimpleVQA_ds | 52.19 | <ins>57.09</ins> | **61.34** | 55.8 |
|  | MMVP | 66 | 67.33 | **73.33** | <ins>72</ins> |
|  | HallusionBench | 56.5 | 63.07 | 63.49 | **<ins>64.83</ins>** |
|  | CVBench | 84.15 | 85.36 | **89.68** | <ins>85.65</ins> |
|  | Blink | 61.7 | <ins>71.86</ins> | **72.38** | <ins>66.33</ins> |
| **OCR/Doc/Chart** | charxiv(dq) | 88.2 | <ins>90.3</ins> | 89.6 | **92.1** |
|  | charxiv(rq) | 48.5 | **68.3** | 63.4 | <ins>64.4</ins> |
|  | OCRReasoning | 38.02 | **70.81** | 63.42 | <ins>66.23</ins> |
|  | DOCVQA | 96.23 | <ins>95.42</ins> | 93.65 | **96.52** |
|  | ChartQA | 86.1 | 86.16 | <ins>86.88</ins> | **87.68** |
|  | OCRBenchV1 | 87.1 | <ins>86.6</ins> | **86.7** | 82.3 |
|  | AI2D | 88.3 | **91.03** | <ins>89.05</ins> | 88.37 |
| **Grounding/Counting** | RefCOCO | 90.3 | 74.6 | **91.3** | <ins>90.45</ins> |
|  | CountBench | **92.4** | 91.79 | 89 | <ins>91.99</ins> |
| **Multi Image** | muir | 69.38 | 70.5 | **79.77** | <ins>78.58</ins> |
|  | mantis | 79.26 | <ins>84.33</ins> | 82.3 | **86.18** |
| |  | **Deepseek-R1-0528** | **Qwen3-235B-A22B** | **Qwen3-235B-A22B-think-2507**|**dots.vlm1**|
| **Text** | LiveCodeBench | <ins>73.3</ins> | 70.7 | **78.4** | 72.94 |
|  | AIME 2025 | <ins>87.5</ins> | 82.6 | **92.3** | 85.83 |
|  | GPQA | <ins>81</ins> | 70.7 | **81.1** | 72.78 |

## 3. Usage

### Environment Setup

You have two options to set up the environment:

#### Option 1: Using Base Image + Manual Installation
```bash
# Use the base SGLang image
docker run -it --gpus all lmsysorg/sglang:v0.4.9.post1-cu126

# Clone and install our custom SGLang branch
# IMPORTANT: Only our specific SGLang version supports dots.vlm1 models
# We have submitted a PR to the main SGLang repository (currently under review):
# https://github.com/sgl-project/sglang/pull/8778
git git clone --branch dots.vlm1.v1 https://github.com/rednote-hilab/sglang sglang
pip install -e sglang/python
```

#### Option 2: Using Pre-built Image (Recommended)
```bash
# Use our pre-built image with dots.vlm1 support
docker run -it --gpus all rednotehilab/dots.vlm1_sglang:v0.4.9.post1-cu126
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
### Configuration Parameters

Key parameters explanation:
- `--tp 16`: Tensor parallelism across 16 GPUs per node
- `--nnodes 2`: Total number of nodes in the cluster
- `--node-rank`: Node identifier (0 for master, 1+ for workers)
- `--context-length 65536`: Maximum context length
- `--quantization fp8`: Use FP8 quantization for efficiency
- `--chat-template dots-vlm`: Use custom chat template for dots.vlm model

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
        "top_p": 0.9,
        "max_tokens": 32768
    }'
```