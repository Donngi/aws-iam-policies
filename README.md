# aws-iam-policies
利用頻度の高いIAM Policyのまとめ

## MFA強制ポリシー(force-mfa.json)
MFA突破前に実施できる操作を大幅に絞る。

MFA突破前でも実施可能な操作
- パスワード変更
- MFA端末の新規追加
- 既存MFA端末の再同期

MFA突破後に実施可能な操作
- ↑の操作
- 既存MFA端末の削除

※明示的なDenyで絞っているため、他のIAM Policyやリソースポリシーが存在していても、MFA前にできる操作は↑のみとなるので注意

※※カスタマイズする場合は、Condition句の条件に要注意。組み合わせを誤ると、MFAチェックが有効に働かなくなってしまう。
参考: [aws:MultiFactorAuthPresent](https://docs.aws.amazon.com/ja_jp/IAM/latest/UserGuide/reference_policies_condition-keys.html#condition-keys-multifactorauthpresent)

## アクセスキー管理権限コントロールポリシー(\*-access-key-\*.json)
アクセスキーの発行、削除、アクティブ/非アクティブ化の管理権限をコントロールする。
3種類のポリシーのいずれかを必ずアタッチする想定。

### 1️⃣ allow-create-access-key.json
全操作を許可。

### 2️⃣ deny-manage-access-key-except-existing-key.json
既存のアクセスキーの削除、アクティブ/非アクティブ化のみ可能。
新規発行はできない。

※非アクティブ化されたキーの、再有効化ができてしまう点に注意

### 3️⃣ deny-manage-access-key-strict.json
全操作を禁止。
