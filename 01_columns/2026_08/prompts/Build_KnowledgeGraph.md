# 指示
提供した16チャンク（manual_v4_Atomic_Data.md）を解析し、
「どの情報が、どの機種に、どの工具を使って紐付いているか」という
意味的な繋がり（SPO：主語・述語・目的語）を抽出してください。

# 抽出条件
- **Subject（主語）**: チャンクのTitle
- **Predicate（述語）**: iiRDSのプロパティ（iirds:relates-to-product-variant, iirds:has-tool, iirds:has-supply 等）
- **Object（目的語）**: 機種名、工具名、部品名、消耗品名

# 出力形式
[主語：チャンク名] --(述語：iiRDSプロパティ)--> [目的語：エンティティ名]
の形式で、網羅的にリストアップしてください。
