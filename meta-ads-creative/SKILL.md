---
name: meta-ads-creative
description: Use when generating Meta (Facebook/Instagram) ad creatives — square 1:1 SaaS ad images with a consistent brand character and photo-realistic UI, using the dual-reference technique. Triggers: "広告画像を作って", "クリエイティブ作成", "この訴求のバナー", "ad creative", "make an ad image", "generate ad banner". Pairs with meta-ads-ops (delivery) and the meta-ads MCP (operation).
---

# Meta Ads Creative — 広告クリエイティブ生成（dual-reference 方式）

このスキルは、**ブランドの世界観を保ったまま、成果の出る Meta 広告の静止画**をAIに作らせるための型です。
広告を「操作」する Meta Ads MCP、「運用」する meta-ads-ops に対して、これは広告の「**中身（画像）を作る**」担当です。

> 入稿（画像アップロード→クリエイティブ作成）は Meta Ads MCP に委譲します。**Meta公式リモートMCPでも自作MCPでも動く**。本文中のツール名（`upload_ad_image` / `create_ad_creative` 等）は**例示**で、MCP により名前が多少違うので、接続中のMCPが公開している同じ役割のツールを使うこと。

> ⚠️ これは **手法（technique）** です。あなたのブランド素材（ロゴ・キャラクター・色・CTA文言）は
> `config.example.md` をコピーした `config.md` に登録して使います。勝ちクリエイティブそのものは、運用しながら育てる部分です。

> 🚨 画像生成API（gpt-image-2 等）は従量課金です。**課金が発生する生成は、実行前に必ずユーザーに確認**すること。
> Codex CLI 経由（ChatGPTサブスク枠内）は追加API課金なしで使えます（`references/backends.md`）。

---

## 中心となる考え方：dual-reference（参照画像2枚）

AIに広告画像を作らせると、ふつうは「UIが安っぽい」か「ブランドキャラが毎回別物」になります。
これを、**2枚の参照画像を同時に渡す**ことで両立させるのが dual-reference 方式です。

- **参照1＝ブランドキャラ/ロゴ**（あなたのマスコット・ロゴ。毎回固定で渡す → キャラの一貫性）
- **参照2＝構図/品質のお手本**（photo-realistic な SaaS UI モックの見本 → UIの質を引き上げる）

プロンプトで「**この2つのスタイルを共存させる：UI＝写実的、キャラ＝イラスト**」と明示するのが肝です。
詳細は `references/dual-reference-method.md`。

---

## ワークフロー（5ステップ）

最初に必ず `config.md`（無ければ `config.example.md`）を読み、ブランド素材・色・CTA文言・参照画像のパスを把握する。

### Step 1: 訴求を1つに絞る
1画像1メッセージ。複数の訴求を1枚に詰めない。`config.md` の訴求リストから1つ選ぶ。

### Step 2: 構図テンプレを選ぶ
代表的な型から1つ：
- **プロダクトモックアップ**（明るい背景にUI＋キャラ）
- **アラート/ダーク**（課題を突く心理訴求）
- **比較（左右分割）**（他のやり方 vs あなたの製品）
- **3ステップ オンボーディング**（導入の簡単さ）
- **ハブ&スポーク**（中心に製品、周囲に連携先）

### Step 3: お手本（参照2）を選ぶ
訴求・構図に合った **photo-realistic な見本画像**を1枚選ぶ（自社の過去の良いクリエ、または品質の高いSaaS広告の構図見本）。`config.md` に登録しておく。

### Step 4: 生成する
`references/prompt-template.md` の書式でプロンプトを組み、`references/backends.md` のいずれかで生成する。
- **試行錯誤・1枚もの → Codex CLI**（サブスク枠内、追加課金なし。デフォルト推奨）
- **量産・最終品質 → gpt-image-2 API**（dual-reference edits。従量課金、要ユーザー承認）

参照1（ブランドキャラ）は毎回渡す。参照2（構図見本）は訴求ごとに切り替える。

### Step 5: 検収する
`references/qa-checklist.md` を上から確認し、崩れ（テキスト崩れ・キャラ別物・UIが安っぽい・1枚に複数訴求）があれば作り直す。**入稿は meta-ads MCP の `upload_ad_image` → `create_ad_creative` で**（このスキルは「作る」まで、入稿は MCP）。

---

## やらないこと

- 広告アカウントの操作・入稿そのもの → meta-ads MCP
- 配信設定・運用判断 → meta-ads-ops スキル
- コピー（文言）の戦略設計 → これは別途。ここでは `config.md` で決めた文言を画像に焼き込むだけ
- ユーザー承認なしの課金API実行（必ず確認）
