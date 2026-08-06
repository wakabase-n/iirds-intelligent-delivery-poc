# Role
あなたはiiRDSの品質保証およびアノテーションの公認スペシャリストです。
入力された「対象ドキュメント」を解析し、後述の「iiRDS完全版定義（JSON）」と「チャンク化ルール」に基づいて、厳密に構造化データを作成してください。

# チャンク化ルール（必須要件）
1. **バリアントによる分割**: 見出し単位ではなく、「意味の塊」で分割してください。特に「SP-X200のみ」のように特定のProduct Variantに限定される記述は、必ず独立したトピック（チャンク）として切り出してください。共通部分は全バリアントのタグを付与します。
2. **粒度**: 1つのトピックは「1つの質問に答える単位（1つのTopicType）」にしてください。

# Output Format (JSON List)
各チャンクに対し、以下の要素を持つJSONオブジェクトのリストを出力してください。
* `Title`: チャンクのタイトル（例: 交換手順：2. 旧フィルターの除去 (SP-X200専用)）
* `Content`: **チャンクの本文（対象ドキュメントから該当箇所を正確に抽出し、マークダウン形式で記述してください）**
* `TopicType`: 最も適切なクラスIRI
* `InformationSubject`: 該当する場合のみIRIのリスト（無い場合は空配列）
* `ProductVariant`: 該当する機種のIRIリスト（例: ["ex:SP-X100", "ex:SP-X200"]）
* `RelatedEntities`: チャンク内に登場する工具(Tool)や消耗品(Supply)、部品(Component)があれば抽出
* `Confidence`: 判定の自信度（0-100%）
* `Reasoning`: なぜそのTopicTypeやInformationSubjectを選んだのか、iiRDS定義の `indicators` や `what_it_is_not` を具体的に引用して論理的に説明してください。

# iiRDS定義 (Knowledge Base)

```
{
  "meta": {
    "source": "Guide for the Standardized Use of iiRDS",
    "version": "1.0 (Complete Edition)",
    "date": "2025-10-13",
    "description": "Comprehensive definition set including Document Types, Topic Types, Info Subjects, Product Metadata, Functional Metadata, and Lifecycle Phases."
  },
  "DocumentTypes": [
    {
      "iri": "iirds:OperatingInstructions",
      "label": "Operating Instructions",
      "definition": "Document type that refers to information on the correct use of the product.",
      "indicators": [
        "Purpose: Guide users in correct/safe use during normal operation.",
        "Audience: End users, operators.",
        "Features: Operating procedures, safety instructions, basic setup, troubleshooting for daily use."
      ],
      "what_it_is_not": "Administrator guides, Installation instructions."
    },
    {
      "iri": "iirds:MaintenanceInstructions",
      "label": "Maintenance Instructions",
      "definition": "Document type that refers to information on procedures to be followed to ensure that a product remains in good working order.",
      "indicators": [
        "Purpose: Ensure continued safe/efficient operation through upkeep.",
        "Audience: Maintenance personnel.",
        "Features: Scheduled tasks, inspection checklists, cleaning, minor repair."
      ],
      "what_it_is_not": "Operating instructions, Repair instructions (deep overhaul)."
    },
    {
      "iri": "iirds:InstallationInstructions",
      "label": "Installation Instructions",
      "definition": "Document type that refers to information on how to set up a product in the designated target environment.",
      "indicators": [
        "Purpose: Ensure proper/safe physical or software installation.",
        "Audience: Technicians, system integrators.",
        "Features: Mounting, required tools, safety notices for installation, initial setup."
      ],
      "what_it_is_not": "Maintenance instructions, Assembly instructions."
    },
    {
      "iri": "iirds:AssemblyInstructions",
      "label": "Assembly Instructions",
      "definition": "Document type that refers to information on how parts are put together to complete a specific product.",
      "indicators": [
        "Purpose: Step-by-step guidance to assemble a product physically.",
        "Audience: Technicians, assembly workers.",
        "Features: Exploded views, sequential assembly steps."
      ],
      "what_it_is_not": "Installation instructions (mounting in environment)."
    }
  ],
  "TopicTypes": [
    {
      "iri": "iirds:GenericTask",
      "label": "Task",
      "definition": "Topic type that provides procedures and action steps to be followed.",
      "indicators": [
        "Question: 'How do I...?'",
        "Features: Imperative verbs (Click, Select), step-by-step instructions, prerequisites."
      ],
      "what_it_is_not": "Troubleshooting, Reference, Concept."
    },
    {
      "iri": "iirds:GenericConcept",
      "label": "Concept",
      "definition": "Topic type providing background information or essential principles.",
      "indicators": [
        "Question: 'What is...?', 'Why...?'",
        "Features: Definitions, architecture overviews, relationships, theory."
      ],
      "what_it_is_not": "Task, Reference."
    },
    {
      "iri": "iirds:GenericReference",
      "label": "Reference",
      "definition": "Topic type that provides additional details for lookup.",
      "indicators": [
        "Question: 'What are the values/options?'",
        "Features: Tables, parameter lists, UI element descriptions, error code lists."
      ],
      "what_it_is_not": "Task, Concept."
    },
    {
      "iri": "iirds:GenericTroubleshooting",
      "label": "Troubleshooting",
      "definition": "Topic type that provides explanation on symptoms, diagnosis, and resolution.",
      "indicators": [
        "Question: 'What’s wrong and how do I fix it?'",
        "Features: Symptom description, cause explanation, corrective actions."
      ],
      "what_it_is_not": "Standard maintenance task."
    },
    {
      "iri": "iirds:GenericForm",
      "label": "Form",
      "definition": "Topic type that provides information in pre-defined fields to be filled out.",
      "indicators": [
        "Features: Field labels, checkboxes, empty lines for entry, checklists."
      ],
      "what_it_is_not": "Reference (static data)."
    },
    {
      "iri": "iirds:GenericLearning",
      "label": "Learning",
      "definition": "Topic type that provides learning content.",
      "indicators": [
        "Purpose: Education / Training.",
        "Features: Learning objectives, quizzes, tutorials."
      ],
      "what_it_is_not": "Concept (pure explanation without pedagogical structure)."
    }
  ],
  "InformationSubjects": [
    {
      "iri": "iirds:GenericSafety",
      "label": "Safety",
      "definition": "Information subject that covers content which helps to avoid risk.",
      "indicators": [
        "Features: Signal words (DANGER, WARNING), hazard symbols, PPE requirements."
      ],
      "what_it_is_not": "Conformity statements."
    },
    {
      "iri": "iirds:GenericTechnicalData",
      "label": "Technical Data",
      "definition": "Information subject covering qualitative and quantitative characteristics.",
      "indicators": [
        "Features: Dimensions, tolerances, performance metrics, units of measurement."
      ],
      "what_it_is_not": "Technical Overview."
    },
    {
      "iri": "iirds:IntendedUse",
      "label": "Intended Use",
      "definition": "Information subject stating the range of functions or foreseen applications.",
      "indicators": [
        "Features: Target environments, user roles, functional boundaries, misuse warnings."
      ],
      "what_it_is_not": "Safety instructions."
    },
    {
      "iri": "iirds:ProductIdentification",
      "label": "Product Identification",
      "definition": "Information subject covering the identity and characteristics of a product.",
      "indicators": [
        "Features: Model numbers, serial numbers, manufacturer details."
      ],
      "what_it_is_not": "Technical Data."
    },
    {
      "iri": "iirds:GenericTechnicalOverview",
      "label": "Technical Overview",
      "definition": "Information subject covering the technical structure/architecture.",
      "indicators": [
        "Features: Block diagrams, system maps, component breakdown."
      ],
      "what_it_is_not": "Functionality (behavior)."
    },
    {
      "iri": "iirds:OperatingElement",
      "label": "Control Element",
      "definition": "Information subject covering interaction elements in a user interface.",
      "indicators": [
        "Features: Buttons, switches, LEDs, icons, touch zones."
      ],
      "what_it_is_not": "Product Function."
    },
    {
      "iri": "iirds:GenericConformity",
      "label": "Conformity",
      "definition": "Information subject covering applicable law, standards, or compliance.",
      "indicators": [
        "Features: Declaration of Conformity, CE marking, ISO standards, certificates."
      ],
      "what_it_is_not": "Safety."
    },
    {
      "iri": "iirds:GenericProcess",
      "label": "Process",
      "definition": "Information subject covering structured activities achieving a specific goal.",
      "indicators": [
        "Features: Flowcharts, cross-functional workflows, swim lanes."
      ],
      "what_it_is_not": "Task (single procedure)."
    }
  ],
  "ProductMetadata": [
    {
      "iri": "iirds:ProductVariant",
      "label": "Product Variant",
      "definition": "Item or service designed to meet needs of customers.",
      "indicators": [
        "Features: Specific model names (e.g., SP-X100), localized versions."
      ],
      "what_it_is_not": "Product family."
    },
    {
      "iri": "iirds:Component",
      "label": "Component",
      "definition": "Part used as a constituent in an assembled product.",
      "indicators": [
        "Features: Physical parts (Screw, Motor, Board), BOM items."
      ],
      "what_it_is_not": "Product variant."
    },
    {
      "iri": "iirds:GenericProductProperty",
      "label": "Product Property",
      "definition": "A characteristic that a product ALWAYS exhibits (Static).",
      "indicators": [
        "Features: Weight, dimensions, material, color, voltage rating."
      ],
      "what_it_is_not": "Product Function (dynamic)."
    },
    {
      "iri": "iirds:GenericProductFunction",
      "label": "Product Function",
      "definition": "A characteristic exhibited only during a process (Dynamic).",
      "indicators": [
        "Features: Actions (Pumping, Heating), capabilities, modes."
      ],
      "what_it_is_not": "Product Property (static)."
    }
  ],
  "FunctionalMetadata": [
    {
      "iri": "iirds:GenericRole",
      "label": "Role",
      "definition": "Set of behaviors associated with a party.",
      "indicators": [
        "Features: Job titles (Admin, Technician), user types."
      ],
      "what_it_is_not": "Specific person names."
    },
    {
      "iri": "iirds:GenericPlanningTime",
      "label": "Planning Time",
      "definition": "Period of time required for a task.",
      "indicators": [
        "Features: Durations (mins, hours), 'Estimated time'."
      ]
    },
    {
      "iri": "iirds:GenericSupply",
      "label": "Supply",
      "definition": "Consumables used by an actor.",
      "indicators": [
        "Features: Grease, oil, cleaning fluid, replacement filters."
      ],
      "what_it_is_not": "Tools."
    },
    {
      "iri": "iirds:GenericTool",
      "label": "Tool",
      "definition": "Instrument used by an actor.",
      "indicators": [
        "Features: Screwdriver, wrench, diagnostic software."
      ],
      "what_it_is_not": "Supply."
    }
  ],
  "ProductLifecyclePhases": [
    {
      "iri": "iirds:GenericPuttingToUse",
      "label": "Putting Into Use",
      "definition": "Phase after production, before regular use.",
      "indicators": [
        "Features: Transportation, Unboxing, Mounting, Commissioning."
      ]
    },
    {
      "iri": "iirds:GenericUse",
      "label": "Use",
      "definition": "Phase where product realizes its function.",
      "indicators": [
        "Features: Normal operation, control."
      ]
    },
    {
      "iri": "iirds:MaintenancePhase",
      "label": "Maintenance Phase",
      "definition": "Phase comprising activities to retain/restore state.",
      "indicators": [
        "Features: Cleaning, Inspection, Repair."
      ]
    },
    {
      "iri": "iirds:Disposal",
      "label": "Disposal",
      "definition": "Phase of elimination.",
      "indicators": [
        "Features: Disassembly, recycling, scrapping."
      ]
    }
  ]
}
```

# 対象ドキュメント
# 10_スマート・ポンプ SP-Xシリーズ　取扱説明書 3章
# 第3章 フィルターエレメントの交換

## 3.1 メンテナンスの概要
スマート・ポンプ SP-Xシリーズ（SP-X100およびSP-X200）において、フィルターエレメントは製品の性能を維持するための最も重要な部品です。フィルターが目詰まりを起こすと、吐出圧力の低下やモーターへの過負荷が発生する可能性があります。
推奨される交換時期は、累積稼働時間が500時間に達した時点、または差圧計の表示が0.2MPaを超えた時点のいずれか早い方です。定期的な交換により、ポンプの寿命を延ばし、突発的な故障を防ぐことができます。

## 3.2 安全上のご注意

**警告**
* **感電の危険**: 作業を始める前に、必ず主電源を切り、電源プラグをコンセントから抜いてください。
* **残留圧力**: ポンプ内部には高圧が残留している場合があります。ドレンバルブを開放し、圧力が完全に抜けたことを確認してから作業を行ってください。

**注意（SP-X200のみ）**
* **化学熱傷の危険**: 耐薬品モデル（SP-X200）を使用している場合、内部に危険な薬液が残っている可能性があります。必ず耐薬品手袋と保護メガネを着用し、皮膚への付着を防いでください。

## 3.3 準備するもの

作業には以下の工具と交換部品が必要です。作業前に準備してください。

| 品目名 | 規格・品番 | 備考 |
| :--- | :--- | :--- |
| 交換用フィルター | FLT-X100 (標準) / FLT-X200 (耐薬品) | モデルに合ったものを用意 |
| Oリング | OR-S25 | 新品に交換してください |
| 六角レンチ | 5mm | ハウジング固定用 |
| トルクレンチ | 設定範囲 10-20 N・m | 締め付け管理用 |
| セラミック製スパナ | SP-TOOL-01 | **SP-X200のみ必要** |

## 3.4 交換手順

以下の手順に従って交換を行ってください。

1.  **ハウジングの取り外し**
    5mmの六角レンチを使用して、フィルターハウジング下部の4本のボルトを緩めます。ボルトを完全に取り外し、ハウジングをゆっくりと引き抜いてください。内部の液体がこぼれる場合があるため、受け皿を用意してください。

2.  **旧フィルターの除去**
    使用済みのフィルターエレメントを反時計回りに回して取り外します。
    * **SP-X100（標準モデル）の場合**: そのまま手で引き抜いてください。
    * **SP-X200（耐薬品モデル）の場合**: フィルターが固着している場合があります。専用のセラミック製スパナ（SP-TOOL-01）を使用して、慎重に緩めてください。

3.  **清掃とOリング交換**
    ハウジング内部を清潔なウエスで拭き取ります。古いOリングを取り外し、新しいOリング（OR-S25）にシリコングリスを薄く塗布してから溝に装着してください。

4.  **新フィルターの取り付け**
    新しいフィルターエレメントを装着します。確実に奥まで差し込まれていることを確認してください。

5.  **組み立てと締め付け**
    ハウジングを元の位置に戻し、ボルトを手で仮締めします。その後、トルクレンチを使用して **15 N・m** のトルクで対角線上に本締めを行ってください。締め付けトルクが不足すると液漏れの原因となり、過大すぎると破損の原因となります。

## 3.5 廃棄について
取り外した使用済みフィルターおよびOリングは、産業廃棄物として処理する必要があります。
特に **SP-X200（耐薬品モデル）** で使用したフィルターには有害な化学物質が付着している可能性があります。必ず密閉袋に入れ、お客様の地域の環境規制および社内規定に従って、特別管理産業廃棄物として適切に廃棄してください。一般ゴミとして捨てないでください。

## 3.6 主な仕様（参考）

| 項目 | SP-X100 (標準) | SP-X200 (耐薬品) |
| :--- | :--- | :--- |
| フィルターろ過精度 | 10 µm | 5 µm |
| 最大使用圧力 | 1.0 MPa | 1.5 MPa |
| 許容液体温度 | 0 ~ 60℃ | 0 ~ 90℃ |
| 本体材質 | SUS304 | PTFEライニング |

---
