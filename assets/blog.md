
<p align="center">
    <img src="/assets/logo.png" width="300"/>
<p>



<h1 align="center">
dots.vlm1
</h1>


## 1. Introduction

We are excited to introduce **dots.vlm1**, the first vision-language model in the dots model family. Built upon a 1.2 billion-parameter vision encoder and the DeepSeek V3 large language model (LLM), **dots.vlm1** demonstrates strong multimodal understanding and reasoning capabilities.  

**Model Highlights**:
- **NaViT Vision Encoder**: Trained entirely from scratch rather than fine-tuning an existing vision backbone. It natively supports dynamic resolution and incorporates pure visual supervision in addition to traditional text supervision, thereby enhancing the upper bound of perceptual capacity. Beyond image captioning datasets, a large amount of structured image data was introduced during pretraining to improve the model’s perceptual capabilities—particularly for tasks such as OCR.  
- **Multimodal Training Data**: In addition to conventional approaches, dots.vlm1 leverages a wide range of synthetic data strategies to cover diverse image types (e.g., tables, charts, documents, graphics) and descriptions (e.g., alt text, dense captions, grounding annotations). Furthermore, a strong multimodal model was used to rewrite web page data with interleaved text and images, significantly improving the quality of the training corpus.  
Through large-scale pretraining and carefully tuned post-training, **dots.vlm1 achieves near state-of-the-art performance in both visual perception and reasoning**, setting a new performance ceiling for open-source vision-language models—while still maintaining competitive capabilities in pure-text tasks.

**Code**: xxxx(待补充)   
**Huggingface**: xxxx(待补充)  
**Demo**: xxxx(待补充)  

*Special thanks to the DeepSeek team for the excellent DeepSeek V3 model.*

## 2. Performance

### 2.1 Benchmark Results
|  | | Qwen2.5VL-72B | **Gemini2.5 Pro** | **Seed-VL1.5 thinking** | dots.vlm1 |
|------|--------|----------------|--------------------|--------------------------|-----------|
| **STEM/Reasoning** | MMMU | 69.3 | **84.22** | 79.89 | <ins>80.11</ins> |
|  | MMMU_pro | 51.91 | **76.5** | **68.9** | <ins>70.11</ins> |
|  | MathVision | 39.4 | **72.34** | 68.77 | <ins>69.64</ins> |
|  | MathVista | 74.6 | 83.5 | **86.1** | <ins>83.4</ins> |
|  | ZeroBench | 2 | **5** | 2 | <ins>4</ins> |
|  | ZeroBench-sub | 20 | **30.24** | 25.75 | <ins>26.65</ins> |
|  | VisuLogic | 25.6 | 29.8 | **35.9** | <ins>32.2</ins> |
| **General Visual** | MMbench-CN | 88.2 | 89 | **89.78** | <ins>88.24</ins> |
|  | MMbench-EN | 89.2 | **89.55** | **89.47** | <ins>88.47</ins> |
|  | MMStar | 71.13 | **78.73** | **78.33** | <ins>76.67</ins> |
|  | RealWorldQA | 75.9 | **78.43** | **78.69** | <ins>75.82</ins> |
|  | Vibe(GPT4o) | 60.13 | **76.39** | 68.59 | <ins>69.24</ins> |
|  | m3gia(cn) | 88.24 | 89.54 | **91.2** | <ins>90.85</ins> |
|  | SimpleVQA_ds | 52.19 | 57.09 | **61.34** | <ins>55.8</ins> |
|  | MMVP | 66 | 67.33 | **73.33** | <ins>72</ins> |
|  | HallusionBench | 56.5 | 63.07 | 63.49 | **<ins>64.83</ins>** |
|  | CVBench | 84.15 | 85.36 | **89.68** | <ins>85.25</ins> |
|  | Blink | 61.7 | **71.86** | **72.38** | <ins>66.33</ins> |
| **OCR/Doc/Chart** | charxiv(dq) | 88.2 | 90.3 | 89.6 | **<ins>92.1</ins>** |
|  | charxiv(rq) | 48.5 | **68.3** | 63.4 | <ins>64.4</ins> |
|  | OCRReasoning | 38.02 | **70.81** | 63.42 | <ins>65.01</ins> |
|  | DOCVQA | 96.23 | 95.42 | 93.65 | **<ins>96.52</ins>** |
|  | ChartQA | 86.1 | 86.16 | 86.88 | **<ins>87.68</ins>** |
|  | OCRBenchV1 | 87.1 | 86.6 | **86.7** | <ins>82.3</ins> |
|  | AI2D | 88.3 | **91.03** | 89.05 | <ins>88.37</ins> |
| **Grounding/Counting** | RefCOCO | 90.3 | 74.6 | **91.3** | <ins>90.45</ins> |
|  | CountBench | **92.4** | 91.79 | 89 | <ins>91.99</ins> |
| **Multi Image** | muir | 69.38 | 70.5 | **79.77** | <ins>78.58</ins> |
|  | mantis | 79.26 | 84.33 | 82.3 | **<ins>86.18</ins>** |
| **Text** | LiveCodeBench | **73.3** | 70.7 | **78.4** | <ins>72.94</ins> |
|  | AIME 2025 | **87.5** | 82.6 | **92.3** | <ins>85.83</ins> |
|  | GPQA | **81** | 70.7 | **81.1** | <ins>72.78</ins> |

> Due to the inability to reliably reproduce reported results, we re-evaluated all models using our evaluation pipeline. Our evaluation configuration is as follows:  
> For multiple-choice datasets (including MMMU, MMMU_Pro, and related benchmarks), we adopted the default inference and evaluation protocols established by VLMEvalKit. To minimize errors during the response-to-option mapping stage, we inhibit rule-based extraction in favor of a model-based solution (see the corresponding [pull request](https://github.com/open-compass/VLMEvalKit/pull/1175) for details). For the MMVP dataset, we report pair-accuracy metrics following the SeedVL evaluation framework.  
> For structured reasoning and document understanding tasks—specifically OCRReasoning, DOCVQA, ChartQA, MUIR, and Mantis—we utilized xVerify-9B-C as the discriminative scoring model. Our ChartQA evaluation was conducted on the "human_test" subset to ensure consistency with established benchmarks. For subjective evaluation on the Vibe-Eval dataset, we employed GPT-4o as the adjudicator model to assess response quality and appropriateness.  
> All evaluations of dots.vlm1 were conducted with a sequence length of 64k.  

On major visual benchmarks, dots.vlm1 has achieved overall performance comparable to leading models such as **Gemini 2.5 Pro** and **Seed-VL1.5 thinking**. In particular, it demonstrates strong visual-text understanding and reasoning capabilities on datasets like **MMMU**, **MathVision**, and **OCR Reasoning**, where it delivers competitive results.  

For typical text-based reasoning tasks (e.g., **AIME**, **GPQA**, **LiveCodeBench**), **dots.vlm1** performs roughly on par with **DeepSeek-R1-0528**, showing a certain degree of general capability in mathematics and coding. However, there is still a noticeable performance gap on more diverse reasoning challenges such as **GPQA**. 

Overall, **dots.vlm1** approaches state-of-the-art levels in multimodal visual understanding and achieves mainstream performance in text reasoning. That said, there remains a measurable gap on some specialized tasks, which calls for further optimization in both architecture design and training data. These subsets will also be key areas of focus in our next phase of improvements.  

### 2.2 Demo Highlights

#### Examples for Complex Doc/Chart Reasoning

#### Examples for STEM Problem


#### Examples for Long Tail Recognition

#### Examples for Visual Reasoning


## 3. Methods
### 3.1 Architecture Overview
**dots.vlm1** integrates a 1.2B NaViT vision encoder, a lightweight MLP adapter and a DeepSeek V3 MoE language model. These components are trained through a three-stage process.  

- **Stage 1: Vision Encoder Pretraining** — The NaViT vision encoder is trained entirely from scratch to maximize perceptual capability across diverse visual data.
- **Stage 2: VLM Pretraining** — The vision encoder and DeepSeek V3 LLM are jointly pretrained on large-scale, diverse multimodal datasets.
- **Stage 3: VLM Post-training** — A final phase of supervised fine-tuning (SFT) is performed using task-varied data to enhance generalization.  

*Training note: Post-training only includes supervised fine-tuning (SFT); reinforcement learning methods are planned for future work.* . 

### 3.2 NaVIT Vision Encoder
We developed a two-phase training strategy for the NaViT encoder—while the overall structure and training method are similar to AimV2[1], our model is trained entirely from scratch at native resolution. The 1.2B vision encoder comprises 42 transformer layers, incorporating techniques such as RMSNorm, SwiGLU, and 2D RoPE.
#### Phase 1: Pretrain
We start from random initialization and train on 224×224 image resolution using a dual supervision strategy: one is Next Token Prediction (NTP) using a large amount of image-text pairs to enhance the model's perceptual capability; the other is Next Patch Generation (NPG), which leverages vision-only data to predict image patches by diffusion model, further improving the vision encoder's spatial and semantic perception. The training leverages massive image-text pairs.
#### Phase 2: Resolution Scaling Pretrain
We gradually increased image resolution, starting with 1M-pixel inputs trained on massive tokens, followed by 10M-pixel inputs training. To further enhance generalization, we also incorporated more diverse visual sources, including OCR-rich images, grounding annotations, and video frames.
### 3.3 VLM Pretraining Data
To enhance dots.vlm1’s multimodal capabilities, we organize the pretraining data into two major categories:
#### Cross-Modal Translation Data
Teaches the model to describe, summarize, or reinterpret image content in text:
- General images with alt-text or dense captions
- Complex charts/tables/Formula/Graphic (real or synthesized) with structured annotations or captions.
- OCR: Multilingual / Scene Grounding / Plain text / Doc Parsing, etc.
- Video frames with temporal captions.
- Grounding supervision data, including bounding boxes and keypoints 

It is difficult to exhaustively enumerate all types of cross-modal translation data, as they involve a wide range of image and video types along with corresponding perceptual outputs. Broadly speaking, our objective is to construct a data spectrum that captures all forms of human-interpretable information that can be expressed as discrete token sequences aligned with visual content.
#### Cross-Modal Fusion Data
Cross-modal fusion data refers to interleaved visual and textual content that trains the model to perform next-token prediction in complex multimodal contexts, helping mitigate over-reliance on any single modality. We designed careful preprocessing pipelines for various types of interleaved data, with two particularly effective categories:
- **Web Data**: We found that image-text data from web pages offers rich diversity but often suffers from weak visual-textual alignment. Rather than relying on traditional CLIP-score based filtering, we used an in-house VLM to rewrite and clean the data, removing low-quality images and irrelevant or weakly grounded text content.
- **PDF data**: We observed that PDF data is often of high quality. To fully leverage this, we developed a dedicated parsing model, dots.ocr, which converts PDF documents into interleaved image-text representations. Additionally, we render full PDF pages as images and selectively mask text blocks, prompting the model to reconstruct the masked content using layout and contextual cues—enhancing its ability to read and understand visually formatted documents.  


## 4. Future Work
Despite the progress achieved with dots.vlm1, our evaluation reveals notable limitations in both visual perception and reasoning capabilities.  
For visual perception, we plan to significantly expand the scale and diversity of cross-modal translation data. In parallel, we will continue to improve the vision encoder by exploring innovations in neural network architectures and loss function design to significantly improve training efficiency.  
For visual reasoning, we prioritize advancing reinforcement learning approaches to reduce the test-time scaling gap between text-only and multimodal prompts. Furthermore, we are investigating the feasibility of shifting more reasoning ability into the pretraining stage to improve generalization and efficiency.  

> Hiring!!!  
> We believe that collaboration is the key to tackling these exciting challenges. If you are passionate about advancing the frontiers of multimodal intelligence, we would love to hear from you.  
> Please reach out to us via email at: martin [dot] xiaohongshu [dot] com

## 5. Author List
Core Contributor: 阿渡/白珩/沧行/德克/国海/简米/莱特/连轩/千悟/乔羽/时墨/时清/天南/温良/无幻/小智/燕青/一朗/云开/洪凌屹/叶意檬/马祎炜/李雨萌  
Contributor: 小红书 hilab 研发团队   
Project Lead: 柯雄   
Advisor: 宇尘/凯奇   


[1] Enrico Fini and Mustafa Shukor and Xiujun Li and Philipp Dufter and Michal Klein and David Haldimann and Sai Aitharaju and Victor Guilherme Turrisi da Costa and Louis Béthune and Zhe Gan and Alexander T Toshev and Marcin Eichner and Moin Nabi and Yinfei Yang and Joshua M. Susskind and Alaaeldin El-Nouby. Multimodal Autoregressive Pre-training of Large Vision Encoders. CVPR 2025. 
