# VLM・画像異常検知レポート内リンク整理版

## 1. 論文・arXiv

### 基礎VLM / Image-Text Matching / Cross-Modal Matching

```markdown
[2021] CLIP - Learning Transferable Visual Models From Natural Language Supervision
https://arxiv.org/abs/2103.00020

[2023] SigLIP - Sigmoid Loss for Language Image Pre-Training
https://arxiv.org/abs/2303.15343

[2021] ALBEF - Align before Fuse: Vision and Language Representation Learning with Momentum Distillation
https://arxiv.org/abs/2107.07651

[2022] BLIP - BLIP: Bootstrapping Language-Image Pre-training for Unified Vision-Language Understanding and Generation
https://arxiv.org/abs/2201.12086

[2023] BLIP-2 - BLIP-2: Bootstrapping Language-Image Pre-training with Frozen Image Encoders and Large Language Models
https://arxiv.org/abs/2301.12597

[2023] InstructBLIP - InstructBLIP: Towards General-purpose Vision-Language Models with Instruction Tuning
https://arxiv.org/abs/2305.06500
```

---

### Visual Instruction / 生成系VLM

```markdown
[2023] LLaVA - Visual Instruction Tuning
https://arxiv.org/abs/2304.08485

[2023] LLaVA-1.5 - Improved Baselines with Visual Instruction Tuning
https://arxiv.org/abs/2310.03744

[2024] Qwen2-VL - Qwen2-VL: Enhancing Vision-Language Model's Perception of the World at Any Resolution
https://arxiv.org/abs/2409.12191

[2024] InternVL2.5 - Expanding Performance Boundaries of Open-Source Multimodal Models with Model, Data, and Test-Time Scaling
https://arxiv.org/abs/2412.05271

[2024] IDEFICS2 - IDEFICS2 / multimodal model paper
https://arxiv.org/abs/2405.02246
```

---

### Grounding / Detection with Language / Segmentation with Language

```markdown
[2021] GLIP - Grounded Language-Image Pre-training
https://arxiv.org/abs/2112.03857

[2023] Grounding DINO - Grounding DINO: Marrying DINO with Grounded Pre-Training for Open-Set Object Detection
https://arxiv.org/abs/2303.05499

[2023] Florence-2 - Florence-2: Advancing a Unified Representation for a Variety of Vision Tasks
https://arxiv.org/abs/2311.06242

[2022] X-Decoder - Generalized Decoding for Pixel, Image, and Language
https://arxiv.org/abs/2212.11270

[2023] SEEM - Segment Everything Everywhere All at Once
https://arxiv.org/abs/2304.06718
```

---

### 言語情報を使った異常検知 / CLIP系AD

```markdown
[2024] AnomalyCLIP - AnomalyCLIP: Object-agnostic Prompt Learning for Zero-shot Anomaly Detection
https://arxiv.org/abs/2310.18961

[2023] CLIP-AD - CLIP-AD: A Language-Guided Staged Dual-Path Model for Zero-shot Anomaly Detection
https://arxiv.org/abs/2311.00453

[2024] MMAD - MMAD: The First-Ever Comprehensive Benchmark for Multimodal Large Language Models in Industrial Anomaly Detection
https://arxiv.org/abs/2410.09453
```

---

### 産業用異常検知ベースライン

```markdown
[2021] PatchCore - Towards Total Recall in Industrial Anomaly Detection
https://arxiv.org/abs/2106.08265

[2021] CFLOW-AD - Real-Time Unsupervised Anomaly Detection with Localization via Conditional Normalizing Flows
https://arxiv.org/abs/2107.12571

[2021] DRAEM - A Discriminatively Trained Reconstruction Embedding for Surface Anomaly Detection
https://arxiv.org/abs/2108.07610

[2021] FastFlow - FastFlow: Unsupervised Anomaly Detection and Localization via 2D Normalizing Flows
https://arxiv.org/abs/2111.07677

[2023] EfficientAD - EfficientAD: Accurate Visual Anomaly Detection at Millisecond-Level Latencies
https://arxiv.org/abs/2303.14535
```

---

### 新しめの異常検知・追跡候補

```markdown
[2025] ADNet - ADNet: A Large-Scale and Extensible Multi-Domain Benchmark for Anomaly Detection Across 380 Real-World Categories
https://arxiv.org/abs/2511.20169

[2025] Kaputt - Kaputt / large-scale visual defect detection dataset
https://arxiv.org/abs/2510.05903

[2024] IAD-GPT / anomaly-focused MLLM candidate
https://arxiv.org/abs/2409.20146

[2025] OmniAD / anomaly-focused MLLM candidate
https://arxiv.org/abs/2505.22039

[2025] MMR-AD / multimodal anomaly detection candidate
https://arxiv.org/abs/2510.16036

[2025] IMDD-1M / multimodal defect dataset candidate
https://arxiv.org/abs/2512.24160

[2026] Additional anomaly detection candidate
https://arxiv.org/abs/2604.10971
```

---

## 2. GitHub / 公式実装

```markdown
[GitHub] CLIP - openai/CLIP
https://github.com/openai/CLIP

[GitHub] SigLIP / Big Vision - google-research/big_vision
https://github.com/google-research/big_vision

[GitHub] ALBEF - salesforce/ALBEF
https://github.com/salesforce/ALBEF

[GitHub] BLIP - salesforce/BLIP
https://github.com/salesforce/BLIP

[GitHub] BLIP-2 / InstructBLIP / LAVIS - salesforce/LAVIS
https://github.com/salesforce/LAVIS

[GitHub] Qwen2-VL - QwenLM/Qwen2-VL
https://github.com/QwenLM/Qwen2-VL

[GitHub] Grounding DINO - IDEA-Research/GroundingDINO
https://github.com/IDEA-Research/GroundingDINO

[GitHub] Segment Anything - facebookresearch/segment-anything
https://github.com/facebookresearch/segment-anything

[GitHub] SAM 2 - facebookresearch/sam2
https://github.com/facebookresearch/sam2

[GitHub] AnomalyCLIP - zqhang/AnomalyCLIP
https://github.com/zqhang/AnomalyCLIP

[GitHub] WinCLIP - mala-lab/WinCLIP
https://github.com/mala-lab/WinCLIP

[GitHub] PatchCore - amazon-science/patchcore-inspection
https://github.com/amazon-science/patchcore-inspection

[GitHub] RefCOCO / Referring Expression - lichengunc/refer
https://github.com/lichengunc/refer
```

---

## 3. Hugging Faceモデルカード

```markdown
[HF] Qwen2-VL - Qwen/Qwen2-VL-7B-Instruct
https://huggingface.co/Qwen/Qwen2-VL-7B-Instruct

[HF] InternVL2.5 - OpenGVLab/InternVL2_5-8B
https://huggingface.co/OpenGVLab/InternVL2_5-8B

[HF] Florence-2 - microsoft/Florence-2-large
https://huggingface.co/microsoft/Florence-2-large

[HF] IDEFICS2 - HuggingFaceM4/idefics2-8b
https://huggingface.co/HuggingFaceM4/idefics2-8b
```

---

## 4. API / 公式ドキュメント

```markdown
[Docs] OpenAI - Images and Vision
https://platform.openai.com/docs/guides/images-vision

[Docs] OpenAI - Models
https://developers.openai.com/api/docs/models

[Docs] Gemini - Image Understanding / Vision
https://ai.google.dev/gemini-api/docs/vision

[Docs] Gemini - Models
https://ai.google.dev/gemini-api/docs/models

[Docs] Claude - Vision
https://docs.anthropic.com/en/docs/build-with-claude/vision

[Docs] Claude - Models
https://platform.claude.com/docs/en/api/models
```

---

## 5. データセット / ベンチマーク

```markdown
[Dataset] MVTec AD - The MVTec Anomaly Detection Dataset
https://www.mvtec.com/company/research/datasets/mvtec-ad

[Dataset] VisA - Visual Anomaly Dataset
https://registry.opendata.aws/visa/

[Dataset] MVTec LOCO AD - Logical Constraints Anomaly Detection Dataset
https://www.mvtec.com/research-teaching/datasets/mvtec-loco-ad

[Dataset] MVTec AD 2 - The MVTec Anomaly Detection Dataset 2
https://www.mvtec.com/company/research/datasets/mvtec-ad-2

[Dataset] Kaputt - Large-Scale Visual Defect Detection
https://www.kaputt-dataset.com

[Dataset] COCO - Common Objects in Context
https://cocodataset.org/

[Dataset] Flickr30k / Denotation Graph
https://shannon.cs.illinois.edu/DenotationGraph/

[Dataset] VQAv2 - Visual Question Answering
https://visualqa.org/
```

---

## 6. NotebookLMに優先投入するTop 20

```markdown
1. [2024] MMAD - MMAD: The First-Ever Comprehensive Benchmark for Multimodal Large Language Models in Industrial Anomaly Detection
https://arxiv.org/abs/2410.09453

2. [2025] ADNet - ADNet: A Large-Scale and Extensible Multi-Domain Benchmark for Anomaly Detection Across 380 Real-World Categories
https://arxiv.org/abs/2511.20169

3. [Dataset] MVTec AD - The MVTec Anomaly Detection Dataset
https://www.mvtec.com/company/research/datasets/mvtec-ad

4. [Dataset] MVTec LOCO AD - Logical Constraints Anomaly Detection Dataset
https://www.mvtec.com/research-teaching/datasets/mvtec-loco-ad

5. [Dataset] MVTec AD 2 - The MVTec Anomaly Detection Dataset 2
https://www.mvtec.com/company/research/datasets/mvtec-ad-2

6. [Dataset] VisA - Visual Anomaly Dataset
https://registry.opendata.aws/visa/

7. [2021] CLIP - Learning Transferable Visual Models From Natural Language Supervision
https://arxiv.org/abs/2103.00020

8. [2021] ALBEF - Align before Fuse: Vision and Language Representation Learning with Momentum Distillation
https://arxiv.org/abs/2107.07651

9. [2022] BLIP - BLIP: Bootstrapping Language-Image Pre-training for Unified Vision-Language Understanding and Generation
https://arxiv.org/abs/2201.12086

10. [2023] BLIP-2 - BLIP-2: Bootstrapping Language-Image Pre-training with Frozen Image Encoders and Large Language Models
https://arxiv.org/abs/2301.12597

11. [2023] Grounding DINO - Grounding DINO: Marrying DINO with Grounded Pre-Training for Open-Set Object Detection
https://arxiv.org/abs/2303.05499

12. [2023] Florence-2 - Florence-2: Advancing a Unified Representation for a Variety of Vision Tasks
https://arxiv.org/abs/2311.06242

13. [2024] AnomalyCLIP - AnomalyCLIP: Object-agnostic Prompt Learning for Zero-shot Anomaly Detection
https://arxiv.org/abs/2310.18961

14. [2023] CLIP-AD - CLIP-AD: A Language-Guided Staged Dual-Path Model for Zero-shot Anomaly Detection
https://arxiv.org/abs/2311.00453

15. [2023] EfficientAD - EfficientAD: Accurate Visual Anomaly Detection at Millisecond-Level Latencies
https://arxiv.org/abs/2303.14535

16. [2021] PatchCore - Towards Total Recall in Industrial Anomaly Detection
https://arxiv.org/abs/2106.08265

17. [2024] Qwen2-VL - Qwen2-VL: Enhancing Vision-Language Model's Perception of the World at Any Resolution
https://arxiv.org/abs/2409.12191

18. [2024] InternVL2.5 - Expanding Performance Boundaries of Open-Source Multimodal Models with Model, Data, and Test-Time Scaling
https://arxiv.org/abs/2412.05271

19. [Docs] OpenAI - Images and Vision
https://platform.openai.com/docs/guides/images-vision

20. [Docs] Gemini - Image Understanding / Vision
https://ai.google.dev/gemini-api/docs/vision
```

---

## 7. 注意メモ

```markdown
- Deep Researchの本文中に出る `` のような文字列は、ChatGPT内部の引用タグなのでNotebookLMには不要。
- NotebookLMに入れるときは、上記のように「登録名 + URL」の形で入れるのが安全。
- GitHub、HF、Docs、Datasetは論文とは別ソースとして登録したほうがよい。
- 論文タイトルが曖昧な追跡候補は、NotebookLM投入前にarXivページで正式タイトルを確認する。
- MVTec系データセットは非商用ライセンスに注意。
```
