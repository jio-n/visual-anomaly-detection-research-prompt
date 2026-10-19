# VLM・工業画像異常検知 研究論文カタログ

**更新日：2026-10-19／53本（A:22件・B:2件・C:10件・D:19件）**

VLM研究のベンチマーキングレポートv0.5に掲載した論文と、周辺調査で確認した関連論文を統合した文献一覧です。英語の原著タイトル、初出年、概要（日本語）、原著URLを記録しています。

## 分類と注意事項

- **A：レポートv0.5掲載22本**。既存のTWV IDを維持。
- **B：前回TWV一覧にはあるがレポートv0.5には未掲載の2本**。TWV IDを維持。
- **C：このリポジトリの [deep-research-report.md](deep-research-report.md) の「NotebookLM登録用ソース一覧」から、A/Bとの重複を除いた10本**。
- **D：その他の関連研究として追加照合した19本**。今後のベンチマーク候補も含み、Codexによる収集実績を証明するリストではありません。
- **発表年は原則arXiv初出年／雑誌初出年**。学会採択・掲載年と異なる場合があります。原著の書誌を優先し、MMADの題名は原著表記に合わせてあります。
- **「文献のURLが確認できた」ことは「PDFをCodexがダウンロード済み」「精読済み」「FULL対訳済み」を意味しません**。ローカルの保存先とダウンロード履歴はこのリポジトリ上で検証できていないため、PDF取得状況は一律「未確認」です。
- **C/Dには新しいTWV IDを付与していません**。既存のMaster Tracker・レポート本文は変更していません。
- 研究概要は原著要旨と既存調査を要約した補助説明です。論文の主張と独自の産業応用提案を混同しないでください。

## 件数

| 区分 | 件数 | レポートv0.5掲載 | PDF取得状況 |
|---|---:|---|---|
| A | 22 | 掲載 | 未確認 |
| B | 2 | 未掲載 | 未確認 |
| C | 10 | 未掲載 | 未確認 |
| D | 19 | 未掲載 | 未確認 |
| **合計** | **53** | **22件掲載** | **要ローカル照合** |

## A. レポートv0.5掲載（22本）

| ID | 発表年（初出） | 正式論文タイトル | 概要 | 原著リンク |
|---|---:|---|---|---|
| TWV0001 | 2024 | MMAD: A Comprehensive Benchmark for Multimodal Large Language Models in Industrial Anomaly Detection | 工業異常検査について、異常判定だけでなく欠陥位置・種類・説明など複数の質問応答タスクでMLLMを体系的に評価するベンチマーク。 | [原著](https://arxiv.org/abs/2410.09453) |
| TWV0002 | 2022 | Visual Classification via Description from Large Language Models | LLMに分類対象の視覚的特徴を自然言語で説明させ、その記述と画像表現の一致度で分類する方法。分類に用いた属性を読み取れる。 | [原著](https://arxiv.org/abs/2210.07183) |
| TWV0004 | 2023 | DINOv2: Learning Robust Visual Features without Supervision | ラベルなし画像で高品質な視覚表現を自己教師あり学習し、分類や密な予測など幅広いタスクに転用できる画像基盤モデルを研究。 | [原著](https://arxiv.org/abs/2304.07193) |
| TWV0006 | 2021 | Learning Transferable Visual Models From Natural Language Supervision | 大規模な画像とテキストの組を対照学習して共通埋め込み表現を得るCLIPを提案。クラス名のテキストからzero-shot画像分類を行う。 | [原著](https://arxiv.org/abs/2103.00020) |
| TWV0007 | 2023 | Sigmoid Loss for Language Image Pre-Training | 画像・テキストのペアごとにsigmoid損失を計算するSigLIPを提案。softmax型対照学習との違いや学習効率、zero-shot性能を検証。 | [原著](https://arxiv.org/abs/2303.15343) |
| TWV0008 | 2021 | Align before Fuse: Vision and Language Representation Learning with Momentum Distillation | ALBEFを提案。画像とテキストを整列させてからクロスモーダルに融合し、momentum distillationでノイズのある教師情報への頑健性を高める。 | [原著](https://arxiv.org/abs/2107.07651) |
| TWV0009 | 2022 | BLIP: Bootstrapping Language-Image Pre-training for Unified Vision-Language Understanding and Generation | 画像言語理解と生成の両方を扱うBLIPを提案。caption生成・選別によってweb由来のノイズのある画像説明文を活用する。 | [原著](https://arxiv.org/abs/2201.12086) |
| TWV0010 | 2023 | BLIP-2: Bootstrapping Language-Image Pre-training with Frozen Image Encoders and Large Language Models | 凍結した画像エンコーダと大規模言語モデルを軽量なQ-Formerで接続し、追加学習パラメータを抑えつつ画像言語能力を獲得する。 | [原著](https://arxiv.org/abs/2301.12597) |
| TWV0011 | 2023 | Visual Instruction Tuning | LLaVAの初期論文。画像エンコーダとLLMを接続し、視覚的な指示応答データによるinstruction tuningで画像について対話できるモデルを構築する。 | [原著](https://arxiv.org/abs/2304.08485) |
| TWV0012 | 2024 | AnomalyDINO: Boosting Patch-based Few-shot Anomaly Detection with DINOv2 | DINOv2のパッチ特徴と正常画像参照の近傍比較を用いるfew-shot異常検知。異常スコアと位置の推定を目指す。 | [原著](https://arxiv.org/abs/2405.14529) |
| TWV0013 | 2023 | WinCLIP: Zero-/Few-Shot Anomaly Classification and Segmentation | CLIPをウィンドウ単位で利用し、zero-/few-shot条件で画像の正常・異常分類と欠陥領域の推定を行う。 | [原著](https://arxiv.org/abs/2303.14814) |
| TWV0014 | 2023 | AnomalyCLIP: Object-agnostic Prompt Learning for Zero-shot Anomaly Detection | 対象物の種類に依存しない正常・異常のテキストプロンプトを学習し、未知の物体カテゴリの異常判定・セグメンテーションへ一般化する。 | [原著](https://arxiv.org/abs/2310.18961) |
| TWV0015 | 2023 | AnomalyGPT: Detecting Industrial Anomalies Using Large Vision-Language Models | 工業画像の異常を検知・局所化し、自然言語で対話するVLM型の枠組み。擬似異常の生成と指示データの利用を検討する。 | [原著](https://arxiv.org/abs/2308.15366) |
| TWV0016 | 2025 | Towards Zero-Shot Anomaly Detection and Reasoning with Multimodal Large Language Models | Anomaly-OneVision（Anomaly-OV）とLook-Twice Feature Matching等を用い、ゼロショット異常検知と異常に関する推論・回答を強化する。 | [原著](https://arxiv.org/abs/2502.07601) |
| TWV0017 | 2026 | AD-Copilot: A Vision-Language Assistant for Industrial Anomaly Detection via Visual In-context Comparison | 正常参照と検査画像の特徴をクロスアテンションで比較するComparison Encoderを提案。工業異常のQA・欠陥局所化を強化する。 | [原著](https://arxiv.org/abs/2603.13779) |
| TWV0018 | 2026 | JUDO: A Juxtaposed Domain-Oriented Multimodal Reasoner for Industrial Anomaly QA | 検査画像と正常参照画像の並置比較から欠陥領域を把握し、ドメイン知識のSFTとGRPOで工業異常に関する回答を改善する。 | [原著](https://arxiv.org/abs/2605.20284) |
| TWV0019 | 2020 | An Image is Worth 16x16 Words: Transformers for Image Recognition at Scale | 画像を小さなパッチの列としてTransformerへ入力するVision Transformer（ViT）を提案。画像分類の基本アーキテクチャ。 | [原著](https://arxiv.org/abs/2010.11929) |
| TWV0026 | 2021 | Towards Total Recall in Industrial Anomaly Detection | PatchCoreを提案。事前学習済みの局所視覚特徴と正常パッチのmemory bankとの距離から異常スコアと異常箇所を推定する。 | [原著](https://arxiv.org/abs/2106.08265) |
| TWV0032 | 2025 | Morphological segmentation of wear zones on cutting inserts for tool condition monitoring | 低コストのUSB顕微鏡とMATLABの形態学的画像処理により切削インサートの摩耗領域を抽出・計測する。古典的画像処理との比較に有用。 | [原著](https://doi.org/10.1177/16878132251388275) |
| TWV0042 | 2021 | Emerging Properties in Self-Supervised Vision Transformers | DINOの自己蒸留型学習を検証。ラベルなしViTの特徴やattentionが物体領域の情報を捉える性質と転用性能を示す。 | [原著](https://arxiv.org/abs/2104.14294) |
| TWV0181 | 2026 | Implementation of Vision Transformer Model for Robust Tool Wear Monitoring in Milling of Inconel 718 | Inconel 718の切削工具の摩耗カテゴリをViTで識別し、EfficientNet-B0と比較。未知画像や照明変動条件で頑健性を評価。 | [原著](https://doi.org/10.3390/machines14060589) |
| TWV0182 | 2019 | Automatic Identification of Tool Wear Based on Convolutional Neural Network in Face Milling Process | 正面フライス加工で撮像した工具画像からCNNで工具摩耗種類を識別する。畳み込みオートエンコーダによる事前学習も用いる。 | [原著](https://doi.org/10.3390/s19183817) |

## B. TWVで管理しているがv0.5未掲載（2本）

| ID | 発表年（初出） | 正式論文タイトル | 概要 | 原著リンク |
|---|---:|---|---|---|
| TWV0020 | 2023 | Grounding DINO: Marrying DINO with Grounded Pre-Training for Open-Set Object Detection | 言語で記述した物体をbboxで位置特定するopen-set検出。欠陥候補の説明文に基づく探索やセグメンテーションとの連携が可能。 | [原著](https://arxiv.org/abs/2303.05499) |
| TWV0021 | 2023 | Segment Anything | 点や矩形などのプロンプトを使って汎用画像セグメンテーションを行うSAMを提案。欠陥候補のマスク化に利用できる。 | [原著](https://arxiv.org/abs/2304.02643) |

## C. 既存GitHub調査表に掲載、前回の24本に含まれない（10本）

| ID | 発表年（初出） | 正式論文タイトル | 概要 | 原著リンク |
|---|---:|---|---|---|
| — | 2023 | InstructBLIP: Towards General-purpose Vision-Language Models with Instruction Tuning | 指示内容に応じた視覚特徴抽出を可能にするinstruction-awareな画像言語モデルを学習し、幅広いVQA・理解・生成タスクへの汎化を検証する。 | [原著](https://arxiv.org/abs/2305.06500) |
| — | 2023 | Improved Baselines with Visual Instruction Tuning | LLaVA-1.5として、視覚指示チューニングの構成や学習データを改良し、簡潔な構成で多様なVLMベンチマークの性能を改善する。 | [原著](https://arxiv.org/abs/2310.03744) |
| — | 2024 | Qwen2-VL: Enhancing Vision-Language Model's Perception of the World at Any Resolution | 多様な画像解像度に対応するMLLM。画像・動画理解、OCR、VQA、文書理解などの能力を評価する。 | [原著](https://arxiv.org/abs/2409.12191) |
| — | 2024 | Expanding Performance Boundaries of Open-Source Multimodal Models with Model, Data, and Test-Time Scaling | InternVL2.5について、モデル規模、データ、推論時のスケーリングがマルチモーダル性能に与える影響を検証する。 | [原著](https://arxiv.org/abs/2412.05271) |
| — | 2023 | Florence-2: Advancing a Unified Representation for a Variety of Vision Tasks | テキストのタスク指示によりcaptioning、検出、grounding、OCRなどをsequence-to-sequence形式で統合する視覚基盤モデル。 | [原著](https://arxiv.org/abs/2311.06242) |
| — | 2021 | Grounded Language-Image Pre-training | GLIPを提案。言語によるgroundingと物体検出を統合した事前学習を通じて、語彙で指定した物体を検出する。 | [原著](https://arxiv.org/abs/2112.03857) |
| — | 2022 | Generalized Decoding for Pixel, Image, and Language | X-Decoderを提案。ピクセル領域、画像、言語を統合的に処理する汎用デコーダで、分割や言語条件付き理解などを扱う。 | [原著](https://arxiv.org/abs/2212.11270) |
| — | 2023 | CLIP-AD: A Language-Guided Staged Dual-Path Model for Zero-shot Anomaly Detection | CLIPのテキスト表現を改善し、階層特徴を使うStaged Dual-Pathで欠陥領域を推定。zero-shot異常検知の改良を目指す。 | [原著](https://arxiv.org/abs/2311.00453) |
| — | 2023 | EfficientAD: Accurate Visual Anomaly Detection at Millisecond-Level Latencies | student-teacher型等を活用し、工業検査で高い異常検知性能とミリ秒級の推論速度を両立させる。 | [原著](https://arxiv.org/abs/2303.14535) |
| — | 2025 | ADNet: A Large-Scale and Extensible Multi-Domain Benchmark for Anomaly Detection Across 380 Real-World Categories | 産業・医療等380カテゴリにわたる異常検知評価ベンチマーク。多様な画像とピクセル注釈・構造化テキストを整備する。 | [原著](https://arxiv.org/abs/2511.20169) |

## D. そのほか関連調査で確認した論文（19本）

| ID | 発表年（初出） | 正式論文タイトル | 概要 | 原著リンク |
|---|---:|---|---|---|
| — | 2021 | DRAEM -- A discriminatively trained reconstruction embedding for surface anomaly detection | 正常画像の再構成と異常箇所を識別するネットワークを組み合わせ、疑似異常で訓練する表面異常の局所化手法。 | [原著](https://arxiv.org/abs/2108.07610) |
| — | 2021 | FastFlow: Unsupervised Anomaly Detection and Localization via 2D Normalizing Flows | 画像エンコーダの特徴に2次元normalizing flowを適用し、尤度から教師なしの異常スコアと領域を推定する。 | [原著](https://arxiv.org/abs/2111.07677) |
| — | 2021 | CFLOW-AD: Real-Time Unsupervised Anomaly Detection with Localization via Conditional Normalizing Flows | 複数スケールの画像特徴を条件付きnormalizing flowでモデル化し、高速な異常検知・局所化を目指す。 | [原著](https://arxiv.org/abs/2107.12571) |
| — | 2020 | PaDiM: a Patch Distribution Modeling Framework for Anomaly Detection and Localization | 正常画像のパッチ特徴を位置ごとの多変量ガウス分布としてモデル化し、正常分布からの距離で異常を検出する。 | [原著](https://arxiv.org/abs/2011.08785) |
| — | 2024 | SAM 2: Segment Anything in Images and Videos | 画像・動画を対象とするプロンプト可能なセグメンテーションを提案し、動画での対象追跡とマスク推定を統合する。 | [原著](https://arxiv.org/abs/2408.00714) |
| — | 2023 | Segment Everything Everywhere All at Once | SEEMを提案。テキスト、点、boxなど複数の指示形式を使って対象領域をセグメンテーションする。 | [原著](https://arxiv.org/abs/2304.06718) |
| — | 2024 | What matters when building vision-language models? | Idefics2の開発を題材に、画像言語モデルのアーキテクチャ、学習データ、訓練方法の選択を比較・検証する。 | [原著](https://arxiv.org/abs/2405.02246) |
| — | 2025 | OmniAD: Detect and Understand Industrial Anomaly via Multimodal Reasoning | 工業異常の検知と推論・説明をつなぐMLLMアプローチ。ドメイン固有の画像情報を扱い、推論能力を向上させる。 | [原著](https://arxiv.org/abs/2505.22039) |
| — | 2024 | VMAD: Visual-enhanced Multimodal Large Language Model for Zero-Shot Anomaly Detection | 局所的な欠陥を捉える視覚特徴でマルチモーダル言語モデルを補強し、zero-shot異常検知と説明を行う。 | [原著](https://arxiv.org/abs/2409.20146) |
| — | 2025 | IAD-GPT: Advancing Visual Knowledge in Multimodal Large Language Model for Industrial Anomaly Detection | マルチモーダル大規模言語モデルに工業的な視覚知識を追加し、欠陥の検知・位置特定・説明能力の改善を図る。 | [原著](https://arxiv.org/abs/2510.16036) |
| — | 2026 | MMR-AD: A Large-Scale Multimodal Dataset for Benchmarking General Anomaly Detection with Multimodal Large Language Models | 異常の推論・識別をMLLMで評価する大規模マルチモーダルデータセットとベンチマークを提案する。 | [原著](https://arxiv.org/abs/2604.10971) |
| — | 2025 | Towards Open-Vocabulary Industrial Defect Understanding with a Large-Scale Multimodal Dataset | IMDD-1Mとして100万画像・説明文ペアを整備し、製造欠陥についてopen-vocabularyな理解やモデル適応を研究する。 | [原著](https://arxiv.org/abs/2512.24160) |
| — | 2024 | FabGPT: An Efficient Large Multimodal Model for Complex Wafer Defect Knowledge Queries | ウェハ欠陥のSEM画像認識と製造知識を用いたQA・原因分析を支援する半導体プロセス特化MLLM。 | [原著](https://arxiv.org/abs/2407.10810) |
| — | 2025 | Towards Training-free Anomaly Detection with Vision and Language Foundation Models | LogSADを提案。多粒度で領域と構成関係を照合し、追加学習なしに論理異常と構造異常を扱う。 | [原著](https://arxiv.org/abs/2503.18325) |
| — | 2025 | AD-FM: Multimodal LLMs for Anomaly Detection via Multi-Stage Reasoning and Fine-Grained Reward Optimization | 検出位置を確認してから判定する多段階推論と、分類・局所化に関する細粒度報酬によりMLLMの異常検査能力を改善する。 | [原著](https://arxiv.org/abs/2508.04175) |
| — | 2025 | EMIT: Enhancing MLLMs for Industrial Anomaly Detection via Difficulty-Aware GRPO | 難易度を考慮したGRPOによって工業異常QA向けMLLMの強化学習を改善する。 | [原著](https://arxiv.org/abs/2507.21619) |
| — | 2025 | EIAD: Explainable Industrial Anomaly Detection Via Multi-Modal Large Language Models | マルチモーダル言語モデルを利用し、工業異常の検出に加えて位置や理由の説明を行うアプローチ。 | [原著](https://arxiv.org/abs/2503.14162) |
| — | 2025 | AnomalyR1: A GRPO-based End-to-end MLLM for Industrial Anomaly Detection | GRPOを用いたend-to-endの工業異常検査MLLM。異常の推論・位置検出・マスク推定を統合的に学習する。 | [原著](https://arxiv.org/abs/2504.11914) |
| — | 2026 | M3-AD: Reflection-aware Multi-modal, Multi-category, and Multi-dimensional Benchmark and Framework for Industrial Anomaly Detection | 自らの初回判断を見直すreflection-awareな工業異常検出のベンチマークとフレームワークを提案する。 | [原著](https://arxiv.org/abs/2603.00055) |

## 利用・更新方法

- スプレッドシートへの取り込みには同梱の [paper-catalog.csv](paper-catalog.csv) を使用してください。CSVの `TWV_ID` が空欄の行は未採番です。
- PDF保存済み一覧と照合する際は、実ファイル名・ダウンロード記録を根拠として取得状況を変更してください。
- GitHubの既存 [deep-research-report.md](deep-research-report.md) にはモデル比較・NotebookLM用リンクもあります。ここでは論文（53本）を対象とし、APIドキュメントや単独のデータセット配布ページを件数に含めていません。
