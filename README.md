# bulksheet-ebay-categories

一括シートV3 / BulkToolsLib の **eBay カテゴリID AI 判定** 用カテゴリ参照データ（公開ホスティング）。

CLI 翻訳スキル（ebay-translation）が、どのツール（Codex CLI / Codex アプリ / Claude Code / Gemini CLI）からでも HTTP で取得できるよう、ここで配信する。中身は eBay 公開 Taxonomy の確定カテゴリID（treeVersion 134 / EBAY_US）と、一括シートのジャンル名のみ。

## 配信ファイル

- `ebay-category-buckets.json` … `{ tagToGenre, buckets }`
  - `tagToGenre`: タグ名 → ジャンル名
  - `buckets`: ジャンル名 → `[{ id, path }]`（公式確定カテゴリID と fullPath）

公開URL（GitHub Pages）:
`https://naokijodan.github.io/bulksheet-ebay-categories/ebay-category-buckets.json`

## 使い方（スキル側）

各商品で `recommendedUserTags` を決めたあと、`tagToGenre[タグ]` で genre を得て、`buckets[genre]` の候補から最適な categoryId を1つ選ぶ。候補内の数値IDのみ採用、無ければ空。

## 更新手順

このファイルは手編集しない。元データは一括シートApps_v3 の `gen_category_buckets.py`（入力 `~/Desktop/ebay-categories-curated.csv`）が生成する。

1. `cd ~/Desktop/ツール開発/一括シートApps_v3 && python3 gen_category_buckets.py`
2. 生成された `~/Desktop/ebay-category-buckets.json` をこのリポジトリにコピーして commit & push
3. 同時にライブラリの `CategoryBuckets.gs`（API翻訳=route② 用）も更新されるので、ライブラリも clasp push する（両者は同一生成物で整合）
