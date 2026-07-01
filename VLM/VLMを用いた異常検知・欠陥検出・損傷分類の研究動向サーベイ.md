# VLMを用いた異常検知・欠陥検出・損傷分類の研究動向サーベイ

## エグゼクティブサマリー

Vision-Language Model（VLM）やMultimodal Large Language Model（MLLM）を異常検知へ使う研究は、**工業用外観検査の主流をすでに置き換えた**という段階ではなく、**CLIP系のゼロ／少数ショット異常検知**と、**説明可能性を持つ対話型MLLM**が急速に立ち上がった過渡期にあります。分野全体としては、CLIPに代表される埋め込み型VLMが、まずゼロショット／少数ショット検査の基盤を作り、その後に AnomalyGPT、FabGPT、EIAD、Anomaly-OV、AD-Copilot のような「検知＋局在化＋説明」を統合する専用アシスタント型へ進んでいます。いっぽうで、実運用を見据えると、依然として MVTec AD / VisA / MVTec LOCO AD / MVTec 3D-AD などのベンチマーク依存が強く、微小欠陥・高倍率顕微鏡画像・工程依存の摩耗状態分類といった現実の製造課題には未解決部分が多く残っています。 citeturn2search19turn3search0turn3search6turn3search13turn1search0turn20search0

技術的には、現時点で大きく五つの流派に整理できます。第一に、WinCLIP・AnomalyCLIP・VCP-CLIP・PromptAD・Bayes-PFL・AA-CLIP・FE-CLIP・FAPrompt などに代表される **CLIP中心の prompt / adapter / prompt-learning 系**。第二に、PromptAD、IIPAD、Vision-Language In-Context Learning Driven Few-Shot Visual Inspection Model、AD-Copilot などの **few-shot / in-context comparison 系**。第三に、AnomalyGPT、EIAD、Anomaly-OV、EMIT、AD-FM のような **MLLM微調整・専用データセット構築・推論強化系**。第四に、LogicAD、LogicQA、LogSAD、AnomalyRuler のような **ルール・論理・推論系**。第五に、VELM や FabGPT のような **検出器＋言語モデルのハイブリッド実務系**です。 citeturn10search0turn2search16turn2search20turn11search0turn14search0turn2search9turn8search2turn8search1turn12search0turn1search1turn18search0turn1search0turn17search1turn13search1turn19search1turn19search2turn8search0turn1search16turn7search1turn25search0turn15search0turn16search1

あなたのテーマである **Video Microscopeで撮影した超硬インサートの摩耗状態分類と自然言語説明** に最も近い既存研究は、厳密にはまだ少ないです。今回確認できた公開VLM研究の中心は、汎用工業異常検知、半導体ウエハ欠陥、論理異常、あるいは MVTec/VisA ベンチマーク上の欠陥検知であり、**クレータ摩耗・境界摩耗・チッピングを直接扱うVLM研究は見当たりませんでした**。一方で、工具摩耗そのものは従来のCV研究や顕微鏡画像処理研究では進んでおり、VLM研究との間に明確な研究ギャップがあります。これは修士・博士研究として非常に有望です。 citeturn16search1turn1search1turn1search0turn20search0turn21search6turn21search23

## 分野の全体像

VLMベース異常検知の土台は、CLIP の「画像と自然言語を同一埋め込み空間に写す」能力にあります。CLIP 以降、テキストで正常／異常概念を与えながら未知カテゴリへ転移する発想が可能になり、工業検査では WinCLIP がその代表的な出発点になりました。BLIP-2 は凍結済み視覚エンコーダとLLMを軽量に接続する枠組みを、LLaVA は視覚指示チューニングを、Qwen2-VL と Qwen2.5-VL は高解像度・多解像度処理や強い汎用視覚理解を提供し、後続の産業特化モデル群のベースとして使われやすくなっています。 citeturn4search0turn4search1turn5search0turn4search2turn18search13

この分野の成長を支えたのは、モデルだけでなくベンチマークの整備です。MVTec AD は高解像度の15カテゴリ工業画像を含む定番ベンチマークで、MVTec LOCO AD は表面欠陥だけでなく構造・論理異常を評価できるように設計されました。MVTec 3D-AD はRGBと3Dの両方を含み、Eyecandies はRGB・depth・normalを持つ合成マルチモーダル異常検知データセット、VisA はより大規模な産業外観異常データセットです。さらに MMAD は「工業用MLLMをどう評価するか」に焦点を当てた包括ベンチマークで、7つのサブタスクと 39,672 問のQAを用いて、既存MLLMの能力がまだ工業要求に達していないことを示しました。 citeturn2search19turn3search0turn3search6turn3search7turn3search13turn20search0

重要なのは、**VLM異常検知は「単なるゼロショット分類」から「局在化」「理由説明」「工程知識との結合」へ移っている**ことです。AnomalyGPT は工業画像の異常有無・位置・説明を一体化した最初期の専用LVLMのひとつで、FabGPT は半導体製造のSEM画像と工程知識QAを接続し、EIAD はDDQAという専用マルチモーダルデータセットを作って説明と局在化を分離最適化し、Anomaly-OV は大規模指示データセットとLook-Twice Feature Matchingで「異常検知＋推論」を本格化させました。AD-Copilot は比較エンコーダで基準画像との細粒度差分を見る方向へ進み、M3-AD や MMR-AD は「自己反省」「CoT」「一般異常検知ベンチマーク」の時代に入ったことを示しています。 citeturn1search0turn16search1turn17search1turn13search1turn18search0turn20search5turn20search1

## 技術カテゴリの整理

### CLIP系ゼロショット異常検知

最も層が厚いのは CLIP を基盤にしたゼロショット／少数ショット異常検知です。WinCLIP はテンプレートと state word の compositional prompt ensemble、さらに window-based な局所特徴集約で、工業異常分類・セグメンテーションをゼロショット／few-normal-shot で成立させました。AnomalyCLIP は「物体カテゴリ」ではなく「異常性そのもの」を学ぶ object-agnostic prompt learning を打ち出し、この系統の基準点になりました。VCP-CLIP は visual context prompting を導入して、手作業プロンプト依存を減らしつつ詳細局在化を強化しました。AA-CLIP、FE-CLIP、FAPrompt、Bayes-PFL はいずれも「異常テキスト表現をどう細粒度化・多様化・安定化するか」という問題に取り組んでいます。 citeturn10search0turn2search16turn2search20turn2search9turn8search2turn8search1turn14search0

この流派の長所は、**ラベルコストが低いこと、未知カテゴリへ比較的転移しやすいこと、実装が軽いこと**です。短所は、**微小欠陥や形態学的に非常に subtle な異常では、テキスト埋め込みだけでは差を十分捉えにくいこと**、そして自然言語で「なぜ異常か」を深く説明する力が限定的なことです。工場導入の第一歩としては非常に有力ですが、説明性や根本原因分析が必要になると、後述のMLLM系に分があります。 citeturn10search0turn2search16turn2search20turn13search1

### Prompt Learning・PEFT・Adapter系

PromptAD は、正常画像しかない one-class few-shot 設定で prompt learning を成立させた重要研究です。IIPAD はさらに「one-for-one」ではなく「one-for-all」へ進み、カテゴリ共有の prompt generator で実運用性を上げました。MVFA-AD は医療ですが、multi-level residual adapter と多層の visual-language alignment により、自然画像で学習された CLIP をドメイン適応する代表例です。AdaptCLIP も visual adapter・textual adapter・prompt-query adapter を追加する軽量構成で、工業と医療の多ベンチマークへ汎化する方向を示しています。 citeturn11search0turn12search0turn23search1turn23academia20

このカテゴリは、とくに**少量データ・高ドメインシフト**に強いです。あなたのように超硬インサートの顕微鏡画像を扱う場合、一般Web画像からの乖離が大きいため、完全な training-free よりも、PEFTやadapterの方が現実的である可能性が高いです。逆に大規模 end-to-end fine-tuning はデータ収集と計算コストの面で割に合わないことが多く、PromptAD / IIPAD / MVFA-AD 型の軽量適応が第一候補になります。 citeturn11search0turn12search0turn23search1turn18search0

### Few-shot・In-Context Learning・Visual Comparison系

最近の工業検査では、**比較対象となる正常品を数枚見せ、その差を言語的に説明しながら検査する**という、人間の検査行動に近い設計が増えています。Vision-Language In-Context Learning Driven Few-Shot Visual Inspection Model は、説明文つきの正常／異常画像をコンテキストとして与え、新製品に one-shot で適用する一般検査モデルを提案しました。AD-Copilot は Qwen2.5-VL ベースに cross-attention型 Comparison Encoder を導入し、画像を独立に理解する従来MLLMの弱点を補っています。LogSAD や LogicQA も、正常参照画像と論理ルールを与えて異常を判断する点で、広い意味の in-context inspection とみなせます。 citeturn1search1turn18search0turn7search1turn1search16

この方向性は、**あなたの研究テーマと最も相性が良い**です。工具摩耗の判定では、絶対的な損傷形状よりも「新品基準との差」「許容摩耗か限界摩耗か」が重要になるため、正常参照や良品参照を複数与える visual comparison は理にかなっています。しかも Video Microscope 画像は同一姿勢・同一倍率で取得しやすく、比較学習の恩恵を受けやすいです。AD-Copilot の発想を、超硬インサート用の比較エンコーダと摩耗語彙へ移植するのは、非常に筋の良い研究テーマです。 citeturn18search0turn1search1turn21search23

### MLLMアシスタント・説明生成・専用データセット系

AnomalyGPT は「工業異常検知の対話アシスタント」という方向を初めて大きく切り開いた研究です。FabGPT は半導体製造向けに、微小欠陥検出・根本原因分析・Q&A をまとめて扱いました。EIAD は DDQA を構築し、対話機能と局在化機能を分離したことで過学習と説明性低下を抑えようとしています。Anomaly-OV は Anomaly-Instruct-125k と VisA-D&R を作り、一般MLLMが fine-grained anomaly reasoning に弱いことを示した上で、Look-Twice Feature Matching による専門モデルを提案しました。EMIT と AD-FM はさらに GRPO や multi-stage reasoning を導入し、推論過程そのものを改善しています。 citeturn1search0turn16search1turn17search1turn13search1turn19search1turn19search2

この流派の最大の価値は、**説明可能性（Explainability）と人的運用との整合性**です。工場の現場では「異常です」だけでは足りず、「どこが」「なぜ」「どう危険か」「どの不良種別か」が必要です。そのため、二値分類精度が多少落ちても、説明や対話が付くことで総合的な価値が上がるケースがあります。反面、MLLM系は高解像度微小欠陥への生の感度がまだ十分ではなく、MMAD でも既存商用・OSS MLLMは工業要求に届いていません。ゆえに、現実的には **専用視覚モジュール＋言語モジュールの分業** がまだ有効です。 citeturn20search0turn17search1turn15search0turn18search0

### 論理異常・規則推論・Chain-of-Thought系

表面傷や欠けではなく、**構成・配置・数・関係の異常**を扱う論理異常系も急速に伸びています。LogicAD はAVLMからテキスト特徴を取り出し、logic reasoner と組み合わせて MVTec LOCO AD で説明付き異常検知を達成しました。LogicQA は数枚の正常画像から論理ルールを記述し、few-shot で logical AD を行います。LogSAD は GPT-4V を使った match-of-thought で関心対象と構成ルールを作り、構造異常と論理異常を訓練なしで統一処理しました。動画側では AnomalyRuler が正常例からルールを誘導し、LLM推論で VAD を行っています。 citeturn8search0turn1search16turn7search1turn25search0

あなたのテーマは論理異常ではなく摩耗・欠損に近いですが、**「摩耗判定基準を自然言語ルールとして明示する」**という意味では、この系統は大いに参考になります。たとえば「刃先境界線に沿って連続的な摩耗帯が存在する」「クレータがすくい面中央から刃先寄りへ拡大している」「チッピングは局所的な欠損であって一様摩耗ではない」といった規則を、few-shot normal/abnormal reference とともに与える設計は、LogicQA や LogSAD の思想に近いです。 citeturn1search16turn7search1turn25search0

## 年代別トレンド

2020〜2022年は、異常検知そのものではなく「VLMを異常検知へ使える土台」が整った時期です。CLIP がゼロショット転移を可能にし、MVTec AD・VisA・MVTec LOCO AD・MVTec 3D-AD といったベンチマークが異常検知の評価対象を体系化しました。まだ専用VLM異常検知は主流ではなく、異常検知は主として reconstruction / embedding / one-class 学習の時代でした。 citeturn4search0turn2search19turn3search1turn3search0turn3search6

2023年は WinCLIP と AnomalyGPT が転機でした。WinCLIP により「CLIPをそのまま anomaly classification/segmentation に引っ張る」路線が明確になり、AnomalyGPT により「検知＋位置＋説明＋対話」を統合した industrial assistant が初めて強く打ち出されました。この二本立てが、以後の研究をほぼ決めています。 citeturn10search0turn1search0

2024年は、**prompt learning の洗練とドメイン適応**が中心テーマでした。AnomalyCLIP、PromptAD、VCP-CLIP、MVFA-AD、Customizable-VLM、FabGPT がそれぞれ、object-agnostic 異常表現、normal-only few-shot prompt learning、visual context prompting、adapter-based medical adaptation、expert knowledge prompting、半導体工程知識埋め込みを打ち出しました。つまりこの時期は、「VLMは使える」から「どう適応させると工業で効くか」への移行期です。 citeturn2search16turn11search0turn2search20turn23search1turn24search0turn16search1

2025年は、**推論・説明・評価ベンチマーク**の年です。MMAD が 工業MLLM評価を体系化し、Anomaly-OV が instruction tuning と reasoning benchmark を整備し、EIAD が説明付き工業IADデータセット DDQA を追加し、LogSAD・LogicAD・LogicQA が規則推論を押し上げました。同時に Bayes-PFL、AA-CLIP、FE-CLIP、FAPrompt は prompt 表現の豊かさと安定性をさらに高めました。ここで分野は、単なる detection から reasoning へ一段階進みました。 citeturn20search0turn13search1turn17search1turn7search1turn8search0turn1search16turn14search0turn2search9turn8search2turn8search1

2026年は、**専門アシスタント化・反省的推論・一般異常検知化**がキーワードです。AD-Copilot は visual in-context comparison を軸に高性能専門助手を目指し、MMR-AD は general anomaly detection 用の大規模マルチモーダルデータセットと CoT 学習を導入し、M3-AD は self-correction / reflection を導入しました。これは「VLMで異常を見つける」から、「VLMが専門家のように比較し、考え直し、説明する」段階への移行といえます。 citeturn18search0turn20search1turn20search5

## 主要論文一覧

以下の表は、工業優先で選んだ主要論文を、技術的な役割が分かるように整理したものです。表中の内容は各論文の公式ページ・PDF・コード・プロジェクトページに基づく要約です。 citeturn1search0turn1search1turn16search1turn17search1turn13search1turn18search0

| 論文 | 年 | ドメイン | 主VLM/基盤 | 技術カテゴリ | ひと言での特徴 | OSS |
|---|---:|---|---|---|---|---|
| WinCLIP | 2023 | 工業一般 | CLIP | Zero/Few-shot | CLIPの窓特徴とprompt ensembleで工業ADを実用域へ押し上げた出発点 | あり |
| AnomalyGPT | 2023/2024 | 工業一般 | 画像エンコーダ + LLM | MLLM assistant | 検知・局在化・説明・対話を統合した初期専用LVLM | あり |
| AnomalyCLIP | 2024 | 汎用AD | CLIP | Prompt learning | object-agnostic異常プロンプトで広い領域へ転移 | あり |
| PromptAD | 2024 | 工業一般 | CLIP系 | Few-shot prompt learning | 正常画像のみで few-shot prompt learning を成立 | あり |
| VCP-CLIP | 2024 | 工業一般 | CLIP | Visual context prompting | 手作業prompt依存を減らす visual context prompting | あり |
| FabGPT | 2024 | 半導体 | カスタムLMM | Domain-specific assistant | SEM画像の微小欠陥検出と工程QAを同時処理 | 一部あり |
| Customizable-VLM | 2024 | 工業・多モーダル | 汎用VLM | Expert prompting | 参照画像・ルール・専門知識をまとめて条件化 | あり |
| Vision-Language ICL Driven Few-Shot Visual Inspection Model | 2025 | 工業一般 | VLM | In-context learning | few-shot normal/defect reference と説明文で one-shot 検査 | あり |
| MMAD | 2025 | 工業一般 | ベンチマーク | Evaluation | MLLMの工業検査能力を7タスクで体系評価 | あり |
| LogicAD | 2025 | 論理異常 | AVLM + logic reasoner | Explainable logical AD | テキスト特徴抽出と論理推論で説明付きLOCO検査 | あり |
| LogicQA | 2025 | 論理異常・半導体 | Pretrained VLM | Few-shot logical reasoning | 正常例数枚からルール化して論理異常を検出 | 研究コードあり |
| LogSAD | 2025 | 工業一般 | GPT-4V + foundation models | Training-free reasoning | match-of-thoughtで構造異常と論理異常を統合 | あり |
| Bayes-PFL | 2025 | 工業・医療 | CLIP | Prompt distribution learning | prompt空間を分布として学習し unseen category へ汎化 | あり |
| AA-CLIP | 2025 | 工業・医療 | CLIP | Anomaly-aware adapter | anomaly-aware設計でゼロショットADを強化 | あり |
| FE-CLIP | 2025 | 工業・医療 | CLIP | Frequency-aware adapter | 周波数特徴を取り入れ微細欠陥に強化 | あり |
| FAPrompt | 2025 | 工業・医療 | CLIP | Fine-grained prompt learning | defect type に近い細粒度異常プロンプトを学習 | あり |
| EIAD | 2025 | 工業一般 | MLLM | Explainable IAD | DDQAと分離最適化で説明と局在化を両立 | あり |
| Anomaly-OV | 2025 | 工業・医療・3D | Specialist MLLM | Detection + reasoning | Anomaly-Instruct-125k/VisA-D&R とLTFMで reasoning 強化 | あり |
| EMIT | 2025 | 工業一般 | InternVL3-8Bベース | RLHF/GRPO | 難例重視GRPOとsoft promptでIAD適応 | あり |
| AD-FM | 2025/2026 | 工業一般 | 汎用MLLM | Deliberative reasoning | multi-stage reasoning と fine-grained reward | 論文中心 |
| AD-Copilot | 2026 | 工業一般 | Qwen2.5-VL | Visual comparison assistant | 比較エンコーダで fine-grained 差分を見る専門助手 | あり |
| MMR-AD / Anomaly-R1 | 2026 | 一般AD・工業寄り | MLLM | CoT benchmark | general AD を見据えた大規模マルチモーダルベンチマーク | あり |
| M3-AD | 2026 | 工業一般 | MLLM | Reflection-aware | self-correction を明示的に組み込んだ評価枠組み | 予定 |

上の表から読み取れるように、2023〜2024年は CLIP 系が中心で、2025〜2026年は **「専用データセット＋専用MLLM＋推論強化」** が増えています。また、工業そのものに近いのは AnomalyGPT、FabGPT、EIAD、Vision-Language ICL、AD-Copilot で、論理異常に強いのは LogicAD / LogicQA / LogSAD、基盤技術として有力なのは WinCLIP / PromptAD / VCP-CLIP / Bayes-PFL / AA-CLIP / FE-CLIP / FAPrompt です。 citeturn10search0turn1search0turn16search1turn17search1turn1search1turn18search0turn8search0turn1search16turn7search1turn11search0turn2search20turn14search0turn2search9turn8search2turn8search1

## 製造業への適用可能性比較

以下は文献を踏まえた**実務観点の総合評価**です。性能そのものではなく、少量データ、未知欠陥、説明可能性、導入容易性を重視しています。これは複数論文の結果と設計思想から行った整理であり、表の「高・中・低」は厳密なベンチマーク値ではなく、実装判断のための研究者レビューです。 citeturn10search0turn11search0turn1search1turn17search1turn13search1turn18search0turn20search0

| 技術カテゴリ | 少量データ適性 | 未知欠陥適性 | 説明可能性 | 推論コスト | 実装難易度 | 製造現場への即応性 |
|---|---|---|---|---|---|---|
| CLIP系 training-free / zero-shot | 高 | 中〜高 | 低 | 低 | 低 | 高 |
| Prompt learning / adapter | 高 | 中〜高 | 低〜中 | 低〜中 | 中 | 高 |
| In-context visual comparison | 高 | 高 | 中〜高 | 中 | 中 | 高 |
| 専用MLLM assistant | 中 | 中〜高 | 高 | 高 | 高 | 中 |
| 論理推論・rule-based | 中 | 中 | 高 | 中〜高 | 中〜高 | 中 |
| Detector + LLM hybrid | 中 | 中 | 中〜高 | 中 | 中 | 高 |

実務上の含意はかなり明確です。**まず動くものを作る**なら、WinCLIP / PromptAD / VCP-CLIP / Bayes-PFL のような CLIP系で始めるのが良いです。**少量データで未知工具にも転移させたい**なら、Vision-Language ICL や AD-Copilot のような visual comparison / in-context 系が有望です。**説明付きの研究成果を論文化したい**なら、EIAD、Anomaly-OV、AD-FM、EMIT のような reasoning・説明指向が魅力的ですが、データセット設計と計算資源が重くなります。 citeturn10search0turn11search0turn2search20turn14search0turn1search1turn18search0turn17search1turn13search1turn24search11turn19search1

VLMのモデル選択だけを見ると、**CLIP/OpenCLIP は安い・強い・安定**、**BLIP-2 / LLaVA は説明生成の入口として扱いやすい**、**Qwen2-VL / Qwen2.5-VL は高解像度・位置理解・実装資産のバランスが良い**、**GPT-4V/4o 系は汎用能力は高いが工業微細欠陥の専門性はそのままでは不足**、という整理になります。これは一般モデル能力の差というより、工業画像とWeb画像のギャップ、および fine-grained visual comparison の不足に起因します。 citeturn4search0turn4search1turn5search0turn4search2turn18search13turn5search1turn20search0turn13search1

## 研究ギャップと今後の研究方向

最も大きい研究ギャップは、**工具摩耗・超硬インサート・顕微鏡摩耗状態分類にVLMを真正面から適用した研究がほぼ見当たらない**ことです。今回確認できた公開研究は、MVTec/VisA に代表される一般工業欠陥、半導体ウエハ、論理異常、工業QAが中心でした。一方で、工具摩耗の画像解析自体は machine vision や顕微鏡画像ベースで既に研究があり、ボールエンドミルの inline microscope 検出や、デジタル顕微鏡による工具摩耗分類などは存在します。したがって、「従来CVで扱われてきた工具摩耗」を「VLMで少量データ・説明付きへ拡張する」という位置づけが成立します。 citeturn1search0turn1search1turn16search1turn20search0turn21search6turn21search23

第二のギャップは、**微小欠陥・高倍率顕微鏡画像・高解像度局在化**です。多くのMLLMは粗い意味理解には強い一方で、微細な欠け・クラック・摩耗帯の境界のような subtle pattern には弱いことが、Anomaly-OV や MMAD 系の問題設定からも明白です。この点では FE-CLIP の周波数強化、AD-Copilot の比較エンコーダ、Qwen2-VL/Qwen2.5-VL の高解像度処理が参考になりますが、顕微鏡画像向けの体系研究はまだ足りません。 citeturn13search1turn20search0turn8search2turn18search0turn4search2turn18search13

第三のギャップは、**生成される説明の妥当性評価**です。EIAD、Anomaly-OV、LogicAD、AD-FM は説明生成や reasoning を扱いますが、工場で本当に使える説明かどうかをどう評価するかは未成熟です。異常位置の正確さだけでなく、説明が工程知識と整合するか、誤説明で現場をミスリードしないか、根拠画像と説明が対応しているかを評価する必要があります。これは tool wear のように専門用語が明確な領域ほど、逆に研究しやすいテーマでもあります。 citeturn17search1turn13search1turn8search0turn24search11

第四のギャップは、**VLM + Agent / RAG / Knowledge Graph の工業異常検知への本格導入**です。確認できた主要査読論文の中心は、prompt・adapter・instruction tuning・rule reasoning・comparison encoder であり、RAG や明示的 Agent を本格的に組み込んだ工業IADの中核論文はまだ薄いです。逆に言えば、工具摩耗では「過去の類似摩耗事例」「工具寿命基準」「加工条件」「材種情報」「熟練者メモ」を検索する設計がハマりやすく、実務インパクトも高いです。研究としても、比較的取りやすい新規性だと思います。 citeturn24search0turn18search0turn20search5turn20search1

### あなたの研究テーマへの具体提案

あなたの条件に最も合うのは、**一段で全部やる end-to-end MLLM** ではなく、**比較型視覚モジュール + 軽量VLM/MLLM説明器**の二段構成です。第一段で、正常基準画像と対象画像の差分から「クレータ摩耗」「境界摩耗」「チッピング」「その他」を出す比較器を置きます。ここは AD-Copilot の comparison encoder、Vision-Language ICL の reference-based inspection、PromptAD / IIPAD の few-shot 適応思想が参考になります。第二段で、その分類結果と局所ヒートマップ、参照画像差分を Qwen2.5-VL や InternVL 系に入力し、自然言語説明を生成します。この構成なら、視覚性能と説明性能を分離でき、データ不足にも強いです。 citeturn18search0turn1search1turn11search0turn12search0turn18search13

推奨アーキテクチャは次のようになります。画像前処理では同倍率・同姿勢で撮影し、刃先近傍をROI切り出しします。視覚側は OpenCLIP/CLIP あるいは Qwen2.5-VL の視覚バックボーンを使い、正常参照との cross-attention 比較で residual feature を取ります。少量ラベルに対しては PromptAD 風の normal-only prompt learning、もしくは IIPAD 風の shared prompt generator を使い、局在化が必要なら VCP-CLIP や FE-CLIP 的な fine-grained/frequency-aware 改良を取り入れます。説明生成側には、摩耗語彙辞書とルールテンプレートを与え、「どこに」「どの種類の」「どの程度の」摩耗があるかを定型＋自由記述の併用で生成させるのがよいです。 citeturn11search0turn12search0turn2search20turn8search2turn18search13

評価指標は、分類だけなら Accuracy より **Macro-F1、MCC、Balanced Accuracy** を推奨します。摩耗クラスが偏る可能性が高いからです。局在化があるなら IoU または defect-region overlap、説明は専門家評価で「正確性」「根拠との整合」「有用性」を5段階で採点し、可能なら DDQA や VisA-D&R の発想にならって構造化評価を作ると研究の説得力が増します。もし説明評価まで含めるなら、あなたのデータセット自体が論文貢献になります。 citeturn17search1turn13search1turn20search0

今後3〜5年で有望なのは、**顕微鏡工具画像向けの比較型VLM**, **摩耗状態説明付き few-shot benchmark**, **加工条件・材種・切削条件を含めたRAG型異常説明**, **自己反省型説明修正**, **VLM + open-vocabulary detector による摩耗部位自動ラベリング** です。とくに「超硬インサートの顕微鏡画像」「少量ラベル」「自然言語説明」は、公開ベンチマークに対する独自性が強く、テーマ設定として非常に良いです。 citeturn18search0turn20search5turn22search0turn20search1

## おすすめ論文ランキングと参考URL一覧

### おすすめ論文ランキング

以下は、**製造業への近さ、少量データへの有用性、説明可能性、あなたの工具摩耗テーマへの転用しやすさ**を基準にしたランキングです。 citeturn1search1turn18search0turn17search1turn13search1turn11search0

| 順位 | 論文 | 推薦理由 |
|---:|---|---|
| 1 | AD-Copilot | 正常参照との fine-grained visual comparison が、顕微鏡工具画像に最も転用しやすい |
| 2 | Vision-Language In-Context Learning Driven Few-Shot Visual Inspection Model | few-shot 参照画像＋説明文という設計が、そのまま研究プロトタイプになりやすい |
| 3 | PromptAD | 正常画像のみの few-shot 学習という制約が、工具摩耗データ収集と非常に相性が良い |
| 4 | Anomaly-OV | 異常説明と推論を研究として深めるときの最重要参照文献 |
| 5 | EIAD | 工業向け説明付き異常検知の設計と DDQA 発想が参考になる |
| 6 | WinCLIP | CLIPベース few-shot/zero-shot の出発点として必読 |
| 7 | IIPAD | one-for-all few-shot の実運用観点が強い |
| 8 | VCP-CLIP | visual context prompting は微細摩耗部位の局在化改善に応用しやすい |
| 9 | FE-CLIP | 周波数強化は微小欠け・細線状摩耗に相性が良い可能性が高い |
| 10 | Bayes-PFL | unseen category への安定汎化という観点で重要 |
| 11 | AnomalyCLIP | object-agnostic prompt 学習の代表 |
| 12 | AnomalyGPT | 産業IADに説明と対話を持ち込んだ歴史的に重要な論文 |
| 13 | FabGPT | 工程知識・微小欠陥・専門QAを結びつけた半導体分野の好例 |
| 14 | LogSAD | ルールベース推論を取り込みたい場合の重要文献 |
| 15 | LogicAD | 説明可能 logical AD の設計が評価指標づくりにも参考になる |
| 16 | LogicQA | few-shot ルール誘導という発想が現場基準書と相性が良い |
| 17 | EMIT | RL系・難例学習で MLLM を工業IADへ適応する最新潮流 |
| 18 | AD-FM | multi-stage reasoning と fine-grained reward の研究方向を把握できる |
| 19 | Customizable-VLM | 外部知識や専門ルールを prompt 化する設計が工具摩耗向けに有効 |
| 20 | MVFA-AD | 医療だが adapter でドメインシフトを乗り越える手本として有用 |

### 参考URL一覧

以下は、読んでおく価値が高い論文・コード・プロジェクトページの一覧です。URLはコピーしやすいようにコード形式で示しています。

- AnomalyGPT  
  論文: `https://arxiv.org/abs/2308.15366`  
  コード: `https://github.com/CASIA-LMC-Lab/AnomalyGPT`

- WinCLIP  
  論文: `https://arxiv.org/abs/2303.14814`  
  PDF: `https://openaccess.thecvf.com/content/CVPR2023/papers/Jeong_WinCLIP_Zero-Few-Shot_Anomaly_Classification_and_Segmentation_CVPR_2023_paper.pdf`

- AnomalyCLIP  
  論文ページ: `https://openreview.net/forum?id=buC4E91xZE`  
  コード: `https://github.com/zqhang/AnomalyCLIP`

- PromptAD  
  論文: `https://arxiv.org/abs/2404.05231`  
  PDF: `https://openaccess.thecvf.com/content/CVPR2024/papers/Li_PromptAD_Learning_Prompts_with_only_Normal_Samples_for_Few-Shot_Anomaly_CVPR_2024_paper.pdf`  
  コード: `https://github.com/FuNz-0/PromptAD`

- VCP-CLIP  
  PDF: `https://www.ecva.net/papers/eccv_2024/papers_ECCV/papers/08761.pdf`

- Bayes-PFL  
  論文: `https://arxiv.org/abs/2503.10080`  
  コード: `https://github.com/xiaozhen228/Bayes-PFL`

- AA-CLIP  
  PDF: `https://openaccess.thecvf.com/content/CVPR2025/papers/Ma_AA-CLIP_Enhancing_Zero-Shot_Anomaly_Detection_via_Anomaly-Aware_CLIP_CVPR_2025_paper.pdf`

- FE-CLIP  
  PDF: `https://openaccess.thecvf.com/content/ICCV2025/papers/Gong_FE-CLIP_Frequency_Enhanced_CLIP_Model_for_Zero-Shot_Anomaly_Detection_and_ICCV_2025_paper.pdf`

- FAPrompt  
  論文: `https://arxiv.org/abs/2410.10289`  
  PDF: `https://openaccess.thecvf.com/content/ICCV2025/papers/Zhu_Fine-grained_Abnormality_Prompt_Learning_for_Zero-shot_Anomaly_Detection_ICCV_2025_paper.pdf`

- Vision-Language In-Context Learning Driven Few-Shot Visual Inspection Model  
  論文: `https://arxiv.org/abs/2502.09057`  
  コード: `https://github.com/ia-gu/Vision-Language-In-Context-Learning-Driven-Few-Shot-Visual-Inspection-Model`

- FabGPT  
  論文: `https://arxiv.org/abs/2407.10810`  
  DOIページ: `https://dl.acm.org/doi/10.1145/3676536.3676750`

- EIAD  
  論文: `https://arxiv.org/abs/2503.14162`  
  コード: `https://github.com/Solunny/EIAD`

- Anomaly-OV  
  論文: `https://arxiv.org/abs/2502.07601`  
  プロジェクト: `https://xujiacong.github.io/Anomaly-OV/`  
  コード: `https://github.com/honda-research-institute/Anomaly-OneVision`

- LogSAD  
  PDF: `https://openaccess.thecvf.com/content/CVPR2025/papers/Zhang_Towards_Training-free_Anomaly_Detection_with_Vision_and_Language_Foundation_Models_CVPR_2025_paper.pdf`  
  コード: `https://github.com/zhang0jhon/LogSAD`

- LogicAD  
  論文ページ: `https://ojs.aaai.org/index.php/AAAI/article/view/32433`  
  PDF: `https://ojs.aaai.org/index.php/AAAI/article/view/32433/34588`

- LogicQA  
  PDF: `https://aclanthology.org/2025.acl-industry.29.pdf`

- MMAD  
  論文: `https://arxiv.org/abs/2410.09453`  
  コード・データ: `https://github.com/jam-cc/mmad`

- EMIT  
  論文: `https://arxiv.org/abs/2507.21619`  
  コード: `https://github.com/guanwei49/EMIT`

- AD-FM  
  論文: `https://arxiv.org/abs/2508.04175`  
  AAAI PDF: `https://ojs.aaai.org/index.php/AAAI/article/download/38548/42510`

- AD-Copilot  
  論文: `https://arxiv.org/abs/2603.13779`  
  コード: `https://github.com/jam-cc/AD-Copilot`

- MMR-AD  
  論文: `https://arxiv.org/abs/2604.10971`

- M3-AD  
  論文: `https://arxiv.org/abs/2603.00055`

- Customizing Visual-Language Foundation Models for Multi-modal Anomaly Detection and Reasoning  
  論文: `https://arxiv.org/abs/2403.11083`  
  コード: `https://github.com/Xiaohao-Xu/Customizable-VLM`

- MVFA-AD  
  論文: `https://arxiv.org/abs/2403.12570`  
  コード: `https://github.com/MediaBrain-SJTU/MVFA-AD`

- MVTec AD  
  データセット: `https://www.mvtec.com/research-teaching/datasets/mvtec-ad`

- MVTec LOCO AD  
  データセット: `https://www.mvtec.com/research-teaching/datasets/mvtec-loco-ad`

- MVTec 3D-AD  
  データセット: `https://www.mvtec.com/research-teaching/datasets/mvtec-3d-ad`

- VisA  
  データセット: `https://github.com/amazon-science/spot-diff`

- Eyecandies  
  データセット: `https://eyecan-ai.github.io/eyecandies/`

このURL群のうち、あなたの研究にまず直結するのは **AD-Copilot、Vision-Language ICL、PromptAD、Anomaly-OV、EIAD、WinCLIP** です。これらを読むだけでも、**比較型few-shot設計**、**説明生成**、**工業向けデータセット構築**、**評価設計**の骨格をかなり具体化できます。 citeturn18search0turn1search1turn11search0turn13search1turn17search1turn10search0
