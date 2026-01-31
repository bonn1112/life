# Yosukeさんのライフ・キャリア・学習管理リポジトリ

GitHub Issues + Projects + Markdown で人生を管理する。

## 構成

### Issues / Projects
- **2025年目標**：セキュリティ × 認証スペシャリスト構築
- **2026年目標**：スタートアップCTO 転職実現
- **月別学習**：OWASP ASVS 体系的習得
- **TL昇格**：リーダーシップ実績作り

### ideas/daily/
毎日のトレンド情報と学習日記
- `YYYYMMDD-trend.md`：セキュリティ × AI のトレンド情報
- `YYYYMMDD-diary.md`：その日の学習内容、思考、気づき

### ideas/security/
セキュリティ学習の詳細記録
- `oauth-2.1-study.md`：OAuth 2.1 仕様書の読書記録
- `owasp-asvs-v*.md`：各カテゴリの学習まとめ
- `threat-modeling-notes.md`：脅威モデリング実践記録

### ideas/blog/
ブログ発信の企画・下書き
- 日本語記事：月2-3本
- 英語記事：月1本（Medium）

### ideas/english/
英語 × セキュリティの強化
- 英語ブログ・論文の要約
- 英語での発信準備

## 運用ルール

### 1. 毎日のトレンド収集（朝15分）
```bash
# 毎朝 8:00 に実行
# ideas/daily/YYYYMMDD-trend.md を作成
# セキュリティ × AI のトレンド情報を記録
```

テンプレート：
```markdown
# トレンドネタ: YYYY-MM-DD

## はてブIT（日本市場）

| タイトル | ブクマ数 | 興味度 | メモ |
|---------|---------|--------|------|
| [タイトル](URL) | XXX users | ★★★/★★/★ | 発信に活用できるポイント |

## Hacker News（グローバル）

| タイトル（日本語翻訳） | ポイント | 興味度 | メモ |
|---------|---------|--------|------|
| [タイトル](HNコメントページURL) | XXXpt | ★★★/★★/★ | ... |

## Reddit（13サブレッド）

| タイトル（日本語翻訳） | 投票数 | コメント数 | 興味度 | カテゴリ | メモ |
|---------|---------|---------|--------|---------|------|
| [タイトル](Redditコメント完全URL) | XXX ups | XXX | ★★★ | Security/AI/OSS等 | ... |

## 注目トピック

（今日特に気になったことを自由に記述）
```

### 2. 毎日の学習日記（夜30分）
```bash
# 毎晩 22:00 に実行
# ideas/daily/YYYYMMDD-diary.md を作成
# その日の学習内容、気づき、改善案を記録
```

テンプレート：
```markdown
# 日記: YYYY-MM-DD

## 今日の学習
- （OWASP ASVS / 徳丸本 / RFC など）

## 気づき
-

## 実装への応用
-

## 英語の学習
-

## 次のアクション
-

## 気分
-
```

### 3. 週1回のブログ執筆（金曜 2-3時間）
```bash
# 金曜日に以下を実施：
# 1. ideas/blog/ に下書きを保存
# 2. ブログプラットフォーム（Zenn など）に発信
# 3. SNS（Twitter / LinkedIn）でシェア
```

### 4. 月1回の振り返り（月末 1時間）
```bash
# 月末に以下を実施：
# 1. Issues / Projects を確認
# 2. 先月の成果物をリスト化
# 3. 来月の目標を設定
```

## 参考資料

- [GitHub で人生を管理する](https://zenn.dev/hand_dot/articles/85c9640b7dcc66)
- [Claude Code Desktop の使い方](./github-life-management-for-yosuke.md)
- [CLAUDE.md](./CLAUDE.md)

## 推奨ツール

- **エディター**：VS Code
- **脅威モデリング**：Microsoft Threat Modeling Tool
- **脆弱性テスト**：Burp Suite（Community Edition）
- **開発効率化**：Claude Code Desktop / Claude Haiku

## セキュリティ学習教材体系

### Tier 1：基礎理論（無料）
- OWASP ASVS 4.0
- OAuth 2.1 / OpenID Connect 仕様書
- CWE（Common Weakness Enumeration）

### Tier 2：実装教材（書籍）
- 徳丸本「安全なWebアプリケーション開発ガイド」
- 「Webセキュリティ大全」
- 「暗号化プログラミング」
- 「マイクロサービス セキュリティ イン アクション」

### Tier 3：脅威モデリング（無料ツール）
- Microsoft Threat Modeling Tool
- OWASP Threat Dragon

### Tier 4：発展教材（無料）
- セキュリティ論文（Google Scholar / IACR）
- 徳丸浩ブログ
- Auth0 ブログ
- IPA / JPCERT/CC の情報

### Tier 5：実践（無料）
- Burp Suite（Community Edition）
- WebGoat

## 2025年のマイルストーン

```
【Q1】セキュリティ基礎習得
  ✓ OWASP ASVS [V4/V6/V7/V8]
  ✓ 脅威モデリング習得
  ✓ 改善提案 3-4件

【Q2-3】セキュリティ深掘り + TL昇格
  ✓ OWASP ASVS 全17カテゴリ
  ✓ 改善提案 10-15件
  ✓ ブログ 10-15記事
  ✓ TL 昇格確定

【Q4】グローバル発信 + CTO転職準備
  ✓ 英語記事 3-5本
  ✓ 論文 5-10本
  ✓ 転職面接準備
```

## 最終目標：2026年スタートアップCTO転職

```
年収：2,500～3,000万 + equity 2.0%
市場評価：「セキュリティ × 認証」スペシャリスト
グローバル評価：「英語で論文が読める」「AIコードのセキュリティレビューができる」

市場での立場：市場の5%以下（超稀少）
```

---

**このリポジトリで「思考の可視化」と「学習の加速」を実現します。**
