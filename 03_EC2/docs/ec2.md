# EC2設計・構築メモ

## 目的
- EC2インスタンスのバックアップの仕方
- 

## 設計方針
- コストの最適解
- 運用を意識した構成


## 構成図
![構成図](../images/IAM_architect.png)

---

## 構成

- EC2構成

| インスタンス名 | 配置サブネット | AZ |　用途 |
|------|------|------|------|
| Web-server-1a | Test-public-1a | ap-northeast-1a | Apacheサーバ |
| DB-server-1a | Test-public-1c | ap-northeast-1a  | DBサーバ |

<br>

- セキュリティグループ構成

| Direction | Protocol | Port | Source/Destination | 用途 |
|------------|----------|------|--------------------|------|
| Inbound    | TCP      | 22   | 0.0.0.0/0          | SSH接続 |
| Inbound    | HTTP     | 80   | 0.0.0.0/0          | Web通信 |
| Inbound    | HTTPS    | 443  | 0.0.0.0/0          | Web通信 |
| Outbound   | All      | All  | 0.0.0.0/0          | 外向き通信許可 |

<br>

- その他構成は下記のセクションで使用したリソースを引用（構成を参照）

[02_VPC/docs/vpc.md](https://github.com/ttakumi0027-beep/aws-practice-lab/blob/main/02_VPC/docs/vpc.md)

---

## 構築手順

### 1. EC2インスタンス

- インスタンス（Web-server-1a）の作成
- Apacheのインストール

**実行コマンド**

```bash
# Apacheのインストール
yum install httpd -y

# httpdを自動起動に設定
systemctl enable httpd
```

- index.htmlファイルの作成

<details>
<summary>index.htmlの中身</summary>
  
```/var/www/html/index.html
<html>
<h1>Hello, World</h1>
</html>
```

</details>

- Webブラウザより表示されていることを確認

---

## 学んだこと

- 

---

## 詰まった点・要確認事項

--

## 参考

---
