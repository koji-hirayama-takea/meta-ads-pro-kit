# meta-ads-ops-skill

Meta (Facebook/Instagram) 広告を、AI（Claude Code）に **事故らせず・成果が出る形で**運用させるための
**運用メソッドのスキル**です。広告APIを叩く「手」（[meta-ads-mcp](https://github.com/koji-hirayama-takea/meta-ads-mcp)）に対して、
このスキルが「**いつ・何を・どう判断するか**」の運用脳を提供します。

> 道具（MCP）だけでは成果は出ません。同じ道具でも、配信の「型」を持っているかで結果は大きく変わります。
> このスキルは、その型 — 配信前監査 / 学習フェーズの扱い / 判断ルール / 運用ループ — を AI に実行させます。

---

## これは「型」であって「秘伝の数値」ではありません

このスキルが渡すのは、**どの事業でも通用する判断の方法論（method）**です。
「どの予算で・どの入札値で・どのオーディエンスが勝つか」といった**個別の正解（config）は入っていません**。
それは事業ごとに違い、あなたが運用しながら育てる部分だからです。

自社の数値は `meta-ads-ops/config.example.md` を `config.md` にコピーして書き込みます。

---

## インストール

1. このリポジトリを取得（GitHub からダウンロード or clone）
2. `meta-ads-ops/` フォルダを、あなたのプロジェクトの `.claude/skills/meta-ads-ops/` にコピー
3. `meta-ads-ops/config.example.md` を `meta-ads-ops/config.md` にコピーし、自社の値を記入
4. 広告操作には [meta-ads-mcp](https://github.com/koji-hirayama-takea/meta-ads-mcp) が必要なので、未導入なら先にセットアップ
5. Claude Code を再起動 → スキルが認識される

> Claude Code 以外のエージェントでも、`SKILL.md` と `references/` を読ませれば同じ方法論を適用できます。

---

## 使い方（話しかけるだけ）

- **「配信を始める前に、設定を点検して」** → 配信前監査を回し、危ない箇所と GO/NO-GO を返す
- **「今この広告セットいじって大丈夫?」** → 学習フェーズ的に触っていいタイミングかを判断
- **「この設定でいい?（言語 / 配置 / 入札 / 自動拡張）」** → 判断ルールに照らして助言
- **「今日の状況は?」「今週の振り返りして」「月次まとめて」** → 日次 / 週次 / 月次の運用ループを実行

---

## 中身

```
meta-ads-ops/
├── SKILL.md                      ← 本体（ルーティング + 鉄則 + 4つの動作）
├── config.example.md             ← 自社の値テンプレ（config.md にコピーして使う）
└── references/
    ├── pre-launch-audit.md       ← 配信前監査チェックリスト
    ├── learning-phase.md         ← 学習フェーズの扱い（3日触らない等）
    ├── decision-rules.md         ← 迷ったときの判断ルール
    ├── operating-loop.md         ← 日次 / 週次 / 月次の運用ループ
    └── glossary.md               ← 指標の定義と一般的な目安
```

---

## ライセンス

MIT License — [LICENSE](./LICENSE) を参照。
