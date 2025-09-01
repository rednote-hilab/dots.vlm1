<div align="center">
<p align="center">
    <img src="/assets/logo.png" width="300"/>
<p>



[![Blog](https://img.shields.io/badge/Blog-View_on_GitHub-333.svg?logo=github)](https://github.com/rednote-hilab/dots.vlm1/blob/main/assets/blog.md)
[![HuggingFace](https://img.shields.io/badge/HuggingFace%20Weights-black.svg?logo=HuggingFace)](https://huggingface.co/rednote-hilab/dots.vlm1.inst)

<div align="center">
  <a href="https://huggingface.co/spaces/rednote-hilab/dots-vlm1-demo" target="_blank" rel="noopener noreferrer"><strong>🖥️ Live Demo</strong></a> | 
  <a href="/assets/wechat.png" target="_blank" rel="noopener noreferrer"><strong>💬 WeChat</strong></a> | 
  <a href="https://www.xiaohongshu.com/user/profile/683ffe42000000001d021a4c" target="_blank" rel="noopener noreferrer"><strong>📕 rednote</strong></a>
</div>
</div>

## 1. Introduction

We are excited to introduce **dots.vlm1**, the first vision-language model in the dots model family. Built upon a 1.2 billion-parameter vision encoder and the DeepSeek V3 large language model (LLM), **dots.vlm1** demonstrates strong multimodal understanding and reasoning capabilities.  

**Model Highlights**:
- **NaViT Vision Encoder**: Trained entirely from scratch rather than fine-tuning an existing vision backbone. It natively supports dynamic resolution and incorporates pure visual supervision in addition to traditional text supervision, thereby enhancing the upper bound of perceptual capacity. Beyond image captioning datasets, a large amount of structured image data was introduced during pretraining to improve the model’s perceptual capabilities—particularly for tasks such as OCR.  
- **Multimodal Training Data**: In addition to conventional approaches, dots.vlm1 leverages a wide range of synthetic data strategies to cover diverse image types (e.g., tables, charts, documents, graphics) and descriptions (e.g., alt text, dense captions, grounding annotations). Furthermore, a strong multimodal model was used to rewrite web page data with interleaved text and images, significantly improving the quality of the training corpus.


Through large-scale pretraining and carefully tuned post-training, **dots.vlm1 achieves near state-of-the-art performance in both visual perception and reasoning**, setting a new performance ceiling for open-source vision-language models—while still maintaining competitive capabilities in pure-text tasks.

*Special thanks to the DeepSeek team for the excellent DeepSeek V3 model.*

## 2. Performance

### 2.1 Benchmark Results
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

> Due to the inability to reliably reproduce reported results, we re-evaluated all models using our evaluation pipeline. Our evaluation configuration is as follows:  
> For multiple-choice datasets (including MMMU, MMMU_Pro, and related benchmarks), we adopted the default inference and evaluation protocols established by VLMEvalKit. To minimize errors during the response-to-option mapping stage, we inhibit rule-based extraction in favor of a model-based solution (see the corresponding [pull request](https://github.com/open-compass/VLMEvalKit/pull/1175) for details). For the MMVP dataset, we report pair-accuracy metrics following the SeedVL evaluation framework.  
> For structured reasoning and document understanding tasks—specifically OCRReasoning, DOCVQA, ChartQA, MUIR, and Mantis—we utilized xVerify-9B-C as the discriminative scoring model. Our ChartQA evaluation was conducted on the "human_test" subset to ensure consistency with established benchmarks. For subjective evaluation on the Vibe-Eval dataset, we employed GPT-4o as the adjudicator model to assess response quality and appropriateness.  
> All evaluations of dots.vlm1 were conducted with a sequence length of 64k.  

On major visual benchmarks, dots.vlm1 has achieved overall performance comparable to leading models such as **Gemini 2.5 Pro** and **Seed-VL1.5 thinking**. In particular, it demonstrates strong visual-text understanding and reasoning capabilities on datasets like **MMMU**, **MathVision**, and **OCR Reasoning**, where it delivers competitive results.  

For typical text-based reasoning tasks (e.g., **AIME**, **GPQA**, **LiveCodeBench**), **dots.vlm1** performs roughly on par with **DeepSeek-R1-0528**, showing a certain degree of general capability in mathematics and coding. However, there is still a noticeable performance gap on more diverse reasoning challenges such as **GPQA**. 

Overall, **dots.vlm1** approaches state-of-the-art levels in multimodal visual understanding and achieves mainstream performance in text reasoning. That said, there remains a measurable gap on some specialized tasks, which calls for further optimization in both architecture design and training data. These subsets will also be key areas of focus in our next phase of improvements.  

### 2.2 Demo Highlights

<details>
<summary> Examples for Complex Doc/Chart Reasoning </summary>
<img src="/assets/cases/1040025031km07evmi00ddb8r1c.png" width="300"/>   


**Prompt**: What is the average amount of goods where the second letter in the name is 'e'?

**Response**: `<think>`…`</think>`   
To determine the average amount of goods where the second letter in the name is 'e', first identify the goods from the list and check the second letter of their names.

The goods and their export values are:

- Petroleum products: $69.6B
- Pearls, precious & semiprecious stones: $39.3B
- Machinery and appliances: $25.4B
- Iron and steel: $22.9B
- Organic chemicals: $22.1B

Now, check the second letter of the first word in each name (as is standard for such queries):

- Petroleum products: First word "Petroleum" – second letter is 'e' (P-e-t-r-o-l-e-u-m). Qualifies.
- Pearls, precious & semiprecious stones: First word "Pearls" – second letter is 'e' (P-e-a-r-l-s). Qualifies.
- Machinery and appliances: First word "Machinery" – second letter is 'a' (M-a-c-h-i-n-e-r-y). Does not qualify.
- Iron and steel: First word "Iron" – second letter is 'r' (I-r-o-n). Does not qualify.
- Organic chemicals: First word "Organic" – second letter is 'r' (O-r-g-a-n-i-c). Does not qualify.

Only two goods qualify: Petroleum products (69.6B) and Pearls, precious & semiprecious stones (39.3B).

Calculate the average:

- Sum of values: 69.6B + 39.3B = $108.9B
- Number of goods: 2
- Average: 108.9B / 2 = 54.45B

The average amount is $54.45 billion.  
\boxed{54.45}

**Answer**: 54.45

<img src="/assets/cases/1040025031km08ed5200979plfk.png" width="300"/>   

**Prompt**: 如果一个12人的团队，其中有6个身高1.3米的儿童，2个身高1.8米的成人，4个本科在读大学生，他们参观黄姚古镇，总共需要花费多少钱？

**Response**: `<think>`…`</think>`   
根据黄姚古镇景区价目表，计算12人团队的门票费用：

6个身高1.3米的儿童：身高在1.2米（不含）至1.4米（含）之间，适用半票，价格为50元/人。费用：6 × 50 = 300元。

2个身高1.8米的成人：身高超过1.4米，适用全票，价格为100元/人。费用：2 × 100 = 200元。

4个本科在读大学生：凭证学生（含本科及以下在读）适用半票，价格为50元/人。费用：4 × 50 = 200元。

门票总费用：300 + 200 + 200 = 700元。

团队为12人，属于10人以上团队，但价目表中团体票价格未明确指定，且无旅行社行程单或结算单信息，因此按 individual 票价计算。观光车票价格为0元（免费），景区讲解费为80元/每团/次，但问题未提及需要讲解服务，故不包括。

总花费为门票费用700元。

\boxed{700}

**Answer**: 700

<img src="/assets/cases/1040025031km09b4fi005gg197s.png" width="300"/>   

**Prompt**: What is the difference in protein content between the black-packaged product and the blue-packaged product if you eat 100 calories?  

**Response**: `<think>`…`</think>`   
To determine the difference in protein content between the black-packaged product and the blue-packaged product when consuming 100 calories, first calculate the protein content per 100 calories for each product.  

For the blue-packaged product (left nutrition label):  

- Calories per serving: 130
- Protein per serving: 2 g Protein per 100 calories = \frac{2}{130} \times 100 = \frac{200}{130} = \frac{20}{13} \approx 1.538 g

For the black-packaged product (right nutrition label):

- Calories per serving: 150
- Protein per serving: 3 g Protein per 100 calories = \frac{3}{150} \times 100 = \frac{300}{150} = 2 g

The difference in protein content per 100 calories is calculated as the absolute difference between the black-packaged and blue-packaged products:  

|2 - \frac{20}{13}| = |\frac{26}{13} - \frac{20}{13}| = |\frac{6}{13}| = \frac{6}{13} g  

Thus, the difference is \frac{6}{13} grams per 100 calories.  

\boxed{\dfrac{6}{13}}  

**Answer**: 0.46g

<img src="/assets/cases/1040025031km0k8hh2006updpps.png" width="300"/>   

**Prompt**: How many our bid/ask actions categories will result in exactly 9 competitor's bid/ask actions' categories to have a value above 21? * Your final answer must be an exact integer.

**Response**: `<think>`…`</think>`   
To determine how many of our bid/ask actions categories result in exactly 9 competitor's bid/ask actions' categories having a value above 21, each column (corresponding to our bid/ask actions) is examined. The values in each column are checked to count how many are greater than 21.

Column 1 (our action 1): Values above 21 are in rows 1, 2, 3, 5, 6, 7, 9, 10, 11. Count = 9.

Column 2 (our action 2): Values above 21 are in rows 1, 2, 3, 5, 6, 7, 9, 10, 11. Count = 9.

Column 3 (our action 3): All values are below 21. Count = 0.

Column 4 (our action 4): All values are below 21. Count = 0.

Column 5 (our action 5): Values above 21 are in rows 1, 2, 3, 5, 6, 7, 9, 10, 11. Count = 9.

Column 6 (our action 6): Values above 21 are in rows 1, 2, 3, 5, 6, 7, 9, 10, 11. Count = 9.

Column 7 (our action 7): All values are below 21. Count = 0.

Column 8 (our action 8): All values are below 21. Count = 0.

Column 9 (our action 9): All values are below 21. Count = 0.

Column 10 (our action 10): All values are below 21. Count = 0.

Column 11 (our action 11): All values are below 21. Count = 0.

Column 12 (our action 12): All values are below 21. Count = 0.

Column 13 (our action 13): All values are below 21. Count = 0.

Column 14 (our action 14): All values are below 21. Count = 0.

Column 15 (our action 15): All values are below 21. Count = 0.

Column 16 (our action 16): All values are below 21. Count = 0.

The columns with exactly 9 values above 21 are columns 1, 2, 5, and 6, corresponding to our bid/ask actions 1, 2, 5, and 6. Thus, there are 4 such categories.

**Answer**: 4



    
</details>


<details>
<summary> Examples for STEM Problem </summary>

<img src="/assets/cases/1040025031km175a3i0030p4k24.png" width="300"/>   

**Prompt**: Hint: Please answer the question and provide the final answer at the end. Question: Triangle ABC has a right angle at C, AC=3 and BC=4. Triangle ABD has a right angle at A and AD=12. Points C and D are on opposite sides of AB. The line through D parallel to AC meets CB extended at E. If DE/DB=m/n, where m and n are relatively prime positive integers, then m+n=

**Response**: `<think>`…`</think>`   
In triangle ABC with a right angle at C, AC = 3 and BC = 4. Using the Pythagorean theorem, AB = \sqrt{AC^2 + BC^2} = \sqrt{3^2 + 4^2} = \sqrt{25} = 5.  

Triangle ABD has a right angle at A and AD = 12. Since \angle DAB = 90^\circ, BD = \sqrt{AB^2 + AD^2} = \sqrt{5^2 + 12^2} = \sqrt{169} = 13.  

Place C at (0,0), A at (0,3), and B at (4,0). The line AB has the equation y = -\frac{3}{4}x + 3. Point C(0,0) is below this line. Since C and D are on opposite sides of AB, D must be above AB.  

The vector \overrightarrow{AB} = (4, -3). A vector perpendicular to \overrightarrow{AB} is (3, 4), with length \sqrt{3^2 + 4^2} = 5. Since AD = 12, the vector \overrightarrow{AD} = 12 \cdot \frac{(3, 4)}{5} = \left(\frac{36}{5}, \frac{48}{5}\right). Thus, D is at \left(0 + \frac{36}{5}, 3 + \frac{48}{5}\right) = \left(\frac{36}{5}, \frac{63}{5}\right).  

The line AC is vertical (from (0,3) to (0,0)). The line through D parallel to AC is vertical, so it has the equation x = \frac{36}{5}. This line intersects the extension of CB (which is the x-axis, y = 0) at E\left(\frac{36}{5}, 0\right).  

The distance DE is the vertical distance between D\left(\frac{36}{5}, \frac{63}{5}\right) and E\left(\frac{36}{5}, 0\right), so DE = \left|\frac{63}{5} - 0\right| = \frac{63}{5}. The distance DB is between D\left(\frac{36}{5}, \frac{63}{5}\right) and B(4, 0) = \left(\frac{20}{5}, 0\right):  

DB = \sqrt{\left(\frac{36}{5} - \frac{20}{5}\right)^2 + \left(\frac{63}{5} - 0\right)^2} = \sqrt{\left(\frac{16}{5}\right)^2 + \left(\frac{63}{5}\right)^2} = \sqrt{\frac{256}{25} + \frac{3969}{25}} = \sqrt{\frac{4225}{25}} = \frac{65}{5} = 13.  

The ratio \frac{DE}{DB} = \frac{\frac{63}{5}}{13} = \frac{63}{65}. The fraction \frac{63}{65} is in simplest terms since \gcd(63, 65) = 1. Thus, m = 63, n = 65, and m + n = 128.  

\boxed{128}

**Answer**: 128

<img src="/assets/cases/1040025031km1bh7ii00f4vhe68.png" width="300"/>   

**Prompt**: Hint: Please answer the question and provide the correct option letter, e.g., A, B, C, D, at the end. Question: If ABCD is a 2 X 2 square, E is the midpoint of AB, F is the midpoint of BC, AF and DE intersect at I, and BD and AF intersect at H, then the area of quadrilateral BEIH is Choices: (A) 1/3 (B) 2/5 (C) 7/15 (D) 8/15 (E) 3/5

**Response**: `<think>`…`</think>`   
The area of quadrilateral BEIH in the 2x2 square ABCD is calculated using coordinate geometry. Assign coordinates to the square: A(0,2), B(0,0), C(2,0), D(2,2). E is the midpoint of AB, so E(0,1). F is the midpoint of BC, so F(1,0).

The line AF passes through A(0,2) and F(1,0), with equation y = -2x + 2. The line DE passes through D(2,2) and E(0,1), with equation y = (1/2)x + 1. The intersection of AF and DE is I, found by solving -2x + 2 = (1/2)x + 1, giving x = 2/5 and y = 6/5, so I(2/5, 6/5).

The diagonal BD passes through B(0,0) and D(2,2), with equation y = x. The intersection of BD and AF is H, found by solving x = -2x + 2, giving x = 2/3 and y = 2/3, so H(2/3, 2/3).

The vertices of quadrilateral BEIH are B(0,0), E(0,1), I(2/5, 6/5), and H(2/3, 2/3). Using the shoelace formula with the order B-E-I-H-B:

Sum = (0·1 - 0·0) + (0·6/5 - 2/5·1) + (2/5·2/3 - 2/3·6/5) + (2/3·0 - 0·2/3) = 0 + (-2/5) + (-8/15) + 0 = -14/15

Absolute value = 14/15

Area = (1/2) · 14/15 = 7/15

Alternatively, split BEIH into triangles BEI and BIH:

Area of ΔBEI: Base BE = 1 (vertical), height = x-coordinate of I = 2/5, area = (1/2)·1·(2/5) = 1/5

Area of ΔBIH: Shoelace formula gives sum = -8/15, absolute value 8/15, area = (1/2)·8/15 = 4/15

Total area = 1/5 + 4/15 = 3/15 + 4/15 = 7/15

Both methods confirm the area is 7/15, which corresponds to option (C).

\boxed{\text{C}}

**Answer**: C

<img src="/assets/cases/1040025031km1dqmm2005ou9re0.png" width="300"/>   

**Prompt**: Solve this problem

**Response**: `<think>`…`</think>`   
The acceleration vs. time graph for both cars starts at (0,0) and ends at (T,0), with both reaching a maximum acceleration of 10 m/s². The area under the acceleration-time graph represents the change in velocity. Since both cars start from rest, the velocity at time T is given by the area under their respective acceleration curves from 0 to T.

Both acceleration curves are triangular, with a base of T and a height of 10 m/s². The area of a triangle is \frac{1}{2} \times \text{base} \times \text{height}, so the area for each car is \frac{1}{2} \times T \times 10 = 5T m/s. Thus, the change in velocity is the same for both cars, and since they start from rest, v_P = v_Q at time T.

The position at time T is given by the integral of velocity from 0 to T, which is equivalent to the double integral of acceleration. Specifically, x(T) = \int_0^T a(s) (T - s) ds, where (T - s) is a weighting factor that decreases linearly from T to 0 as s increases from 0 to T. This weighting factor emphasizes acceleration at earlier times more than at later times.

Car P has a higher acceleration than car Q for early times (s < s_{\text{cross}}), while car Q has a higher acceleration for later times (s > s_{\text{cross}}). Since the weighting factor (T - s) is larger for smaller s, the region where a_P(s) > a_Q(s) is weighted more heavily. Therefore, the integral for x_P(T) is greater than for x_Q(T), so x_P > x_Q at time T.

Thus, the speeds are equal (v_P = v_Q) and the position of car P is greater than that of car Q (x_P > x_Q), which corresponds to option (A).

\boxed{\text{A}}

**Answer**: A

<img src="/assets/cases/1040025031km3c2iri00b99tbfg.png" width="300"/>   

**Prompt**: The square is filled in with a pattern of triangles that become smaller and smaller until they are infinitely small. what fraction of the square is shaded blue?

**Response**: `<think>`…`</think>`   
The square has an area of 1. The pattern consists of a sequence of blue right triangles, each similar to the previous one but scaled down by a factor of \frac{1}{2} in linear dimensions, and only one triangle is added at each level.

The largest blue triangle (level 0) has legs of length 1, so its area is \frac{1 \times 1}{2} = \frac{1}{2} .

The next blue triangle (level 1) has legs of length \frac{1}{2} , so its area is \frac{\frac{1}{2} \times \frac{1}{2}}{2} = \frac{1}{8} .

The subsequent blue triangle (level 2) has legs of length \frac{1}{4} , so its area is \frac{\frac{1}{4} \times \frac{1}{4}}{2} = \frac{1}{32} .

This pattern continues indefinitely, with the area of each triangle scaled by a factor of \frac{1}{4} relative to the previous triangle (since area scales with the square of the linear scale factor).

The areas of the blue triangles form a geometric series:

\frac{1}{2} + \frac{1}{8} + \frac{1}{32} + \frac{1}{128} + \cdots

The first term a is \frac{1}{2} , and the common ratio r is \frac{1}{4} . The sum of an infinite geometric series is given by \frac{a}{1 - r} :

\text{Total blue area} = \frac{\frac{1}{2}}{1 - \frac{1}{4}} = \frac{\frac{1}{2}}{\frac{3}{4}} = \frac{1}{2} \times \frac{4}{3} = \frac{4}{6} = \frac{2}{3}.

Thus, the fraction of the square shaded blue is \frac{2}{3} .

\boxed{\dfrac{2}{3}}

**Answer**: 2/3

<img src="/assets/cases/1040025031km3cg062003b8stno.png" width="300"/>   

**Prompt**: the area of the blue triangle is 12 which is a right triangle and the area of the gray triangle is 9 which is a right triangle. what is the area of the orange rectangle?

**Response**: `<think>`…`</think>`   
The blue triangle has a base of 3 and an area of 12. The area of a triangle is given by \frac{1}{2} \times \text{base} \times \text{height}. Solving for the height:

\frac{1}{2} \times 3 \times h_b = 12 \implies \frac{3h_b}{2} = 12 \implies 3h_b = 24 \implies h_b = 8.

Thus, the height from the apex to the base of the blue triangle is 8, which is also the height of the large triangle.

The gray triangle is above the orange rectangle, and the rectangle has a height of 2. The base of the gray triangle is the top side of the rectangle, which is parallel to the base of the large triangle. The vertical distance from the base of the large triangle to the base of the gray triangle is 2, so the distance from the apex to the base of the gray triangle is 8 - 2 = 6.

The area of the gray triangle is 9. Using the area formula for a triangle:

\frac{1}{2} \times w \times 6 = 9 \implies 3w = 9 \implies w = 3,

where w is the width of the rectangle (and the base of the gray triangle).

The orange rectangle has a width of w = 3 and a height of 2, so its area is:

3 \times 2 = 6.

Thus, the area of the orange rectangle is 6.

\boxed{6}

**Answer**:  6

    
</details>

<details>
<summary> Examples for Long Tail Recognition </summary>

<img src="/assets/cases/1040025031km1sneri00ce3n0bg.png" width="300"/>   

**Prompt**: What is the name of the location in this photo?

**Response**: `<think>`…`</think>`   

Butlers Wharf

**Answer**: Butler's Wharf

<img src="/assets/cases/1040025031km226usi003565j3k.png" width="300"/>   

**Prompt**: What is the title of this artwork?

**Response**: `<think>`…`</think>`   

\boxed{Christ Walking on Water}

**Answer**: christ walking on the water

<img src="/assets/cases/1040025031km1uuj3i00apbgr10.png" width="300"/>   

**Prompt**: What is the title of this artwork?

**Response**: `<think>`…`</think>`   
To determine the title of the artwork, we analyze key elements:

Artist and Context: This fresco is by Giotto di Bondone, part of his cycle in the Scrovegni Chapel (Padua, Italy), which depicts scenes from the lives of the Virgin Mary and Christ.

Subject Matter: The scene shows a group of figures in a ceremonial setting, with architectural details and halos (indicating holy figures). This matches the Marriage of the Virgin—a traditional episode where Mary is wed to Joseph.

The title of the artwork is The Marriage of the Virgin.

**Answer**: Marriage of the Virgin

<img src="/assets/cases/1040025031km1psp6i003mbo95c.png" width="300"/>   

**Prompt**: 图中文物的名称是什么？
A: 金腰带饰
B: 凤首人身形玉佩
C: 四联璜玉组佩
D: 跽坐人形玉佩

**Response**: `<think>`…`</think>`   
\boxed{B}

**Answer**: B

<img src="/assets/cases/1040025031km1rmsr2007ajpqu0.png" width="300"/>   

**Prompt**: 图中文物的名称是什么？
A: 亚长方斝
B: 王子午鼎
C: 亚址鼎
D: 齐侯盂

**Response**: `<think>`…`</think>`   
\boxed{D}

**Answer**: D
    
</details>

<details>
<summary> Examples for Visual Reasoning </summary>

<img src="/assets/cases/1040025031kolrtqji000efpsjg.png" width="300"/>   

**Prompt**: can you solve this Rebus puzzle?

**Response**: `<think>`…`</think>`   
The Rebus puzzle features the word "LOAD" written vertically, with each letter stacked from top to bottom (L, O, A, D). This vertical arrangement suggests the direction "down," as reading from top to bottom implies a downward motion. Combined with "load," this forms the common term "download," which refers to the process of transferring data from a remote system (like the internet) to a local device.

\boxed{download}

**Answer**:  download

<img src="/assets/cases/1040025031kolsok7i000i9pnps.png" width="300"/>   

**Prompt**: Which novel do these emojis remind you of?

**Response**: `<think>`…`</think>`   
The emojis 🎶🐦&🐍 most likely represent the novel "The Ballad of Songbirds and Snakes" by Suzanne Collins, which is a prequel to "The Hunger Games" series. Here's why:

- 🎶 Musical notes: Represents the "ballad" in the title, as a ballad is a type of song or poem that tells a story, often with musical elements. The novel features themes of music and performance, including the "Hanging Tree" song, which is central to the story.

- 🐦 Blue bird: Symbolizes the "songbirds" in the title. Songbirds are often depicted as blue or colorful in illustrations and are a key motif in the book, representing innocence, hope, and the characters' connections to nature.

- & Ampersand: Directly corresponds to the "and" in the title, linking "songbirds" and "snakes" as dual symbols of the story's conflict.

- 🐍 Green snake: Represents the "snakes" in the title, which symbolize danger, corruption, and the darker aspects of the story, particularly through the character of Coriolanus Snow and the serpentine themes.

This novel explores the origins of the Hunger Games and the moral complexities of its characters, making the emojis a fitting visual shorthand for the title and its themes. If you're thinking of something else, it could be a reference to another work, but this is the most direct match based on common interpretations! 📚

**Answer**: The Ballad of Songbirds and Snakes

<img src="/assets/cases/1040025031km25jkdi006vrceig.png" width="300"/>   

**Prompt**: These seemingly random phrases hide the names of eight capital cities around the world. Each phrase contains the name of two cities. Can you unscramble them and figure out what they are?

**Response**: `<think>`…`</think>`   
The phrases are anagrams that hide pairs of capital cities. By rearranging the letters in each phrase, the following capital cities are revealed:

LION JOB ENDING unscrambles to Beijing (capital of China) and London (capital of the United Kingdom).

Letters: L, I, O, N, J, O, B, E, N, D, I, N, G → Beijing (B, E, I, J, I, N, G) and London (L, O, N, D, O, N).

TOOK MY ORE unscrambles to Tokyo (capital of Japan) and Rome (capital of Italy).

Letters: T, O, O, K, M, Y, O, R, E → Tokyo (T, O, K, Y, O) and Rome (R, O, M, E).

CRIMSON ELBOW unscrambles to Moscow (capital of Russia) and Berlin (capital of Germany).

Letters: C, R, I, M, S, O, N, E, L, B, O, W → Moscow (M, O, S, C, O, W) and Berlin (B, E, R, L, I, N).

RAPID DISARM unscrambles to Paris (capital of France) and Madrid (capital of Spain).

Letters: R, A, P, I, D, D, I, S, A, R, M → Paris (P, A, R, I, S) and Madrid (M, A, D, R, I, D).

The eight capital cities are: Beijing, London, Tokyo, Rome, Moscow, Berlin, Paris, and Madrid.

\boxed{\text{Beijing, London, Tokyo, Rome, Moscow, Berlin, Paris, Madrid}}

**Answer**: London, Beijing, Tokyo, Rome, Berlin, Moscow, Paris, Madrid


<img src="/assets/cases/1040025031km265kr2003hs0ap4.png" width="300"/>   

**Prompt**: Alice and Betty are playing “guess my word”. Betty thinks of a five-letter word (all distinct letters), and Alice guesses. For each guess, Betty tells Alice how many letter from her guess are right. What is Betty’s word?

**Response**: `<think>`…`</think>`   
Betty's word is a five-letter word with all distinct letters. The guesses and the number of correct letters are as follows:

- HUNKY: 2 correct letters
- JUNKS: 0 correct letters
- WHISK: 2 correct letters
- CENTS: 2 correct letters
- STINK: 0 correct letters

From JUNKS having 0 correct letters, the letters J, U, N, K, and S are not in Betty's word.

From HUNKY having 2 correct letters and U, N, K excluded by JUNKS, the correct letters must be H and Y. Thus, H and Y are in Betty's word.

From STINK having 0 correct letters and S, N, K excluded by JUNKS, the letters T and I are not in Betty's word.

From WHISK having 2 correct letters, and S, K excluded by JUNKS and I excluded by STINK, the only possible correct letters are W and H. Since H is already in the word, W must also be in the word.

From CENTS having 2 correct letters, and N, S excluded by JUNKS and T excluded by STINK, the only possible correct letters are C and E. Thus, both C and E are in the word.

The letters in Betty's word are C, E, H, W, and Y. These form the word CHEWY, which has all distinct letters and satisfies all the guesses:

- HUNKY: H and Y are correct (2 letters).
- JUNKS: No letters match (0 letters).
- WHISK: W and H are correct (2 letters).
- CENTS: C and E are correct (2 letters).
- STINK: No letters match (0 letters).

Thus, Betty's word is CHEWY.

\boxed{CHEWY}

**Answer**: CHEWY

    
</details>

## 3. Methods
### 3.1 Architecture Overview
**dots.vlm1** integrates a 1.2B NaViT vision encoder, a lightweight MLP adapter and a DeepSeek V3 MoE language model. These components are trained through a three-stage process.  

- **Stage 1: Vision Encoder Pretraining** — The NaViT vision encoder is trained entirely from scratch to maximize perceptual capability across diverse visual data.
- **Stage 2: VLM Pretraining** — The vision encoder and DeepSeek V3 LLM are jointly pretrained on large-scale, diverse multimodal datasets.
- **Stage 3: VLM Post-training** — A final phase of supervised fine-tuning (SFT) is performed using task-varied data to enhance generalization.  

*Training note: Post-training only includes supervised fine-tuning (SFT); reinforcement learning methods are planned for future work.*  

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
- **PDF data**: We observed that PDF data is often of high quality. To fully leverage this, we developed a dedicated parsing model, [dots.ocr](https://huggingface.co/rednote-hilab/dots.ocr), which converts PDF documents into interleaved image-text representations. Additionally, we render full PDF pages as images and selectively mask text blocks, prompting the model to reconstruct the masked content using layout and contextual cues—enhancing its ability to read and understand visually formatted documents.  


## 4. Future Work
Despite the progress achieved with dots.vlm1, our evaluation reveals notable limitations in both visual perception and reasoning capabilities.  

For visual perception, we plan to significantly expand the scale and diversity of cross-modal translation data. In parallel, we will continue to improve the vision encoder by exploring innovations in neural network architectures and loss function design to significantly improve training efficiency.  

For visual reasoning, we prioritize advancing reinforcement learning approaches to reduce the test-time scaling gap between text-only and multimodal prompts. Furthermore, we are investigating the feasibility of shifting more reasoning ability into the pretraining stage to improve generalization and efficiency.  

> Hiring!!!  
> We believe that collaboration is the key to tackling these exciting challenges. If you are passionate about advancing the frontiers of multimodal intelligence, we would love to hear from you.  
> Please reach out to us via email at: martin [at] xiaohongshu [dot] com

## 5. Author List
### Core Contributor
ADu, Baiheng, Chaohui Yu, Guang Yang, Guangwei Zhao, Guofu, Guohai Xu, Hao Liu, Jack Hong, Jiayu Chen, Jie Lou, Laite, Liang Xin, Qianwu, Rui Yang, Shengdong Chen, Weijian Luo, Wenliang, Wenze, Xiaozhi, Xing Wu, Yimeng Ye, Yiwei Ma, Yumeng Li, Yunkai, Yuqiu Ji, Zhenhang Huang

### Contributor
rednote hi lab all

### Project Lead
Colin Zhang

### Advisor
Debing Zhang, Lei Zhang


[1] Enrico Fini and Mustafa Shukor and Xiujun Li and Philipp Dufter and Michal Klein and David Haldimann and Sai Aitharaju and Victor Guilherme Turrisi da Costa and Louis Béthune and Zhe Gan and Alexander T Toshev and Marcin Eichner and Moin Nabi and Yinfei Yang and Joshua M. Susskind and Alaaeldin El-Nouby. Multimodal Autoregressive Pre-training of Large Vision Encoders. CVPR 2025. 
