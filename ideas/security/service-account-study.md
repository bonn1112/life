# Service Account 設計学習記録

## 目的
MicoOne Service Account機能の設計・実装をリードするため、
OAuth 2.0 M2M認証の業界標準と実装パターンを習得する。

## 学習リソース

### RFC（必読）
- [ ] RFC 6749 Section 4.4 - Client Credentials Flow
- [ ] RFC 9068 - JWT Profile for OAuth 2.0 Access Token
- [ ] RFC 7592 - OAuth 2.0 Dynamic Client Registration Management
- [ ] RFC 6819 - OAuth 2.0 Security Considerations
- [ ] RFC 8725 - JWT Best Current Practices

### 業界実装調査
- [ ] Auth0 M2M (Machine-to-Machine)
- [ ] Okta Service Apps / API Services
- [ ] Microsoft Entra ID Workload Identity
- [ ] Google Cloud Service Accounts
- [ ] AWS IAM Roles (比較参考)

## 設計パターン

### 1. 認証フロー
- Client Credentials Flow
- Token発行エンドポイント設計
- Secret生成・ハッシュ化（bcrypt）

### 2. 認可モデル（3層権限モデル）
- Layer 0: Feature Flag Matrix（Human User & SA共通）
- Layer 1: Scope定義 + visible flag（コードレベル）
- Layer 2: 動的DB設定（Product Admin選択）

### 3. Scope設計
- gRPC 1:1マッピング（各gRPCメソッド = 1スコープ）
- visible flagの用途（選択可能なスコープを制御）
- Permission Templates（スコープのバンドル化）

### 4. JWT構造
- RFC 9068準拠（scope claim = space-separated string）
- Human User JWT: { ma, mo, mt }
- SA JWT: { sub, scope, tpl, client_id }
- 統一認証アプローチ（Layer 0共通）

## MicoOneへの適用

### 既存インフラ活用
| コンポーネント | 再利用 | 備考 |
|---------------|:-----:|------|
| JWTService.sign()/verify() | ✅ | payloadタイプのみ新規 |
| JtiManager | ✅ | SA用トークン管理 |
| AuthenticationInterceptor | 拡張 | UnifiedAuthInterceptor |
| RequestContextService | 拡張 | isServiceAccount(), getOperatorId() |

### 設計判断
| 項目 | 判断 | 根拠 |
|------|------|------|
| 認証フロー | Client Credentials | RFC 6749 |
| JWT構造 | 別々 | 既存影響最小化 |
| Scope形式 | Space-separated | RFC 9068 |
| Tenant境界 | DB lookup（tpl flag） | 即時反映、無制限 |
| Layer 0 | Human/SA共通 | 技術負債回避 |

## 脅威モデリング（STRIDE）

### Spoofing（なりすまし）
- [ ] Client Secret の漏洩対策
- [ ] Token 盗聴への対策

### Tampering（改ざん）
- [ ] JWT 署名検証
- [ ] Scope の改ざん防止

### Repudiation（否認）
- [ ] 監査ログの設計
- [ ] Token 発行・使用履歴

### Information Disclosure（情報漏洩）
- [ ] Secret の安全な保管
- [ ] Token の最小権限原則

### Denial of Service（サービス拒否）
- [ ] Rate Limiting
- [ ] Token 発行制限

### Elevation of Privilege（権限昇格）
- [ ] Scope 検証の厳格化
- [ ] Tenant 境界の検証

## 確認事項
- [ ] 「統一」の範囲（Layer 0のみ or JWT構造も）
- [ ] 3層モデルの詳細実装イメージ
- [ ] 既存Human User認証への影響有無

## ブログ記事化予定
1. 「OAuth 2.0 Client Credentials Flow 完全ガイド」
2. 「Service Account設計：Auth0/Okta/Entra ID比較」
3. 「M2M認証のセキュリティベストプラクティス」
