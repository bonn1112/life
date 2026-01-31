# OWASP ASVS [V6] Authentication 学習記録

## V6 の要件一覧

### V6.1：Credential Design and Management
- [ ] 6.1.1：Password policy（最小文字数、複雑性など）
- [ ] 6.1.2：Password hashing（bcrypt/Argon2 など）
- [ ] 6.1.3：Password breach verification

### V6.2：General Authenticator Properties
- [ ] 6.2.1：Out-of-band authenticators
- [ ] 6.2.2：Multi-factor authentication
- [ ] 6.2.3：User registration

### V6.3：Authenticator Lifecycle
- [ ] 6.3.1：Token generation
- [ ] 6.3.2：Token storage
- [ ] 6.3.3：Token expiration

## MicoOne への適用

### 現在の実装状況
- ✅ Password hashing：bcrypt で実装済み
- ✅ Token generation：JWT で実装済み
- ⚠️ Token expiration：30分だが、短すぎる可能性
- ❌ Out-of-band authenticators：未実装（OTP、プッシュ通知など）

### 改善提案
1. **Token Lifetime の見直し**
   - 現在：Access Token 30分、Refresh Token 7日
   - 提案：Access Token 15分、Refresh Token 30日（より安全）
   - 優先度：P1（High）

2. **Multi-factor Authentication**
   - OTP（Time-based One-Time Password）の実装
   - プッシュ通知による認証
   - 優先度：P1（High）

3. **Password Policy の強化**
   - 最小文字数を8から12に
   - 定期的なパスワード変更の強制
   - 優先度：P2（Medium）

## 脅威モデリングとの連結

### 脅威1：Token 盗聴（Eavesdropping）
- 対策：TLS 暗号化（ASVS [V12]）
- 対策：Token Lifetime の短縮（ASVS [V6]）

### 脅威2：Credential 盗聴（Eavesdropping）
- 対策：Rate limiting（ブルートフォース対策）
- 対策：Password policy の厳格化

### 脅威3：認可情報の改ざん（Tampering）
- 対策：JWT 署名（RS256）
- 対策：署名検証の厳格化

## ブログ記事化予定
「OWASP ASVS [V6] Authentication：要件を実装で理解」
