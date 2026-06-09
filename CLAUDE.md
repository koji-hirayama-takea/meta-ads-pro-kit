# meta-ads-pro-kit — セットアップ案内（エージェント用）

このファイルは、Claude Code（や互換エージェント）が、このキットのセットアップを
**対話的に案内・自動化**するための指示書です。

ユーザーが「**このキットをセットアップして**」「setup this kit」「広告のスキル入れて」等と言ったら、
以下を**上から順に**実行してください。各ステップで結果を報告し、次に進む前に必要な確認を取ること。

> このキットは2つのAIスキル（広告クリエイティブ生成＋配信運用）です。広告を実際に操作するには
> 無料の **meta-ads MCP**（広告APIを叩く「手」）が必要なので、未導入なら**それも一緒にセットアップ**します。

---

## 🔐 最優先の安全ルール

- 各スキルの `config.md` には自社の数値・素材が入ります。**`config.md` は commit / 公開しない**（`.gitignore` 済み）。
- MCP の `META_SYSTEM_USER_TOKEN`（広告アカウントの全権限を持つ鍵）は**絶対に commit / 共有しない**。トークンをチャットログに残さない。
- ファイルをコピー・上書きする前に、既存があれば必ずユーザーに確認する。

---

## セットアップ手順

### Step 1: 2つのスキルを導入する

ユーザーが Claude Code を開いているプロジェクトの `.claude/skills/` に、このキットの2フォルダをコピーする。

- `meta-ads-creative/` → `<プロジェクト>/.claude/skills/meta-ads-creative/`
- `meta-ads-ops/` → `<プロジェクト>/.claude/skills/meta-ads-ops/`

`.claude/skills/` が無ければ作成する。同名スキルが既にある場合は上書き前に確認する。

### Step 2: 設定ファイル（config）を用意する

各スキルの `config.example.md` を `config.md` にコピーする（中身は空欄のひな形）。

- `meta-ads-ops/config.example.md` → `meta-ads-ops/config.md`
- `meta-ads-creative/config.example.md` → `meta-ads-creative/config.md`

コピー後、「ここに自社の目標値やブランド素材を入れてください。最初は仮置きでOKです」と案内する。
**`config.md` は commit しない**ことを伝える。

### Step 3: 広告を操作する土台（meta-ads MCP）を確認・導入する

このキットのスキルは、広告の操作を **meta-ads MCP** に委譲します。まず導入済みか確認する。

1. プロジェクトの `.mcp.json` に `meta-ads`（または `meta-ads-self` 等の同等エントリ）があるか確認する。
2. **導入済みなら** → Step 4 へ。
3. **未導入なら**、ユーザーに「広告を操作する土台（無料のMCP）がまだ無いので、一緒に入れます」と伝えてから：
   - 公開リポジトリを clone する：`git clone https://github.com/koji-hirayama-takea/meta-ads-mcp`
   - clone した `meta-ads-mcp/` フォルダ内の **`CLAUDE.md` の手順に従ってセットアップ**する（依存インストール → Meta側トークンの取得を対話で案内 → `.env.local` 記入 → `.mcp.json` への create-or-merge 登録）。
   - ⚠️ **Meta側のトークン発行は、Meta の管理画面での人間の操作**が必要です。エージェントは代理発行できないので、`meta-ads-mcp/docs/01-meta-app-setup.md` を参照して**手順を1つずつ案内**し、ユーザーにクリックしてもらう。
   - 既に MCP は入っているがトークン未設定の場合も、同 docs に沿って案内する。

### Step 4: 反映と動作確認

1. `.claude/skills/` と `.mcp.json` を変更したので、**Claude Code の再起動が必要**。エージェントは自分を再起動できないため、ユーザーに「**Claude Code を再起動してください**」と案内する。
2. 再起動後、ユーザーに次を試してもらう：
   - 「広告アカウントの情報を見せて」→ MCP が動いているか（アカウント名や残高が返れば接続OK）
   - 「配信を始める前に点検して」→ meta-ads-ops スキルが効いているか
   - 「この訴求で広告画像を作って」→ meta-ads-creative スキルが効いているか

---

## 完了の合図

- `.claude/skills/` に `meta-ads-creative/` と `meta-ads-ops/` が入っている
- 各スキルの `config.md` が作成済み（commit されていない）
- `meta-ads` MCP が `.mcp.json` に登録され、トークンが設定されている（未導入だったら clone + セットアップ済み）
- 再起動後、「広告アカウントを見せて」で接続成功

ここまで来たら「セットアップ完了。あとは日本語で『配信前に点検して』『今週の振り返りして』『この訴求で広告画像を作って』のように話しかければ動きます」と案内して終了。

---

## やらないこと

- Meta側トークンの代理取得（Metaの管理画面での人間の操作。エージェントは案内のみ）
- `config.md` の自社固有値を勝手に断定すること（ユーザーと一緒に埋める）
- ユーザー確認なしの上書き・課金API実行
