# Yosukeさん：2026年スタートアップCTO への道

## 基本情報
- 職種：認証基盤エンジニア（MicoOne）
- 経験：8ヶ月（認証基盤）
- 強み：設計・判定・批判能力（AIコード レビューができる）
- 英語力：得意（一次資料を読める）

## 最終目標
**2026年Q1-2：セキュリティスタートアップ CTO 転職**
- 年収：2,500～3,000万 + equity 2.0%
- 市場価値：「セキュリティ × 認証」スペシャリスト

## 🔥 最優先テーマ（2月最重要）

### Service Account（SA）のセキュアな実装
**なぜ最優先か：**
- マイクロサービス間の認証基盤の核
- OAuth 2.0 Client Credentials flow の深い理解が必須
- MicoOne での脆弱性の可能性が高い
- セキュリティ脅威が極めて高い（権限昇格のリスク）

**学習内容：**
- RFC 6749 "Client Credentials" Grant Type
- PKCE と Client Credentials の関係性
- Client Secret の管理・回転・監査ログ
- Service Account と User Account の分離（ASVS [V6]）
- マルチテナント環境での SA 隔離
- 脅威モデリング：SA Token の盗聴・改ざん・冒認

**成果物（2月末までに）：**
- ideas/security/service-account-study.md（完成）
- 脅威分析ドキュメント
- ブログ記事「Service Account のセキュアな実装」
- セキュリティ改善提案 2-3件

## 2025年のマイルストーン

### Q1（1-3月）
- ✓ **Service Account セキュリティ習得（最優先）**
- ✓ OWASP ASVS [V4/V6/V7/V8] 習得
- ✓ 脅威モデリング（STRIDE）習得
- ✓ 徳丸本「第3,4,5章」読破
- ✓ セキュリティ改善提案 5-7件実装（SA関連を含む）

### Q2-3（4-9月）
- ✓ OWASP ASVS 全17カテゴリ習得
- ✓ 脅威モデリング（MicoOne 全体）完成
- ✓ セキュリティ改善提案 10-15件実装
- ✓ **TL 昇格確定**
- ✓ ブログ 10-15記事発信

### Q4（10-12月）
- ✓ 英語でセキュリティ記事 3-5本発信（Medium）
- ✓ OWASP コミュニティ翻訳貢献
- ✓ セキュリティ論文 5-10本読破
- ✓ CTO 転職面接準備

## 得意なスキル
- OAuth 2.0 / OIDC / PKCE 実装
- **Service Account 設計と実装** ⭐ 最優先
- マルチテナント IAM 設計
- 分散トランザクション処理
- **AIコードのセキュリティレビュー** ★★★★★
- 英語での一次資料読解

## 改善対象（2025年で解決）
- Service Account セキュリティ深掘り → 2月末までに完全習得 ⭐
- セキュリティ体系的知識（OWASP ASVS）→ 2月末完全習得
- セキュリティ論文の読解 → Q3-Q4強化
- 英語での発信（Medium）→ Q4開始

## 興味領域（優先度順・更新版）
1. **Service Account / Client Credentials** ⭐ 最優先
2. セキュリティ → OAuth / OIDC → 認証基盤 → マルチテナント
3. AI × セキュリティ → AI生成コードのレビュー → 脅威分析
4. スタートアップ経営 → ファンディング → チーム構築
5. 技術発信 → ブログ（日本語）→ Medium（英語）→ カンファレンス

## 技術スタック
- 認証：OAuth 2.0 / OIDC / PKCE / Client Credentials
- 言語：TypeScript / NestJS / Node.js
- インフラ：gRPC / Kubernetes / AWS
- ツール：Threat Modeling Tool / Burp Suite / Claude Code

## 学習方針（Service Account 版）
1. RFC 6749 "Client Credentials" を「最初に」読む
2. Service Account の脅威モデリング（STRIDE）実施
3. OWASP ASVS [V6] との対応付け
4. 徳丸本で実装パターンを理解
5. MicoOne での現在の実装をレビュー
6. 改善提案を実装・テスト・ドキュメント化

## 重要な認識
- 「AI無しで書けない」は問題ではない = 設計優先の証
- 「セキュリティ × 英語」ができる人 = 市場5%以下（超稀少）
- **「Service Account セキュリティ」は採用面接で必ず出る質問**
  → 2月末に「完全に答えられる状態」にする
- 2026年採用市場では「設計・判定・批判」能力が最重要

## 参考リソース
- RFC 6749 Section 4.4: Client Credentials Grant
- OWASP ASVS [V6]：Authentication
- 徳丸本「第3,4,5章」（特に認可周り）
- Google Cloud SA セキュリティガイド
- AWS IAM Best Practices

## ファイル参照
- ideas/security/service-account-study.md ← **最優先で完成させる**
- ideas/security/oauth-2.1-study.md
- ideas/security/owasp-asvs-v6-authentication.md
- ideas/blog/service-account-security.md ← ブログ記事化
