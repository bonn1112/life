# OAuth 2.1 仕様書読書記録

## 参考資料
- 公式：https://datatracker.ietf.org/doc/draft-ietf-oauth-v2-1/
- RFC 6749：https://datatracker.ietf.org/doc/html/rfc6749
- RFC 7636（PKCE）：https://datatracker.ietf.org/doc/html/rfc7636

## 読書進捗
- [ ] 1. 概要（Introduction）
- [ ] 2. Protocol Flow
- [ ] 3. Authorization Request
- [ ] 4. Token Endpoint
- [ ] 5. Security Considerations（重要）

## 主要な気づき

### 1. PKCE の重要性
- **なぜ必要か**：クライアントが credential を持たない場合（モバイル、SPA）、code を盗聴されると Token を取得されてしまう
- **仕組み**：code_challenge を使って、code を盗聴されてもそれ以上進めないようにする
- **MicoOne への適用**：SPA クライアントなら PKCE は必須

### 2. Token Lifetime について
- Access Token：短命（15分～1時間）
- Refresh Token：長命（日～月単位）
- **トレードオフ**：短いほどセキュアだが、ユーザー体験が悪い

### 3. Scope（権限範囲）
- OAuth は「ユーザーが何を認可するか」を管理する
- つまり「その Token でどこまでアクセスできるか」は Scope で制御
- MicoOne では「tenant ごとに Scope を分離する」が重要

## 実装検証（MicoOne）
- [ ] PKCE が実装されているか確認
- [ ] Token Lifetime の設定が適切か確認
- [ ] Scope の分離が適切か確認
- [ ] Security Considerations の項目を全てチェック

## ブログ記事化予定
「OAuth 2.1 セキュリティ完全ガイド：PKCE、Token Lifetime、Scope 理解」

## 関連する OWASP ASVS
- V4：API and Web Service Security
- V6：Authentication
- V10：OAuth and OIDC
