# manual_v4_Atomic_Data
以下は、ご指定のiiRDS定義およびチャンク化ルールに基づいて抽出・構造化されたアノテーションデータです。

```json
[
  {
    "Title": "メンテナンスの概要と推奨交換時期",
    "Content": "スマート・ポンプ SP-Xシリーズ（SP-X100およびSP-X200）において、フィルターエレメントは製品の性能を維持するための最も重要な部品です。フィルターが目詰まりを起こすと、吐出圧力の低下やモーターへの過負荷が発生する可能性があります。\n\n推奨される交換時期は、累積稼働時間が500時間に達した時点、または差圧計の表示が0.2MPaを超えた時点のいずれか早い方です。定期的な交換により、ポンプの寿命を延ばし、突発的な故障を防ぐことができます。",
    "TopicType": "iirds:GenericConcept",
    "InformationSubject": [],
    "ProductVariant": [
      "ex:SP-X100",
      "ex:SP-X200"
    ],
    "RelatedEntities": [
      "フィルターエレメント",
      "モーター",
      "差圧計"
    ],
    "Confidence": 95,
    "Reasoning": "手順ではなく背景情報や基本原則を提供するトピックであるため、TopicTypeは`iirds:GenericConcept`に該当します。indicatorsの「Features: Definitions, architecture overviews, relationships, theory」や「Question: 'Why...?'」に合致し、なぜ交換が必要なのか（目詰まりによる影響）を説明しています。"
  },
  {
    "Title": "安全上のご注意（共通：感電および残留圧力の危険）",
    "Content": "警告\n\n- 感電の危険: 作業を始める前に、必ず主電源を切り、電源プラグをコンセントから抜いてください。\n- 残留圧力: ポンプ内部には高圧が残留している場合があります。ドレンバルブを開放し、圧力が完全に抜けたことを確認してから作業を行ってください。",
    "TopicType": "iirds:GenericConcept",
    "InformationSubject": [
      "iirds:GenericSafety"
    ],
    "ProductVariant": [
      "ex:SP-X100",
      "ex:SP-X200"
    ],
    "RelatedEntities": [
      "主電源",
      "電源プラグ",
      "ドレンバルブ"
    ],
    "Confidence": 100,
    "Reasoning": "安全に関する警告を含んでいるため、InformationSubjectは`iirds:GenericSafety`を選択しました。indicatorsの「Features: Signal words (DANGER, WARNING)」に合致します。特定の手順ではなく前提となる安全概念のため、TopicTypeは`iirds:GenericConcept`としています。"
  },
  {
    "Title": "安全上のご注意：化学熱傷の危険 (SP-X200専用)",
    "Content": "注意（SP-X200のみ）\n\n- 化学熱傷の危険: 耐薬品モデル（SP-X200）を使用している場合、内部に危険な薬液が残っている可能性があります。必ず耐薬品手袋と保護メガネを着用し、皮膚への付着を防いでください。",
    "TopicType": "iirds:GenericConcept",
    "InformationSubject": [
      "iirds:GenericSafety"
    ],
    "ProductVariant": [
      "ex:SP-X200"
    ],
    "RelatedEntities": [
      "耐薬品手袋",
      "保護メガネ",
      "薬液"
    ],
    "Confidence": 100,
    "Reasoning": "SP-X200固有の安全情報であるため、チャンク化ルールに従い独立したトピックに分割しました。indicatorsの「Features: Signal words (DANGER, WARNING), PPE requirements.」に完全に合致するため、InformationSubjectは`iirds:GenericSafety`です。"
  },
  {
    "Title": "準備するもの：交換に必要な工具と部品 (共通)",
    "Content": "作業には以下の工具と交換部品が必要です。作業前に準備してください。\n\n- Oリング: OR-S25 (新品に交換してください)\n- 六角レンチ: 5mm (ハウジング固定用)\n- トルクレンチ: 設定範囲 10-20 N・m (締め付け管理用)",
    "TopicType": "iirds:GenericReference",
    "InformationSubject": [],
    "ProductVariant": [
      "ex:SP-X100",
      "ex:SP-X200"
    ],
    "RelatedEntities": [
      "Oリング (OR-S25)",
      "六角レンチ",
      "トルクレンチ"
    ],
    "Confidence": 90,
    "Reasoning": "参照用のパラメータや一覧表を提供するTopicTypeである`iirds:GenericReference`に該当します。indicatorsの「Features: Tables, parameter lists」に合致します。共通の工具・部品のみを抽出しています。"
  },
  {
    "Title": "準備するもの：交換用フィルター (SP-X100専用)",
    "Content": "作業には以下の交換部品が必要です。作業前に準備してください。\n\n- 交換用フィルター: FLT-X100 (標準)",
    "TopicType": "iirds:GenericReference",
    "InformationSubject": [],
    "ProductVariant": [
      "ex:SP-X100"
    ],
    "RelatedEntities": [
      "交換用フィルター (FLT-X100)"
    ],
    "Confidence": 95,
    "Reasoning": "バリアント固有の部品リストであるため分割しました。`iirds:GenericReference`の「Features: Tables, parameter lists」に合致します。"
  },
  {
    "Title": "準備するもの：交換用フィルターおよび専用工具 (SP-X200専用)",
    "Content": "作業には以下の工具と交換部品が必要です。作業前に準備してください。\n\n- 交換用フィルター: FLT-X200 (耐薬品)\n- セラミック製スパナ: SP-TOOL-01 (SP-X200のみ必要)",
    "TopicType": "iirds:GenericReference",
    "InformationSubject": [],
    "ProductVariant": [
      "ex:SP-X200"
    ],
    "RelatedEntities": [
      "交換用フィルター (FLT-X200)",
      "セラミック製スパナ (SP-TOOL-01)"
    ],
    "Confidence": 95,
    "Reasoning": "SP-X200固有の部品および専用工具のリストであるため、独立したチャンクに切り出しました。"
  },
  {
    "Title": "交換手順：1. ハウジングの取り外し",
    "Content": "5mmの六角レンチを使用して、フィルターハウジング下部の4本のボルトを緩めます。ボルトを完全に取り外し、ハウジングをゆっくりと引き抜いてください。内部の液体がこぼれる場合があるため、受け皿を用意してください。",
    "TopicType": "iirds:GenericTask",
    "InformationSubject": [],
    "ProductVariant": [
      "ex:SP-X100",
      "ex:SP-X200"
    ],
    "RelatedEntities": [
      "六角レンチ",
      "フィルターハウジング",
      "ボルト",
      "受け皿"
    ],
    "Confidence": 100,
    "Reasoning": "「How do I...?」に対する手順を示すTopicTypeである`iirds:GenericTask`に該当します。indicatorsの「Features: Imperative verbs, step-by-step instructions」に合致します。"
  },
  {
    "Title": "交換手順：2. 旧フィルターの除去 (SP-X100専用)",
    "Content": "使用済みのフィルターエレメントを反時計回りに回して取り外します。\nそのまま手で引き抜いてください。",
    "TopicType": "iirds:GenericTask",
    "InformationSubject": [],
    "ProductVariant": [
      "ex:SP-X100"
    ],
    "RelatedEntities": [
      "フィルターエレメント"
    ],
    "Confidence": 100,
    "Reasoning": "SP-X100固有の手順（手で引き抜く）であるため独立したトピックとして分割しました。TopicTypeは手順を示す`iirds:GenericTask`です。"
  },
  {
    "Title": "交換手順：2. 旧フィルターの除去 (SP-X200専用)",
    "Content": "使用済みのフィルターエレメントを反時計回りに回して取り外します。\nフィルターが固着している場合があります。専用のセラミック製スパナ（SP-TOOL-01）を使用して、慎重に緩めてください。",
    "TopicType": "iirds:GenericTask",
    "InformationSubject": [],
    "ProductVariant": [
      "ex:SP-X200"
    ],
    "RelatedEntities": [
      "フィルターエレメント",
      "セラミック製スパナ (SP-TOOL-01)"
    ],
    "Confidence": 100,
    "Reasoning": "SP-X200固有の手順（専用工具の使用）が含まれるためチャンクを分割しました。手順を示すためTopicTypeは`iirds:GenericTask`です。"
  },
  {
    "Title": "交換手順：3. 清掃とOリング交換",
    "Content": "ハウジング内部を清潔なウエスで拭き取ります。古いOリングを取り外し、新しいOリング（OR-S25）にシリコングリスを薄く塗布してから溝に装着してください。",
    "TopicType": "iirds:GenericTask",
    "InformationSubject": [],
    "ProductVariant": [
      "ex:SP-X100",
      "ex:SP-X200"
    ],
    "RelatedEntities": [
      "ハウジング",
      "ウエス",
      "Oリング (OR-S25)",
      "シリコングリス"
    ],
    "Confidence": 100,
    "Reasoning": "具体的な手順（拭き取る、取り外す、塗布する）を含み、`iirds:GenericTask`のindicatorsに合致します。"
  },
  {
    "Title": "交換手順：4. 新フィルターの取り付け",
    "Content": "新しいフィルターエレメントを装着します。確実に奥まで差し込まれていることを確認してください。",
    "TopicType": "iirds:GenericTask",
    "InformationSubject": [],
    "ProductVariant": [
      "ex:SP-X100",
      "ex:SP-X200"
    ],
    "RelatedEntities": [
      "フィルターエレメント"
    ],
    "Confidence": 100,
    "Reasoning": "手順を示すTopicTypeである`iirds:GenericTask`に該当します。具体的なアクションを示しています。"
  },
  {
    "Title": "交換手順：5. 組み立てと締め付け",
    "Content": "ハウジングを元の位置に戻し、ボルトを手で仮締めします。その後、トルクレンチを使用して 15 N・m のトルクで対角線上に本締めを行ってください。締め付けトルクが不足すると液漏れの原因となり、過大すぎると破損の原因となります。",
    "TopicType": "iirds:GenericTask",
    "InformationSubject": [],
    "ProductVariant": [
      "ex:SP-X100",
      "ex:SP-X200"
    ],
    "RelatedEntities": [
      "ハウジング",
      "ボルト",
      "トルクレンチ"
    ],
    "Confidence": 100,
    "Reasoning": "具体的な操作手順を示すため`iirds:GenericTask`に該当します。トルク値の指定など、作業における明確な指示を含んでいます。"
  },
  {
    "Title": "廃棄について (共通)",
    "Content": "取り外した使用済みフィルターおよびOリングは、産業廃棄物として処理する必要があります。",
    "TopicType": "iirds:GenericConcept",
    "InformationSubject": [],
    "ProductVariant": [
      "ex:SP-X100",
      "ex:SP-X200"
    ],
    "RelatedEntities": [
      "フィルター",
      "Oリング"
    ],
    "Confidence": 85,
    "Reasoning": "具体的な作業手順ではなく廃棄に関する原則や一般的なルールの説明であるため、TopicTypeは`iirds:GenericConcept`を選択しました。"
  },
  {
    "Title": "廃棄について：特別管理産業廃棄物としての処理 (SP-X200専用)",
    "Content": "特に SP-X200（耐薬品モデル） で使用したフィルターには有害な化学物質が付着している可能性があります。必ず密閉袋に入れ、お客様の地域の環境規制および社内規定に従って、特別管理産業廃棄物として適切に廃棄してください。一般ゴミとして捨てないでください。",
    "TopicType": "iirds:GenericConcept",
    "InformationSubject": [
      "iirds:GenericConformity",
      "iirds:GenericSafety"
    ],
    "ProductVariant": [
      "ex:SP-X200"
    ],
    "RelatedEntities": [
      "フィルター",
      "密閉袋"
    ],
    "Confidence": 90,
    "Reasoning": "SP-X200固有の廃棄ルールのため分割しました。地域の環境規制や社内規定（コンプライアンス）への従属を言及しているため、InformationSubjectとして`iirds:GenericConformity`を付与し、有害物質に関する警告を含むため`iirds:GenericSafety`も追加しています。"
  },
  {
    "Title": "主な仕様 (SP-X100)",
    "Content": "項目: SP-X100 (標準)\n- フィルターろ過精度: 10 µm\n- 最大使用圧力: 1.0 MPa\n- 許容液体温度: 0 ~ 60℃\n- 本体材質: SUS304",
    "TopicType": "iirds:GenericReference",
    "InformationSubject": [
      "iirds:GenericTechnicalData"
    ],
    "ProductVariant": [
      "ex:SP-X100"
    ],
    "RelatedEntities": [],
    "Confidence": 100,
    "Reasoning": "仕様（定量・定性データ）のリストであるため、TopicTypeは`iirds:GenericReference`、InformationSubjectは`iirds:GenericTechnicalData`（indicators: Dimensions, performance metrics, units of measurement）を選択しました。バリアント分離のルールに則り、SP-X100の列を独立化しています。"
  },
  {
    "Title": "主な仕様 (SP-X200)",
    "Content": "項目: SP-X200 (耐薬品)\n- フィルターろ過精度: 5 µm\n- 最大使用圧力: 1.5 MPa\n- 許容液体温度: 0 ~ 90℃\n- 本体材質: PTFEライニング",
    "TopicType": "iirds:GenericReference",
    "InformationSubject": [
      "iirds:GenericTechnicalData"
    ],
    "ProductVariant": [
      "ex:SP-X200"
    ],
    "RelatedEntities": [],
    "Confidence": 100,
    "Reasoning": "SP-X200固有の仕様データであるため独立チャンク化しました。`iirds:GenericTechnicalData`のindicators（performance metrics, units）に合致する静的データです。"
  }
]
```