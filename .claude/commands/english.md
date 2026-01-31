# 英語フラッシュカード作成スキル

セキュリティ学習中に出てきたフレーズを英語フラッシュカード化する。

## 入力形式

ユーザーから日本語のフレーズ、概念、または質問が渡される。
複数行でも可。

例:
```
Token TTL が長いとどうなる
Service Account の Secret が漏洩した
PKCE を使わないリスク
```

## 処理

### 1. 各フレーズを解析
- セキュリティの文脈を理解
- 適切な英語表現に変換
- 簡潔な説明を追加

### 2. フラッシュカード形式で出力

各フレーズについて:
```
## [日本語フレーズ]

**English:** [英語フレーズ]

**Explanation:** [英語での説明 2-3文]

**Tags:** #[関連タグ]

---
```

### 3. 日別ファイルに追記

`ideas/english/YYYYMMDD-phrases.md` に追記（日別ファイル）

ファイル形式:
```markdown
# English Phrases: YYYY-MM-DD

今日学んだセキュリティフレーズ。NotebookLM にアップロードして Podcast 化。

---

## [日本語フレーズ]

**English:** [英語フレーズ]

**Explanation:** [英語での説明]

**Tags:** #Token #Security

---
```

### 4. Anki インポート用ファイルにも追記

`ideas/english/YYYYMMDD-anki.txt` に追記（タブ区切り、日別）

```
[日本語]	[English + Explanation]	[tags]
```

## 出力

1. 変換結果を表示
2. `ideas/english/YYYYMMDD-phrases.md` に追記（なければ作成）
3. `ideas/english/YYYYMMDD-anki.txt` に追記（なければ作成）
4. 「追記完了。NotebookLM にアップロード可能」メッセージ

## 例

入力:
```
/anki-phrase Token TTL が長いとどうなる
```

出力:
```markdown
## Token TTL が長いとどうなる

**English:** What happens if token TTL is too long?

**Explanation:** If the token TTL (Time To Live) is too long,
attackers who steal the token can impersonate users for an
extended period. Best practice: access token 15 min, refresh
token 30 days.

**Tags:** #Token #Security #ASVS-V6

---

追記完了: ideas/english/20260201-phrases.md
NotebookLM にアップロードして Podcast 化できます。
```

## 1日の終わりに

```
ideas/english/20260201-phrases.md を NotebookLM にアップロード
  ↓
「Audio Overview」生成
  ↓
通勤・散歩中に聞く
```

## ファイル構成

```
ideas/english/
├── 20260201-phrases.md    ← NotebookLM用（日別）
├── 20260201-anki.txt      ← Ankiインポート用（日別）
├── 20260202-phrases.md
├── 20260202-anki.txt
└── ...
```
