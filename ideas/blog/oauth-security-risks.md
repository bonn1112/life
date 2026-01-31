---
title: OAuth 2.0/2.1 実装のセキュリティリスク：PKCE、Token Lifetime、Scope 分離
date: 2025-02-28
tags: [OAuth, OIDC, Security, Authentication]
category: Security
---

# OAuth 2.0/2.1 実装のセキュリティリスク：PKCE、Token Lifetime、Scope 分離

## はじめに

OAuth 2.0 は「ユーザー認証」と「API アクセス権限」を管理する業界標準です。
ただ「標準」だからといって、実装すればセキュアというわけではありません。

この記事では、私が OWASP ASVS 学習を通じて発見した、OAuth 実装でよくある3つのセキュリティリスクを紹介します。

## リスク1：PKCE を実装していない

### 脅威シナリオ
- ユーザーが SPA（React / Vue など）を使用している
- Attacker が Authorization Code を盗聴する
- Attacker が Authorization Code を使って Token を取得できてしまう

### 対策：PKCE（Proof Key for Code Exchange）
PKCE は「Authorization Code」を盗聴されても、それ以上進めないようにする仕組みです。

具体的には：
1. クライアント側で「code_verifier」（ランダム文字列）を生成
2. 「code_challenge」（code_verifier のハッシュ）を Authorization Request に含める
3. Token Request で「code_verifier」を送信
4. サーバー側で「code_verifier」と「code_challenge」が一致するか検証

Attacker が Authorization Code を盗聴しても、「code_verifier」がないため Token を取得できません。

### 推奨実装
```javascript
// クライアント側
const codeVerifier = generateRandomString(128);
const codeChallenge = base64url(sha256(codeVerifier));

// Authorization Request に含める
const params = new URLSearchParams({
  client_id: CLIENT_ID,
  redirect_uri: REDIRECT_URI,
  response_type: 'code',
  scope: 'openid profile',
  code_challenge: codeChallenge,
  code_challenge_method: 'S256'
});

// Token Request
const tokenParams = new URLSearchParams({
  code: authorizationCode,
  client_id: CLIENT_ID,
  code_verifier: codeVerifier,
  grant_type: 'authorization_code'
});
```

## リスク2：Token Lifetime が不適切

### 脅威シナリオ
- Access Token が盗聴される
- Token Lifetime が長い（例：24時間）場合、24時間の間は Attacker がユーザーに成りすまして API にアクセスできる

### 対策：短い Token Lifetime と Refresh Token の組み合わせ
```
Access Token：15分（短命。盗聴されても被害が限定）
Refresh Token：30日（長命。新しい Access Token を取得に使う）
```

この構成なら：
- Access Token が盗聴されても、15分後に無効化
- Refresh Token は「安全な保管場所」に置く（HttpOnly Cookie など）

### 推奨実装
```javascript
// Token Response
{
  "access_token": "eyJhbGc...",
  "token_type": "Bearer",
  "expires_in": 900,  // 15分（900秒）
  "refresh_token": "abcdef123456...",
  "refresh_expires_in": 2592000  // 30日
}
```

## リスク3：Scope が適切に分離されていない

### 脅威シナリオ
- ユーザーが「profile 情報を読み込む」権限しか与えていない
- しかし Token で「ユーザーを削除する」API にもアクセスできてしまう

### 対策：Scope による権限の厳密な分離
```
Scope: openid profile       # ユーザー情報の読み込み
Scope: write:profile        # プロフィール更新
Scope: delete:user          # ユーザー削除（管理者のみ）
```

Token に含まれる Scope に基づいて、API で検証：
```javascript
// API 実装
app.delete('/users/:id', authenticate, authorize('delete:user'), (req, res) => {
  // ユーザー削除処理
});
```

Scope がないなら、`403 Forbidden` で拒否。

## まとめ

OAuth 2.0/2.1 実装の3つのセキュリティリスク：
1. **PKCE 未実装** → SPA で Authorization Code が盗聴される
2. **Token Lifetime が長い** → Token 盗聴の被害が大きい
3. **Scope が分離されていない** → 権限を超えたアクセスが可能

これらを対策することで、セキュアな OAuth 実装が実現できます。

## 参考資料
- OWASP ASVS [V6] Authentication
- RFC 7636（PKCE）
- OWASP Top 10：A07 Broken Authentication
