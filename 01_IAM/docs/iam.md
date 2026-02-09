# IAMユーザ・グループ作成メモ

## 目的
IAMユーザの作成方法及び意義を学ぶため。

## 構成図
![構成図]()

---

## 構成

IAMユーザ構成

| ユーザ名 | 役割 | 権限 |
|----|----|----|
| admin                 | 管理者  　　 | Admin権限を付与  　　　　　　　　　　　　|
| Operator1             | 運用管理者   | 運用ツールや開発環境のアクセスを付与  　　|
| engineer1, engineer2  | 開発者  　　 | アプリ開発環境のみアクセスを付与  　　　　|

<br>

IAMグループ構成

| グループ名 | 所属メンバー |
|----|----|
| admin       | admin |
| Operation   | Operator1 |
| Application | engineer1, engineer2 |

<br>

ポリシー構成
| ポリシー名 | フルアクセス権限 |
|----|----|
| Administrator | フルアクセス |
| Oeration      | EC2、ELB、Autoscaling、RDS、S3、Clooud Watch、Cloud Trail、Config |
| Apllication   | EC2、ELB、Autoscaling、RDS、S3 |

---

## 構築手順

### 1. IAMポリシーの作成

### 手順

1. Application（カスタムポリシー）の作成<br>
EC2、ELB、Autoscaling、RDS、S3のフルアクセス権限付与
   
2. Oeration（カスタムポリシー）の作成<br>
Clooud Watch、Cloud Trail、Configのフルアクセス権限付与

<br>

### 2. IAMグループ・ユーザの作成

### 手順

1. Applicationグループを作成<br>
   Applicationポリシーを設定
   
2. Operationグループを作成<br>
   Application、Operationポリシーを設定
   
4. engineer1, engineer2の作成<br>
   Apllicationグループに追加
   
5. Operator1の作成<br>
   Operationグループに追加

---

## 学んだこと
- IAMポリシーはユーザ、グループ、ロールに適用する。
- IAMグループは複数のIAMユーザに権限を効率的に設定できる。
- IAMロールはAWSリソースに適用する。また、別のAWSアカウントのIAMユーザにアクセス権限を委譲可。
- ルートユーザでAWSサービスを使うことはなく、基本的にIAMユーザを使うこと。
- インラインポリシーは、一つのアイデンティティ（ユーザ、グループ、ロール）にしか適用不可。逆に管理ポリシーは使い回し可。
- 信頼ポリシーは、特定のユーザやリソースのアクセスを許すためのポリシー。権限の委譲など。
---

## 詰まった点・要確認事項
- IAMポリシー（JSON形式）の記述方法や何を意味するのかを確認する、主に以下。
  - Statement　ポリシーを記載することを宣言、複数可
  - Principal  適用するアカウント・ユーザ。ロールを指定
  - Action     特定のリソースに対する許可・否定の宣言
  - Resource   Actionで設定したリソース一覧
  - Condition  ポリシーの対象を絞る設定。（IPアドレスの制限など）
--

## 参考
