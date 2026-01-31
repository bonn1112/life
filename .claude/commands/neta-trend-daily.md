# トレンドネタ収集スキル

はてなブックマーク、Hacker News、Redditから最新トレンド情報を毎日収集し、`ideas/daily/YYYYMMDD-trend.md`に保存する。

## 実行手順

### 1. ユーザープロファイル読み込み

CLAUDE.md を読み込み、ユーザーの興味領域を把握する：
- AI開発・AIエージェント
- Webセキュリティ・認証基盤（OAuth, OIDC）
- OSS開発
- 個人開発・SaaS・スタートアップ
- キャリア・CTO
- JavaScript/TypeScript/Node.js

### 2. データ収集

以下のソースからトレンド情報を収集：

#### はてブIT（テクノロジー）

```bash
curl -s "https://b.hatena.ne.jp/hotentry/it.rss"
```

RSSからタイトル、URL、ブックマーク数を抽出。

#### Hacker News

トップストーリーのID一覧を取得：
```bash
curl -s "https://hacker-news.firebaseio.com/v0/topstories.json" | jq '.[0:20]'
```

各記事の詳細を取得（Algolia APIが便利）：
```bash
curl -s "https://hn.algolia.com/api/v1/items/{id}" | jq '{title, url, points}'
```

#### Reddit（13サブレッド）

**重要**: `old.reddit.com` を使用し、User-Agent ヘッダーを必ず設定する

```bash
curl -s -H "User-Agent: neta-trend/1.0" "https://old.reddit.com/r/{subreddit}/hot.json?limit=10" | jq '.data.children[].data | {title, url, score, num_comments}'
```

対象サブレッド：
- r/programming
- r/netsec
- r/cybersecurity
- r/javascript
- r/typescript
- r/node
- r/rust
- r/golang
- r/devops
- r/selfhosted
- r/SideProject
- r/startups
- r/MachineLearning

### 3. 興味領域マッチング

収集した記事を以下の観点で分析：
- ユーザーの興味領域との関連度
- トレンド性（ブクマ数、ポイント数、投票数）
- 発信ネタとしての活用可能性

興味度を★3段階で評価：
- ★★★：強く関連、発信ネタになる
- ★★：関連あり、参考になる
- ★：軽く関連

### 4. 出力フォーマット

`ideas/daily/YYYYMMDD-trend.md` に保存（YYYYMMDDは実行日）

```markdown
# トレンドネタ: YYYY-MM-DD

## 注目トピック

（今日特に気になった3-5件を自由に記述）

---

## はてブIT（日本市場）

| タイトル | ブクマ数 | 興味度 | メモ |
|---------|---------|--------|------|
| [タイトル](元記事URL) | XXX users | ★★★ | 発信に活用できるポイント |

---

## Hacker News（グローバル）

| タイトル（日本語翻訳） | ポイント | 興味度 | メモ |
|---------|---------|--------|------|
| [タイトル](HNコメントページURL) | XXXpt | ★★★ | ... |

---

## Reddit（13サブレッド）

| タイトル（日本語翻訳） | 投票数 | コメント数 | 興味度 | カテゴリ | メモ |
|---------|---------|---------|--------|---------|------|
| [タイトル](Redditコメント完全URL) | XXX ups | XXX | ★★★ | Security/AI/OSS等 | ... |
```

## 重要な制約

- **すべての記事にURLリンクを必ず含める**
- はてブは**元記事URL**を使用
- Hacker Newsは**HNコメントページURL**を使用（`https://news.ycombinator.com/item?id=XXX`）
- Redditは**完全URL形式**を使用（`https://www.reddit.com/r/.../comments/.../...`）
- 英語タイトルは**日本語に翻訳**
- 興味度の低い記事は省略可（★以上のみ記載）
- Reddit APIはレート制限あり（1分60リクエスト程度）
