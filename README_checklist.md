# 公開前チェックリスト（害獣駆除 2社比較LP）

生成物は `Gaichu-kujo/` 直下に格納（既存シロアリLPの `index.html` と衝突しないよう害獣LPは `gaichu.html`）：

- `gaichu.html` … 害獣駆除 2社比較LP（単一HTML・CSS/JSインライン・外部依存なし）
- `google_ads_keywords.csv` … Google広告エディタ取込用KWリスト
- `negative_keywords.csv` … 除外KW（全キャンペーン共通）
- `README_checklist.md` … 本ファイル

---

## ユーザー記入・公開前チェック

- [x] A案件の正式サービス名 → **ハウスガード24** で確定（対応済み）。
- [x] B案件の正式サービス名 → **ペスコンpro**（運営：株式会社MUSO）で確定（対応済み）。
- [ ] ※注意：ペスコンproは公式HP上コウモリ等も施工するが、A8の**成果対象はネズミ・ハクビシン・アライグマの3種のみ**。コウモリ導線は必ずハウスガード24へ（現設計どおり）。
- [ ] `{{AFFILIATE_LINK_A}}` / `{{AFFILIATE_LINK_B}}`：A8で発行した各アフィリンクを記入。
- [ ] `{{OPERATOR_NAME}}` / `{{CONTACT}}`：運営者情報・問い合わせ先を記入。
- [ ] A案件の**承認率実績**をA8担当に確認（「相談意志なしは集客経路確認のうえ却下」と明記のため要チェック）。
- [x] A案件の除外KW（社名「ハウスガード24」「ハウスガード」）を `negative_keywords.csv` に追加済み。表記ゆれは運用中に追加。
- [ ] GTMコンテナIDを発行し、`<!-- GTM here -->` にスニペットを貼付。`cta_click` イベントでトリガー／タグを設定。
- [ ] A8成果連携（発生→Google広告）の設定。

---

## 差し込みトークン一覧（`gaichu.html` 内。**未入力のまま残置**）

| トークン | 内容 | 出現箇所 |
|---|---|---|
| `{{AFFILIATE_LINK_A}}` | A案件（ハウスガード24）アフィリンク | 比較表下 / カードA / 結論 の各CTA `href` |
| `{{AFFILIATE_LINK_B}}` | B案件（ペスコンpro）アフィリンク | 比較表下 / カードB / 結論 の各CTA `href` |
| `{{OPERATOR_NAME}}` | 運営者名／サイト名 | フッター |
| `{{CONTACT}}` | 問い合わせ先 | フッター |

> リンクは全CTAで `rel="nofollow sponsored noopener" target="_blank"` を付与済み。

---

## 計測仕様（GTM）

- 全CTAに `data-vendor`（`A`/`B`）・`data-position`（`hero`/`table`/`card`/`conclusion`）を付与。
- 共通クリックリスナーが `dataLayer.push({event:'cta_click', vendor, position})` を発火。
- GTMでは変数 `{{DLV - vendor}}` `{{DLV - position}}` を作成し、カスタムイベント `cta_click` をトリガーに、GA4イベント等を設定。
- `<!-- GTM here -->` は `<head>` 冒頭 と `<body>` 直後 に配置済み（タグ本体を貼付）。

※ヒーローの「▶ 2社の比較を見る」はページ内スクロール用アンカー（`#compare`）で、`data-vendor` を持たないためCTAクリック計測の対象外。案件送客CTAのみ計測される設計。

---

## 遵守事項（生成時に順守済み）

- ASPのPR文は転載せず、指示書の独自コピーのみ使用。
- 最上級・断定表現なし。保証は「永年保証」「最長10年保証」と事業者の主張範囲に限定。
- 未確定項目（B案件の特典等）は「―」表記。
- 社名・商標はKWリストに不使用。社名系（ハウスガード24／ハウスガード／ペスコン系）は除外KWへ登録済み。
- フッターにアフィリエイト広告である旨の免責を表示（景表法ステマ規制対応）。
