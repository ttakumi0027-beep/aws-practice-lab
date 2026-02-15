# VPC作成メモ

## 目的
- VPC及びサブネットの作成方法
- ネットワークの構築
- 

## 設計方針
- マルチAZ構成とし、耐障害性を意識
- 

## 構成図
![構成図]()

---

## 構成

- インターネットゲートウェイ構成

| IGW名 | 接続先VPC | 関連 | ルーティング |
|----|----|----|----|
| Test-igw | Test-vpc | Test-rtb-public | 0.0.0.0/0 → IGW | 

<br>

- NATゲートウェイ構成

| NAT Gateway名 | 配置サブネット | AZ | Elastic IP | 用途 |
|------|------|------|------|------|
| Test-natgw-1c | Test-public-1c | ap-northeast-1c | Test-eip-1c | Test-private-1cのアウトバウンド通信 |

<br>

-  VPC構成

| VPC名 | CIDR |
|----|----|
| Test-vpc | 10.0.0.0/16 |

<br>

- サブネット構成

| AZ | サブネット名 | 種別 | CIDR |
|----|----|----|----|
| ap-northeast-1a | Test-public-1a | Public | 10.0.0.0/24 |
| ap-northeast-1a | Test-private-1a | Private | 10.0.1.0/24 |
| ap-northeast-1c | Test-public-1c | Public | 10.0.2.0/24 |
| ap-northeast-1c | Test-private-1c | Private | 10.0.3.0/24 


<br>

- ルートテーブル構成

| AZ | ルートテーブル名 | 関連サブネット | 宛先 | ターゲット |
|----|----|----|----|----|
| 1a | Test-rtb-public     | Test-public-1a  | 0.0.0.0/0 | IGW |
| 1a | Test-rtb-natgw      | Test-private-1a | 0.0.0.0/0 | NATGW-1a |
| 1c | Test-rtb-public     | Test-public-1c  | 0.0.0.0/0 | IGW |
| 1c | Test-rtb-natgw      | Test-private-1c | 0.0.0.0/0 | NATGW-1c |

---

## 構築手順

### 1. VPCの作成
- IGWの作成
- パブリック・プライベートサブネットの作成
- ルートテーブルの紐付け


<br>

### 2. NATゲートウェイの作成
- NAT（Test-natgw-1c）ゲートウェイの作成
- パブリックサブネット（Test-public-1c）へアタッチ
- プライベートサブネットとNAT GWのルートテーブル（）の作成


---

## 学んだこと

---

## 詰まった点・要確認事項

--

## 参考
