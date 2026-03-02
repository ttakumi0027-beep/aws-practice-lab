# ELB設計・構築メモ

<br>

## 目的

- ALBによる負荷分散
- ASGによるオートスケーリング作成
- RDSのレプリカ構築

---

## 設計方針

- 単一障害点をなくす
- ALBによる高可用性
- マルチAZ構成による可用性の確保
- ネットワークの分離

---

## 構成図
![構成図](../images/ELB_architect.png)

---

## 構成

- インターネットゲートウェイ構成

| IGW名 | 接続先VPC | 関連 |
|----|----|----|
| Test-igw | Test-vpc | Test-rtb-public |

<br>

- NATゲートウェイ構成

| NAT Gateway名 | 配置サブネット | AZ | Elastic IP | 用途 |
|------|------|------|------|------|
| Test-natgw | Test-public-1a | ap-northeast-1a | Test-eip-1a | Test-private-1aのアウトバウンド通信 |

<br>

-  VPC構成

| VPC名 | CIDR |
|----|----|
| Test-vpc | 10.0.0.0/16 |

<br>

- サブネット構成

| AZ | サブネット名 | 種別 | CIDR |
|----|----|----|----|
| ap-northeast-1a | Test-public-1a  | Public | 10.0.0.0/24 |
| ap-northeast-1a | Test-private-1a | Private | 10.0.1.0/24 |
| ap-northeast-1c | Test-public-1c  | Public | 10.0.2.0/24 |
| ap-northeast-1c | Test-private-1c | Private | 10.0.3.0/24 |

<br>

- EC2構成

| AZ | インスタンス名 | 関連サブネット |
|----|----|----|
| 1a | Test-web-1a  | Test-public-1a  |
| 1a | Test-rds-1a  | Test-private-1a |
| 1c | Test-web-1c  | Test-public-1c  |

<br>

- S3構成



---

## 構築手順

### 1. VPC/サブネットの作成

- VPC/サブネット/IGW/NATの作成
- S3バケット（test-vpc-20260302）の作成

### 2. EC2の作成

- Webサーバ（Test-web-1a）の作成　→ 起動時に下記のシェルの実行

<details>
<summary>シェル</summary>

```bash
#!/bin/bash

# サーバーの設定変更
hostnamectl set-hostname Test-bash
timedatectl set-timezone Asia/Tokyo
localectl set-locale LANG=ja_JP.UTF-8

# Apacheのインストール
sudo yum update -y
sudo yum install httpd -y
sudo systemctl start httpd
sudo chkconfig httpd on

# index.htmlの設置
aws s3 cp s3://test-vpc-20260302/index.html /var/www/html

```

</details>

<details>
<summary>シェルの確認</summary>

```bash
# httpdがインストールされていること
yum list installed | grep httpd

# httpdが起動していること
systemctl status httpd

# ホスト名が、Test-bashであること
cat /etc/hostname 

# Asia/Tokyoが表示されていること
ls -la /etc/localtime 

# LANG=ja_JP.UTF-8が表示されていること
cat /etc/locale.conf 

# index.htmlが確認できること
ls -la /var/www/html/index.html
```

</details>

- AMI（test-vpc-web-server）の作成
- Webサーバ（Test-web-1c）をAMIより作成

---

## 学んだこと

- 

---

## 詰まった点・要確認事項


--

## 参考



---
