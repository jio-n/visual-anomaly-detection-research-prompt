# 生成系VLMとMLLMによる説明可能な異常検知の研究動向

## エグゼクティブサマリー

今回の再調査では、先に整理済みのサーベイ本文とリンク一覧を起点コーパスとして使い、その上で主要論文の公式ページ・arXiv・AAAI・ACL・公式リポジトリを追加確認しました。起点コーパスの段階でも、WinCLIP や PromptAD などの CLIP 系論文が厚く、生成系 MLLM による説明可能異常検知は AnomalyGPT、FabGPT、EIAD、Anomaly-OV、EMIT、AD-FM、AD-Copilot、MMR-AD、M3-AD など十数本規模にとどまっていました。したがって、**Q1への答えは「存在は明確に増えているが、まだ少数派であり、主流は依然として CLIP 系である」**です。fileciteturn0file1 fileciteturn0file0 citeturn0academia1turn0academia2turn2academia3turn1academia0turn2academia1turn1academia2turn4academia0turn6view0

生成系 MLLM 型の利点は、**最終出力を「はい／いいえ」「異常箇所」「理由」「追加確認点」といった自然言語で返せること**にあります。これは CLIP 系の anomaly score や埋め込み距離では得にくい説明性であり、工場現場で必要な「どこが、なぜ、どの欠陥なのか」を直接扱えます。一方で欠点も明確で、MMAD は GPT-4o でさえ平均 74.9% と工業要求には届かないことを示し、Anomaly-OV は GPT-4o を含む汎用 MLLM が fine-grained anomaly reasoning に弱いと報告し、AD-Copilot は一般 Web 画像とのドメインギャップと「画像間比較を言語空間に頼りすぎること」が微小差分への弱さにつながると整理しています。したがって、**Q2 への答えは「説明は圧倒的に強いが、微細差分にはそのままだと弱い」**です。citeturn0academia0turn2academia3turn1academia2turn2academia1

あなたの研究アイデアである「熟練者の観察観点をプロンプト化し、画像上で見るべき部位・異常兆候・理由を言語で返す」は、現在の生成系 IAD の中でもかなり筋が良いです。直接の先行例としては、**Vision-Language In-Context Learning Driven Few-Shot Visual Inspection Model** が「説明文つき参照画像」を検査基準として使い、**Customizing Visual-Language Foundation Models for Multi-modal Anomaly Detection and Reasoning** が expert knowledge を task description・class context・normality rule・reference image として与え、**LogicQA** が自動生成された質問群をチェックリストとして使い、**Reason-IAD** が retrieval-augmented knowledge module でカテゴリ固有記述を注入しています。つまり、**Q3 と Q4 への答えは「ある。ただし prompt 単独より、参照画像・QA・追加モジュールとの併用が多い」**です。citeturn3academia0turn2academia0turn9view1turn7academia3turn10view0

いちばん重要なのは、今回確認した公開の生成系 MLLM 論文群の中に、**超硬インサートのクレータ摩耗・境界摩耗・チッピング・フランク摩耗を直接対象にした研究は見当たらなかった**ことです。他方で、従来 CV では insert wear や tool-wear classification は進んでおり、顕微鏡画像・輪郭特徴・階層分類・SEM／microscope ベースの研究は存在します。したがって、**Q8への答えは「直接一致する論文はまだなく、機構的に最も近いのは Vision-Language ICL、AD-Copilot、FabGPT、EIAD、Customizable-VLM の組み合わせ」**です。これは研究ギャップであると同時に、テーマとしての新規性の源泉でもあります。fileciteturn0file1 fileciteturn0file0 citeturn3academia0turn1academia2turn1academia1turn0academia2turn2academia0turn17academia2turn16academia2turn17academia1

## 生成系MLLM型異常検知の定義とCLIP系との違い

このレポートでいう「生成系 VLM / MLLM」は、内部に視覚エンコーダを持つことを許容しつつも、**最終出力が anomaly score や埋め込み距離ではなく、自然言語の判断文・根拠・QA 応答・説明文であるもの**を指します。典型例は、AnomalyGPT の対話型異常判定、EIAD の defect QA と局在化、Anomaly-OV の anomaly reasoning、AD-Copilot の視覚比較にもとづく assistant、M3-AD の reflection-aware decision revision です。逆に、CLIP 系の zero-shot anomaly detection は、画像とテキストを同じ表現空間に写像して類似度で判定するため、説明性は後付けになりやすく、本調査では比較対象にとどめました。citeturn0academia1turn0academia2turn2academia3turn1academia2turn6view0

この違いは、研究課題をどう定式化するかに直結します。CLIP 系は「正常／異常」や defect prompt と画像埋め込みの距離を測るため、**未知カテゴリ・少量ラベル・低コスト導入**に強い一方で、「なぜ異常なのか」「どこを見たのか」を業務的に使える文として返す設計には弱いです。これに対して、生成系 MLLM は **Yes/No、部位説明、理由、欠陥種別、追加確認項目**を一つのインターフェースで返せるので、現場教育・検査支援・報告書自動化に向きます。ただし MMAD が示すように、汎用 MLLM の素の性能はまだ工場水準に満たず、Anomaly-OV や AD-Copilot が示すように fine-grained detail への感度不足が残っています。citeturn0academia0turn2academia3turn1academia2turn2academia1

この意味で、生成系 MLLM 型異常検知は現状で三つに分かれます。第一は **専用データを作って end-to-end に assistant 化する流派**で、AnomalyGPT、EIAD、Anomaly-OV、EMIT、AD-FM、AD-Copilot、M3-AD がここに入ります。第二は **prompt・reference image・checklist を中心にする軽量流派**で、Vision-Language ICL、Customizable-VLM、LogSAD、LogicQA が代表です。第三は **知識注入や RAG・RL・reflection を強化する新しい流派**で、FabGPT、Reason-IAD、AnomalyR1、IAD-R1、LAD-Reasoner、DifferAD-R1 が該当します。あなたの研究は、第二の流派を起点にしつつ、第三の知識注入を取り込むのが最も自然です。citeturn3academia0turn2academia0turn15academia0turn9view1turn1academia1turn7academia3turn4academia1turn4academia2turn11academia2turn4academia3

## 主要研究の比較

以下の表は、**生成系 MLLM が自然言語で異常判定・説明を返すか**を軸に、今回の主対象論文を比較したものです。各行の内容は行頭の論文ソースに対応しています。citeturn0academia1turn0academia2turn2academia3turn1academia1turn3academia0turn15academia0turn1academia0turn2academia1turn1academia2turn4academia0turn6view0turn2academia0turn9view0turn9view1turn7academia3

| タイトル | 年・URL | 対象ドメイン / タスク | 使用モデル | 出力形式 | Yes/No | 説明 | 異常箇所 | 欠陥種別 | 熟練者知識・プロンプト | fine-tuning / 追加モジュール | 強み | 弱み | 工具摩耗への転用 | 適合度 |
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---:|
| **AnomalyGPT** citeturn0academia1 | 2023, `https://arxiv.org/abs/2308.15366` | 工業 IAD / 検知・局在化・対話 | LVLM ベース | 対話文、異常有無、位置説明 | あり | あり | あり | 一部あり | プロンプト学習と異常記述付き合成データ | fine-tune あり、image decoder / prompt learner | 初期の本格的 explainable IAD assistant | 専用学習が必要。微細欠陥は補助モジュール頼み | 中。説明UIの参考として重要 | 4 |
| **FabGPT** citeturn1academia1 | 2024, `https://arxiv.org/abs/2407.10810` | 半導体 SEM / 欠陥検出・根本原因・QA | 独自 LMM | QA、説明文、工程知識応答 | あり | あり | あり | あり | interactive corpus training と defect knowledge 埋め込み | modulation module あり | 微小欠陥と専門知識QAが近い | 半導体特化で公開評価が限定的 | 高。専門知識埋め込みの手本 | 5 |
| **Customizing Visual-Language Foundation Models for Multi-modal Anomaly Detection and Reasoning** citeturn2academia0 | 2024, `https://arxiv.org/abs/2403.11083` | 工業・時系列・点群 / 異常検知と理由付け | 汎用 VLM | anomaly reasoning 文 | あり | あり | 条件付き | 一部あり | task description, class context, normality rules, reference images | 主体は prompting、追加表現統合あり | expert knowledge prompting を正面から扱う | 定量評価は初期的。実装詳細は軽量だが洗練前 | 高。熟練者観点の形式知化に直結 | 5 |
| **Vision-Language In-Context Learning Driven Few-Shot Visual Inspection Model** citeturn3academia0 | 2025, `https://arxiv.org/abs/2502.09057` | 工業一般 / few-shot visual inspection | VLM | unified formatted output text | あり | あり | 条件付き | 条件付き | 参照画像 + explanatory texts を inspection criteria として投入 | 学習あり、新製品には ICL | あなたの「説明文つき検査基準」に最も近い | 局在化や長い reasoning は限定的 | 非常に高い。超硬インサートの few-shot 検査に最有力 | 5 |
| **EIAD** citeturn0academia2 | 2025, `https://arxiv.org/abs/2503.14162` | 工業一般 / explainable IAD | MLLM + localization module | defect QA、説明、局在化 | あり | あり | あり | あり | DDQA による信頼性の高い defect QA | fine-tune あり、欠陥局在化モジュールあり | 人手品質の DDQA が強い | end-to-end ではなく専用局在化が必要 | 高。説明評価設計に有用 | 4 |
| **Towards Zero-Shot Anomaly Detection and Reasoning with Multimodal Large Language Models** / **Anomaly-OV** citeturn2academia3 | 2025, `https://arxiv.org/abs/2502.07601` | 工業・医療・3D / ZSAD + reasoning | 専用 MLLM | 異常検出 + 詳細説明 | あり | あり | あり | あり | Anomaly-Instruct-125k と VisA-D&R | LTFM あり、specialist tuning あり | 汎用 MLLM の弱点を明示し specialist 化 | 構成は重い | 高。fine-grained reasoning の中核文献 | 5 |
| **Towards Training-free Anomaly Detection with Vision and Language Foundation Models** / **LogSAD** citeturn15academia0 | 2025, `https://arxiv.org/abs/2503.18325` | 工業一般 / logical + structural AD | GPT-4V + foundation models | match-of-thought、提案、最終判断 | あり | あり | 条件付き | 一部あり | compositional rules of thought を LMM が生成 | training-free、calibration / multi-granularity detectors | prompt / rule 主体で動く | 検出器統合を含むため純粋 MLLM 単体ではない | 中〜高。観察ルールの言語化に有効 | 4 |
| **LogicQA** citeturn9view1 | 2025, `https://aclanthology.org/2025.acl-industry.29/` | 論理異常・SEM / checklist reasoning | VLM | 質問リストへの回答、説明 | あり | あり | 間接的 | なし | 自動生成質問を checklist 化 | training-free / annotation-free / few-shot | checklist 発想が現場向き | 表面摩耗より論理異常向き | 中。観察チェックリスト設計に直結 | 4 |
| **EMIT** citeturn1academia0 | 2025, `https://arxiv.org/abs/2507.21619` | 工業一般 / MLLM 適応 | InternVL3-8B ベース | QA / 判定文 | あり | あり | あり | 一部あり | GPT 生成 object description と few-shot prompt | GRPO、soft prompt、heatmap-guided contrastive embedding | 難例学習と MLLM 強化 | 設計が重く prompt-only ではない | 中。高性能化の後段として有効 | 4 |
| **AD-FM** citeturn2academia1 | 2025, `https://arxiv.org/abs/2508.04175` | 工業一般 / anomaly reasoning | 汎用 MLLM | multi-stage reasoning text | あり | あり | あり | 一部あり | region identification → focused examination の段階推論 | fine-grained reward、GRPO 系 | 観察手順をモデルに踏ませる点が非常に近い | 実装と学習が重い | 高。熟練者手順の言語化と相性が良い | 5 |
| **AD-Copilot** citeturn1academia2 | 2026, `https://arxiv.org/abs/2603.13779` | 工業一般 / visual comparison assistant | Qwen2.5-VL ベース | 判定文、位置、比較にもとづく説明 | あり | あり | あり | 一部あり | inspection knowledge を Chat-AD に抽出 | Comparison Encoder、multi-stage training | 微細差分に強い。人間検査行動に近い | 比較エンコーダが必要 | 非常に高い。正常品との差で摩耗を見るのに最適 | 5 |
| **MMR-AD / Anomaly-R1** citeturn4academia0turn4academia1 | 2025–2026, `https://arxiv.org/abs/2604.10971` / `https://arxiv.org/abs/2504.11914` | 一般 AD / reasoning benchmark | MLLM + RL | CoT、判定、mask | あり | あり | あり | 一部あり | CoT データと RL | GRPO / ROAM | reasoning 強化の最新潮流 | 工業固有知識は別途必要 | 中。将来拡張向き | 4 |
| **M3-AD** citeturn6view0 | 2026, `https://arxiv.org/abs/2603.00055` | 工業一般 / reflection-aware AD | MLLM | 初期判断 + self-correction | あり | あり | 一部あり | 一部あり | reflection-aware correction | RA-Monitor | 高信頼化の方向性が明確 | まだ新しく検証幅が限られる | 中〜高。誤判定訂正機構として有望 | 4 |
| **Reason-IAD** citeturn7academia3 | 2026, `https://arxiv.org/abs/2602.09850` | 工業一般 / explainable IAD | MLLM + knowledge module | reasoning text | あり | あり | あり | 一部あり | retrieval-augmented knowledge + category text | latent reasoning、dynamic visual injection | 知識検索を明示的に組み込む | 新規で再現性は今後 | 非常に高い。熟練者メモや基準書の RAG 化に近い | 5 |

この比較から見える事実は三つです。第一に、**純粋な prompt-only の成功例は少なく、多くの高性能法は reference image、localization module、comparison encoder、RL、または defect-specific dataset を併用しています**。第二に、**自然言語出力はすでに一般化しつつあるが、JSON のような厳密スキーマはまだ標準ではなく、free-form QA・checklist・multi-turn dialogue が主流**です。第三に、**あなたの研究目的に最も近いのは「説明文つき参照画像」を使う Vision-Language ICL と、「細粒度差分比較」を前面に出す AD-Copilot の折衷**です。citeturn3academia0turn1academia2turn2academia0turn0academia2turn9view1turn2academia1turn7academia3

## プロンプト知識注入とVQAと構造化出力

熟練者知識をプロンプトに入れる方向については、**完全に「プロンプトだけ」で性能向上を主張する論文は多くないものの、観察観点やルール文を入力条件にする研究は確実に存在します**。もっとも直接的なのは Customizable-VLM で、task descriptions、class context、normality rules、reference images を multi-modal prompt として統合しています。Vision-Language ICL も explanatory text を inspection criteria に使っており、MMAD の公開リポジトリは experts と LLM の支援で各カテゴリの normal features、anomaly classifications、detailed descriptions を `domain_knowledge.json` として整理しています。これは、**「異常検知の前提知識をテキストで持たせる」こと自体はすでに妥当な設計として認識されている**ことを意味します。citeturn2academia0turn3academia0turn10view0

VQA 定式化については、AnomalyGPT が multi-turn dialogue を前面に出し、EIAD が DDQA という defect detection question answering データセットを構築し、FabGPT が root cause analysis と expert Q&A を一体化し、LogicQA が質問群を checklist として束ね、MMAD が 7 つの industrial inspection subtasks にまたがる 39,672 問のベンチマークを整備しています。したがって、**Q4 への答えは明確に「ある」であり、しかも QA 化は現在の生成系 IAD の中心的な設計の一つ**です。特にあなたのテーマでは、「この画像に異常はあるか」「どの部位か」「クレータ摩耗か境界摩耗か」「その根拠は何か」という一連の質問列は、既存研究の流れに完全に乗っています。citeturn0academia1turn0academia2turn1academia1turn9view1turn0academia0

構造化出力については、**論文で標準化された JSON schema はまだほぼ見当たりません**。ここは事実というより、今回確認した論文群からの整理です。AnomalyGPT は対話文、EIAD は defect QA と局在化、LogicQA は checklist answers、MMAD は multiple-choice benchmark、AD-Copilot や AnomalyR1 は localization まで含む reasoning output を扱いますが、提示されたような `{"is_anomaly": "...", "observed_region": "...", ...}` を共通形式として採用している論文は確認できませんでした。したがって、**Q5 への答えは「構造化出力の萌芽はあるが、厳密なスキーマ設計はまだ研究余地が大きい」**です。これは、そのまま研究貢献になり得ます。citeturn0academia1turn0academia2turn9view1turn0academia0turn1academia2turn4academia1

微小欠陥・顕微鏡画像への弱さについては、根拠がかなり揃っています。MMAD は商用モデルを含めた包括評価で industrial requirement 未達を示し、Anomaly-OV は GPT-4o が fine-grained anomalous details を正確に検出・記述できないと明記し、AD-Copilot は「各画像を独立に符号化し、画像比較を言語空間に頼る」設計では subtle visual difference に鈍感だと述べています。AD-FM はその対策として region identification から focused examination へ進む multi-stage reasoning を導入し、EMIT は heatmap-guided patch comparison と difficulty-aware GRPO を使っています。よって **Q6 と Q7 への答えは、「そのままでは弱い。対策として reference image、ROI、比較エンコーダ、heatmap、multi-stage reasoning、knowledge retrieval が使われている」**です。citeturn0academia0turn2academia3turn1academia2turn2academia1turn1academia0turn7academia3

あなたのアイデアに直接効く設計要素を、既存研究との対応でまとめると次のようになります。これは複数研究を踏まえた**設計指針としての整理**です。citeturn2academia0turn3academia0turn9view1turn2academia1turn1academia2turn7academia3

| 設計要素 | 既存研究での対応 | 何が示されたか | 超硬インサートへの使い方 |
|---|---|---|---|
| 熟練者知識をテキストで注入 | Customizable-VLM, MMAD domain knowledge, FabGPT, Reason-IAD | normality rule や category-specific knowledge は有効な条件入力になりうる | 「すくい面」「逃げ面」「切れ刃境界」「欠損」「摩耗帯」「溶着」などの語彙辞書を与える |
| 説明文つき few-shot 参照 | Vision-Language ICL | explanatory text は inspection criteria として機能する | 「クレータ摩耗のときはすくい面中央〜刃先寄りの凹みを見る」などの観察文を few-shot exemplar として与える |
| チェックリスト化 | LogicQA | 自動質問群は論理 violations の説明に効く | 「刃先の欠けが局所か連続か」「摩耗帯が深さ方向に沿うか」を checklist 化する |
| 段階的観察 | AD-FM | region identification → focused examination が有効 | まず部位同定、次に摩耗兆候列挙、最後に摩耗種別判定へ分ける |
| 正常参照との比較 | AD-Copilot | subtle difference には visual in-context comparison が効く | 新品または許容摩耗サンプルと比較して判定する |
| RAG / 知識検索 | Reason-IAD | category-specific knowledge retrieval が有効 | 工具メーカー基準、寿命基準、熟練者メモを検索してプロンプトに差し込む |

## 超硬インサート摩耗分類への応用可能性と実験設計

今回確認した公開論文群の中で、**超硬インサートのクレータ摩耗・境界摩耗・チッピング・フランク摩耗を生成系 MLLM で説明付きに扱った論文は確認できませんでした**。これは「存在しない」と断言する意味ではなく、今回の文献コーパスで検証できた範囲では未発見という意味です。ただし、周辺の tool wear 研究そのものは、顕微鏡画像、輪郭特徴、深層学習、階層分類、SEM 画像など多様に存在しています。したがって、これは**先行研究がないから危険**なのではなく、**従来 CV の tool wear と生成系 MLLM の explainable IAD がまだ接続されていない**と読むのが妥当です。fileciteturn0file1 fileciteturn0file0 citeturn17academia2turn16academia2turn17academia1turn16academia1

単一論文として最も近いのは、**Vision-Language In-Context Learning Driven Few-Shot Visual Inspection Model** です。理由は、あなたの研究が「少量データ」「参照画像」「説明文」「新しい対象への転用」を重視しているからです。いっぽう、視覚メカニズムとして最も近いのは **AD-Copilot** で、こちらは fine-grained visual comparison が中心です。専門知識注入の観点では **FabGPT** と **Customizable-VLM** が近く、説明可能性のデータセット設計では **EIAD** が近いです。したがって、**Q8 への最終回答は「最も近い単一論文は Vision-Language ICL、最も近い視覚機構は AD-Copilot、最も近い知識設計は FabGPT / Customizable-VLM、最も近い評価設計は EIAD」**です。citeturn3academia0turn1academia2turn1academia1turn2academia0turn0academia2

実験設計としては、まず **Qwen2.5-VL** のような grounding と dynamic resolution に強い open-weight 系をベースにし、入出力を明示的に構造化するのが最も現実的です。Qwen2.5-VL は動的解像度処理、正確な object localization、structured extraction を強みとしており、画像サイズや ROI の変化に強い素地があります。その上で、入力には **対象画像 + 正常参照画像 + 熟練者観点プロンプト + 欠陥語彙辞書** を与え、出力は `is_anomaly`、`wear_type`、`observed_region`、`abnormal_findings`、`reason`、`additional_check_points` に固定します。論文としては、この**構造化出力スキーマ自体が新規性**になります。citeturn8academia0turn3academia0turn1academia2turn2academia0

推奨する最小実験は三段階です。**第一段階**では prompt-only で、Vision-Language ICL 的に「正常画像 1〜3 枚 + 観察説明文」を与え、Yes/No と wear type を出させます。**第二段階**では AD-Copilot 的な差分比較を模倣し、対象画像と正常参照画像のペア入力を増やします。**第三段階**では RAG を足し、Reason-IAD のように工具種別・被削材・切削条件・許容摩耗基準を取得してプロンプトへ注入します。もし性能が足りなければ、最後に AD-FM 型の multi-stage reasoning か、小規模 SFT を追加するのが順序として自然です。最初から重い end-to-end 学習に行く必要はありません。citeturn3academia0turn1academia2turn7academia3turn2academia1

評価指標は、分類性能だけなら Macro-F1、Balanced Accuracy、MCC を推奨します。摩耗クラスが不均衡になりやすいからです。説明性は、EIAD や LogicQA の発想を借りて、**正確性、部位妥当性、理由妥当性、追加確認点の有用性**を専門家 3 名以上で採点するのがよいです。さらに「熟練者観点との一致率」を独自指標にすると、あなたの研究の独自性が明確になります。これは既存の MMAD や DDQA がまだ十分に扱っていない評価軸であり、研究として十分に立ちます。citeturn0academia2turn9view1turn0academia0

## 推薦論文と参考URL

最初に読むべき 5 本は、**Vision-Language In-Context Learning Driven Few-Shot Visual Inspection Model**、**AD-Copilot**、**Customizing Visual-Language Foundation Models for Multi-modal Anomaly Detection and Reasoning**、**FabGPT**、**EIAD** です。理由は明確で、順に **few-shot 参照 + 説明文**、**細粒度差分比較**、**熟練者知識 prompt**、**専門ドメイン知識埋め込み**、**説明付きデータセットと評価設計**を学べるからです。研究の順番としては、Vision-Language ICL で最小構成を理解し、AD-Copilot で微小差分対策を学び、Customizable-VLM と FabGPT で知識注入を設計し、EIAD で explainability 評価を固めるのがよいです。citeturn3academia0turn1academia2turn2academia0turn1academia1turn0academia2

より広く読むなら、第二群として **Anomaly-OV**、**AD-FM**、**Reason-IAD**、**LogSAD**、**LogicQA** を勧めます。Anomaly-OV は「汎用 MLLM が fine-grained anomaly reasoning に弱い」という問題設定を最もはっきり示し、AD-FM は観察手順の段階化、Reason-IAD は RAG と latent reasoning、LogSAD は training-free での観察ルール化、LogicQA は checklist 設計の参考になります。これらは、あなたが最終的に目指している「熟練者観点の形式知化」に直結します。citeturn2academia3turn2academia1turn7academia3turn15academia0turn9view1

参考 URL は以下です。生の URL を管理しやすいようにコード形式でまとめます。

| タイトル | 論文URL | 補助URL |
|---|---|---|
| AnomalyGPT | `https://arxiv.org/abs/2308.15366` | `https://github.com/CASIA-LMC-Lab/AnomalyGPT` |
| FabGPT | `https://arxiv.org/abs/2407.10810` | `https://dl.acm.org/doi/10.1145/3676536.3676750` |
| Customizing Visual-Language Foundation Models for Multi-modal Anomaly Detection and Reasoning | `https://arxiv.org/abs/2403.11083` | `https://github.com/Xiaohao-Xu/Customizable-VLM` |
| Vision-Language In-Context Learning Driven Few-Shot Visual Inspection Model | `https://arxiv.org/abs/2502.09057` | `https://github.com/ia-gu/Vision-Language-In-Context-Learning-Driven-Few-Shot-Visual-Inspection-Model` |
| EIAD | `https://arxiv.org/abs/2503.14162` | `https://github.com/Solunny/EIAD` |
| Anomaly-OV | `https://arxiv.org/abs/2502.07601` | `https://xujiacong.github.io/Anomaly-OV/` |
| LogSAD | `https://arxiv.org/abs/2503.18325` | `https://github.com/zhang0jhon/LogSAD` |
| LogicQA | `https://aclanthology.org/2025.acl-industry.29/` | `https://aclanthology.org/2025.acl-industry.29.pdf` |
| LogicAD | `https://ojs.aaai.org/index.php/AAAI/article/view/32433` | `https://doi.org/10.1609/aaai.v39i4.32433` |
| MMAD | `https://arxiv.org/abs/2410.09453` | `https://github.com/jam-cc/mmad` |
| EMIT | `https://arxiv.org/abs/2507.21619` | `https://github.com/guanwei49/EMIT` |
| AD-FM | `https://arxiv.org/abs/2508.04175` |  |
| AD-Copilot | `https://arxiv.org/abs/2603.13779` | `https://github.com/jam-cc/AD-Copilot` |
| MMR-AD | `https://arxiv.org/abs/2604.10971` |  |
| M3-AD | `https://arxiv.org/abs/2603.00055` |  |
| Reason-IAD | `https://arxiv.org/abs/2602.09850` |  |
| AnomalyR1 | `https://arxiv.org/abs/2504.11914` |  |
| IAD-R1 | `https://arxiv.org/abs/2508.09178` |  |
| MVTec AD | `https://www.mvtec.com/research-teaching/datasets/mvtec-ad` |  |
| MVTec LOCO AD | `https://www.mvtec.com/research-teaching/datasets/mvtec-loco-ad` |  |

最終結論を一文でまとめると、**生成系 MLLM による説明可能な異常検知は、研究としては立ち上がっているが、まだ CLIP 系ほど成熟していない。だからこそ、「超硬インサート顕微鏡画像」「熟練者観点のプロンプト」「Yes/No + 理由 + 観察部位 + 追加確認点の構造化出力」を一体化した研究は、新規性と実用性の両方を狙えるテーマである**と言えます。fileciteturn0file1 fileciteturn0file0 citeturn3academia0turn1academia2turn2academia0turn0academia2turn7academia3
