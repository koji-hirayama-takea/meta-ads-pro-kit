---
name: meta-ads-ops
description: Use when setting up, launching, or operating Meta (Facebook/Instagram) ad delivery via the meta-ads MCP — runs a pre-launch audit before going live, judges whether it is safe to touch an ad set given its learning phase, applies B2B-SaaS delivery decision rules, and drives a daily/weekly/monthly operating loop. Triggers: "配信前に点検して", "今いじって大丈夫?", "今週の振り返り", "set up this campaign", "audit before launch", "is it safe to change this ad set", "weekly ad review".
---

# Meta Ads Ops — 配信の「運用脳」

このスキルは、Meta 広告を **事故らせずに・再現性高く・成果が出る形で**運用するための判断の型です。
広告 API を叩く「手」（meta-ads MCP）に対して、このスキルが「**いつ・何を・どう判断するか**」の頭脳を提供します。

> 前提：広告の操作には Meta Ads MCP が入っていること。**Meta公式リモートMCP（OAuthだけで使える）でも、自作MCPでも、どちらでも動く**。
> このスキルは「判断」を担当し、実際の作成・更新・取得・診断は MCP のツールに委譲します。
> ⚠️ 本文中のツール名（`get_campaigns` / `search_interests` 等）は**例示**です。MCP によって名前が多少違うので、**接続中のMCPが公開しているツール一覧から、同じ役割のものを選んで使う**こと。

> ⚠️ このスキルは **汎用の方法論（method）** です。あなたの事業に合わせた具体値（予算・目標CPA・勝ちオーディエンス等）は
> `config.example.md` をコピーした `config.md` に書いて運用してください。中身の数値はあなたが育てる部分です。

---

## いつ何をするか（ルーティング）

| ユーザーの意図 | 動作 |
|---|---|
| 「配信前に点検して」「ONにする前に確認」「audit」 | → **A. 配信前監査** (`references/pre-launch-audit.md`) |
| 「今いじって大丈夫?」「変えてもいい?」 | → **B. 学習フェーズ判断** (`references/learning-phase.md`) |
| 「この設定でいい?」「AN は?」「Advantage+ は?」「入札どうする?」 | → **C. 判断ルール** (`references/decision-rules.md`) |
| 「今日の状況」「異常ない?」「今週の振り返り」「月次」 | → **D. 運用ループ** (`references/operating-loop.md`) |
| 指標の意味・目安が知りたい | → **用語と目安** (`references/glossary.md`) |

最初に必ず `config.md`（無ければ `config.example.md`）を読み、その事業の目標値・制約を判断の前提にすること。

---

## 鉄則（すべての判断の土台）

1. **設定値は推測で決めない。必ず API で検証する。**
   言語コード・地域ID・interest ID などは、思い込みで入れると「日本語のつもりが別言語に配信」のような事故になる。
   `meta-ads` MCP の `search_geo_locations` / `search_interests` 等で実際の値を確認してから設定する。
2. **「見る」と「いじる」を分ける。**
   数字は毎日動く。毎日見て毎日いじると、学習をリセットし続けることになる（B 参照）。
3. **ONにする前に必ず止まる。**
   新規 campaign/adset/ad は PAUSED で作り、A の監査を通してから ACTIVE にする。
4. **数字が動いた理由を説明できる状態を保つ。**
   変更したら理由と日時を記録する。後から「なぜ良く/悪くなったか」を辿れるように。
5. **サンプル数を確認してから勝ち負けを決める。**
   数件のデータで結論を出さない（D 週次参照）。

---

## A. 配信前監査（launch する前に必ず）

新規 / 変更した campaign・adset・ad を ACTIVE にする前に、`references/pre-launch-audit.md` のチェックを上から通す。
`meta-ads` MCP で現設定を取得し、チェックリストと突き合わせ、**危ない項目を列挙してから GO/NO-GO を提示**する。
1つでも未解決があれば NO-GO。勝手に ACTIVE にしない（人間の GO を待つ）。

## B. 学習フェーズ判断（「いじって大丈夫?」への答え方）

`references/learning-phase.md` を参照し、対象 adset の状態と経過日数から「触っていいか」を判断する。
- 配信開始から日が浅い / 学習中 → **原則「触らない」と答える**。なぜ触らない方がいいかを必ず添える。
- 触る必要がある場合 → **学習をリセットする変更かどうか**を判定し、リセットされるなら「今やるとここまでの学習が無駄になる」と警告する。

## C. 判断ルール（迷ったときの型）

`references/decision-rules.md` の各ルールを、その事業の `config.md` に照らして適用する。
ルールをそのまま押し付けず、**「なぜそう判断するか」**を説明し、事業の状況（予算規模・CV数・段階）に応じて調整する。

## D. 運用ループ（日次 / 週次 / 月次）

`references/operating-loop.md` の頻度別チェックを実行する。
- 日次：異常（配信停止・極端な数値）だけ確認。問題なければ「触らないでOK」と答える。
- 週次：サンプル数を確認したうえで勝ち負けを整理し、次の一手を提案する。
- 月次：大きな視点で学びをまとめ、来月の仮説を立てる。

---

## やらないこと

- クリエイティブ画像そのものの生成（別の画像 AI / スキルの領域）
- 法務・会計の判断
- `config.md` に無い、その事業固有の勝ち設定を勝手に断定すること（数値はユーザーと一緒に育てる）
