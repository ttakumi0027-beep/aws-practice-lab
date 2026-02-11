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

-  VPC構成

| VPC名 | CIDR |
|----|----|
| Test_vpc | 10.0.0.0/16 |

<br>

- サブネット構成

| AZ | サブネット名 | 種別 | CIDR |
|----|----|----|----|
| ap-northeast-1a | public-subnet-1a | Public | 10.0.0.0/24 |
| ap-northeast-1a | private-subnet-1a | Private | 10.0.1.0/24 |
| ap-northeast-1c | public-subnet-1c | Public | 10.0.2.0/24 |
| ap-northeast-1c | private-subnet-1c | Private | 10.0.3.0/24 |

---

## 構築手順

### 1. VPCの作成




<br>

### 2. 


---

## 学んだこと

---

## 詰まった点・要確認事項

--

## 参考
