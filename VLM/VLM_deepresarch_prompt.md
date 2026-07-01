# Deep Research プロンプト
## テーマ
**Vision-Language Model（VLM）を用いた異常検知・欠陥検出・損傷分類に関する研究動向の包括的サーベイ**

---

# あなたの役割

あなたは、

- コンピュータビジョン
- Vision-Language Model (VLM)
- 画像異常検知
- 製造業AI
- 品質検査
- マルチモーダルAI

の専門家です。

単なる論文検索ではなく、

**「この分野のサーベイ論文を1本執筆する」**

レベルの品質で調査・分析を行ってください。

論文を羅列するのではなく、

- 現在どのような研究が存在するのか
- 技術はどのように発展してきたのか
- どのような流派・カテゴリに分類できるのか
- 現在の主流技術は何か
- 未解決課題は何か
- 今後の研究テーマは何か

まで体系的に整理してください。

---

# 調査目的

Vision-Language Model（VLM）を利用した

- 異常検知
- 欠陥検出
- 欠陥分類
- 損傷分類
- 摩耗分類
- 外観検査
- 品質検査

に関する研究を包括的に調査してください。

私が最も興味を持っているのは

**製造業・工業製品・品質検査**

です。

特に

- 超硬インサート
- 切削工具
- 工具摩耗
- クレータ摩耗
- 境界摩耗
- チッピング
- 金属部品
- 自動車部品
- 半導体
- 電子部品
- 機械部品

などの外観検査・異常検知を優先してください。

---

# 対象分野

優先順位は以下としてください。

1. 製造業
2. FA・品質検査
3. 半導体検査
4. 電子部品検査
5. ロボット検査
6. 医療画像
7. インフラ点検
8. 建築
9. 農業
10. 衛星画像
11. 一般画像異常検知

製造業の論文が少ない場合のみ、対象範囲を徐々に広げてください。

---

# 調査対象

以下を優先してください。

## 学術検索

- Google Scholar
- Semantic Scholar
- arXiv

## 学会

- CVPR
- ICCV
- ECCV
- WACV
- NeurIPS
- ICML
- ICLR
- AAAI

## ジャーナル

- TPAMI
- IJCV
- TIP
- TNNLS
- Pattern Recognition
- IEEE Access
- Sensors
- Journal of Manufacturing Systems
- Robotics and Computer-Integrated Manufacturing

2022年以降を中心に調査してください。

ただし、重要な基礎論文・古典論文がある場合は必ず含めてください。

---

# 調査してほしいこと

## ① この分野はどのような技術カテゴリに分類できるのか

論文を単純に並べるのではなく、

**研究の流派・アプローチごとに分類してください。**

例えば以下のような分類が存在するか調査してください。

### Prompt系

- Prompt Engineering
- Prompt Learning
- Visual Prompt Tuning
- Soft Prompt
- CoOp
- CoCoOp

---

### Few-shot / Zero-shot系

- Zero-shot
- One-shot
- Few-shot
- In-Context Learning

---

### Fine-tuning系

- Fine-tuning
- LoRA
- QLoRA
- Adapter
- PEFT

---

### ハイブリッドモデル

- VLM + CNN
- VLM + ViT
- VLM + SAM
- VLM + Grounding DINO
- VLM + RAG
- VLM + Agent
- VLM + Knowledge Graph
- VLM + External Memory

---

### 推論手法

- Chain of Thought
- Visual Chain of Thought
- Multimodal Reasoning
- Self Reflection
- Planning

---

### Explainability

- 自然言語による説明生成
- 異常理由説明
- Visual Grounding
- Explainable AI

---

### データ工夫

- Synthetic Data
- Data Augmentation
- Self-supervised Learning
- Weak Supervision
- Domain Adaptation
- Active Learning

---

### 推論時の工夫

- Test-time Adaptation
- Retrieval Augmentation
- Ensemble
- Multi-Agent

---

## ② 使用されているVLM

どのVLMが利用されているのか整理してください。

例

- CLIP
- OpenCLIP
- BLIP
- BLIP-2
- InstructBLIP
- LLaVA
- MiniGPT-4
- GPT-4V
- Gemini
- Claude Vision
- Florence
- Florence-2
- Qwen-VL
- Qwen2-VL
- InternVL
- Molmo
- CogVLM
- PaLI
- Kosmos
- DeepSeek-VL

について

- なぜ採用されたのか
- 長所
- 短所
- 製造業との相性

を整理してください。

---

## ③ 製造業特有の課題をどう解決しているのか

例えば

- 少量データ
- ラベル不足
- 未知欠陥
- 微小欠陥
- 高解像度画像
- ドメインシフト
- クラス不均衡
- Explainability

について

各研究がどのように解決しているのか整理してください。

---

# 各論文についてまとめる内容

各論文について以下を整理してください。

|項目|内容|
|---|---|
|タイトル||
|著者||
|発表年||
|学会・ジャーナル||
|DOI||
|論文URL||
|PDF URL||
|GitHub||
|Project Page||
|被引用数（可能なら）||
|対象ドメイン||
|対象タスク||
|対象物||
|使用データセット||
|使用VLM||
|その他モデル||
|学習方法||
|プロンプト利用の有無||
|提案手法||
|新規性||
|評価指標||
|結果||
|強み||
|弱み||
|今後の課題||

---

# 比較表

以下の比較表を作成してください。

- 使用VLM
- 学習方法
- Zero-shot対応
- Few-shot対応
- Fine-tuning必要性
- Explainability
- OSS公開有無
- 実運用しやすさ
- 推論コスト

---

# 年代別トレンド

2020年頃から現在まで

- 2020
- 2021
- 2022
- 2023
- 2024
- 2025
- 最新

について

技術がどのように変化してきたのかを整理してください。

---

# 技術マップ

研究全体を俯瞰できるよう、

技術をツリー構造またはカテゴリ構造で整理してください。

例

```
VLM異常検知

├ Prompt系
├ Fine-tuning系
├ CLIP系
├ GPT系
├ Explainability
├ Hybrid
├ Agent
├ RAG
├ SAM
└ その他
```

---

# 研究ギャップ

現在まだ十分研究されていないテーマを整理してください。

例えば

- 工具摩耗分類
- 超硬インサート
- クレータ摩耗
- 境界摩耗
- チッピング
- Video Microscope画像
- Few-shot
- Explainable Inspection
- VLM + Agent
- VLM + RAG
- VLM + SAM
- VLM + Knowledge Graph

などについて

- なぜ研究されていないのか
- 技術的難易度
- 新規性
- インパクト

を考察してください。

---

# 私の研究テーマに対する提案

以下の研究テーマを前提に、

最も適した技術構成を提案してください。

> Video Microscopeで撮影した超硬インサート画像から、
>
> - クレータ摩耗
> - 境界摩耗
> - チッピング
> - その他摩耗状態
>
> を少量データで分類し、
>
> VLMによって分類理由を自然言語で説明できるシステムを構築したい。

以下について提案してください。

- 最適なVLM
- 推奨アーキテクチャ
- 推奨データセット
- 推奨学習方法
- 推奨評価指標
- 実装難易度
- 研究としての新規性
- 学術的インパクト
- 実用性

---

# 最重要論文

私の研究テーマに最も近い論文を重要度順に20本程度ランキングしてください。

ランキング理由も説明してください。

---

# 出力形式

以下の順番で出力してください。

1. エグゼクティブサマリー
2. 分野全体の概要
3. 技術カテゴリの整理
4. 年代別トレンド
5. VLMごとの特徴比較
6. 製造業への適用事例
7. 他分野への適用事例
8. 論文一覧（表形式）
9. 比較表
10. 研究ギャップ
11. 今後の研究方向
12. 私の研究テーマへの提案
13. おすすめ論文ランキング
14. 参考文献一覧

---

# 出力要件

- 出力は**すべて日本語**で記述してください。
- 論文タイトルは原文（英語）のままとし、日本語で概要を説明してください。
- 専門用語には必要に応じて英語を併記してください。
- 表や箇条書きを積極的に用い、読みやすく整理してください。
- 推測と事実は明確に区別してください。
- 各論文について、可能な限り以下を記載してください。
  - 論文ページURL
  - PDF URL
  - GitHub
  - Project Page
- 単なる論文一覧ではなく、「研究分野全体のサーベイ論文」として読める品質を目指してください。
- 最後に「今後3〜5年で有望と考えられる研究テーマ」を提案してください。
