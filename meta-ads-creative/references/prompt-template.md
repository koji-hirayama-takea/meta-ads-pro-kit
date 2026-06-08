# 広告クリエイティブ プロンプト・テンプレート

dual-reference 方式で生成するときのプロンプト書式。`{ }` を `config.md` の値で埋める。

## テンプレート（英語プロンプト推奨：画像生成は英語の方が安定）

```
Premium square 1:1 Meta ad creative for a {業種/例: B2B SaaS} product. Topic: {訴求の1行}.

REFERENCE IMAGE 1 (brand character/logo): {brand_character_image の説明}.
The brand character in this generated ad MUST match this reference's illustration style exactly.

REFERENCE IMAGE 2 (overall composition & quality): {composition_reference の説明}.
The UI elements MUST match this photo-realistic premium SaaS polish — NOT cartoon, NOT flat illustration.

The two styles coexist: UI = photo-realistic SaaS mockup, brand character = illustration.

Exact text to render (keep it short and crisp):
{ブランド名/ロゴ語}
{大見出し1}
{大見出し2}
{サブコピー}
{バッジ文言（例: 無料 など）}
{CTA文言}

Scene: {構図テンプレに沿った具体描写。写実的な製品UIに「ユーザーの問い → 製品の答え → 次の行動」が見える}.

UI style: photo-realistic premium SaaS mockup matching reference 2.
Brand character style: illustration matching reference 1 exactly.

Composition: 1080x1080. MASSIVE headline in the upper area (~26-28% height) with "{強調キーワード}" in {ブランドの差し色}. {構図に応じた配置}. Badge bottom-left, {差し色} CTA button bottom-center with an arrow, brand character bottom-right (~280px).

Avoid: cartoon/flat-illustration UI (UI must be photo-realistic), making the brand character photo-realistic (it must stay illustration per reference 1), real third-party brand logos (use generic stylized labels), stock-photo people, photographic human faces, garbled text, dark muddy backgrounds, multiple characters.
```

## 埋めるときのコツ

- **大見出しは短く**。1〜2行、各10〜14字程度。長いと崩れる
- **強調キーワードは1つだけ**ブランドの差し色にする（全部色を付けない）
- **焼き込むテキストは最小限**（ブランド名 / 見出し / バッジ / CTA）。説明文を画像に詰めない
- **「The two styles coexist」を必ず残す**（消すとUIかキャラのどちらかが崩れる）
- **Avoid 句の "photo-realistic にしない（キャラ）" と "イラストUIにしない" は両方残す**
- 連携先などの**実ロゴは描かせない**。「generic stylized labels」で逃がす

## サイズ

- 出力は正方形（1024×1024 または 1080×1080）。Meta は 1080×1080 推奨だが 1024 でも入稿可
- 品質設定は最高にする（テキストの崩れと統合感のため）
