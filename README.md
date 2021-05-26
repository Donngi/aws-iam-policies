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
