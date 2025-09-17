

# 🛡️ Greenbone Community Edition (GCE)

[![Docker](https://img.shields.io/badge/Docker-Compose-blue?logo=docker)](https://www.docker.com/)
[![Greenbone](https://img.shields.io/badge/Greenbone-Community%20Edition-00A859?logo=greenbone)](https://www.greenbone.net)
[![License](https://img.shields.io/badge/License-GPLv3-orange)](https://www.gnu.org/licenses/gpl-3.0.html)
[![Platform](https://img.shields.io/badge/Platform-Windows%2010%2F11%20%7C%20WSL2-lightgrey)](#)

---

## 📖 工具介紹

* **名稱**：Greenbone Community Edition (GCE)
* **用途**：進行主機、網段、系統的弱點掃描與管理，偵測 CVE 漏洞、評估資安風險
* **功能簡述**：

  * 支援掃描本地與遠端主機的已知漏洞
  * 可產出報告、評估 CVSS 分數、匯入自訂掃描政策
  * 擁有 Web GUI，可透過瀏覽器操作
* **官方網站**：[Greenbone](https://www.greenbone.net)
* **官方文件**：

  * [Source Build](https://greenbone.github.io/docs/latest/22.4/source-build/index.html)
  * [Container 部署](https://greenbone.github.io/docs/latest/22.4/container/index.html)
* **授權模式**：開源社群版本（非商業授權）

---

## ⚙️ 環境資訊

* **作業系統**：Windows 10/11（以 WSL2 模式執行 Docker 引擎）
* **Docker**：本機已安裝（非透過 WSL 安裝）
* **管理工具**：Git + Docker Compose

---

## 🚀 安裝與部署步驟

```powershell
# 建立專案資料夾
PS D:\Docker> mkdir greenbone-community-container
PS D:\Docker> cd greenbone-community-container

# 下載官方 Docker Compose 設定檔
curl -o docker-compose.yml https://greenbone.github.io/docs/latest/_static/docker-compose-22.4.yml

# 啟動所有容器
docker compose up -d

# 檢查容器狀態
docker compose ps

# 設定初始密碼（更改預設 admin 密碼）
docker compose exec -u gvmd gvmd gvmd --user=admin --new-password='YourPasswordHere'
```

👉 Web 介面登入： [https://127.0.0.1:9392](https://127.0.0.1:9392)
👉 預設帳號：`admin / 你設定的密碼`

<img width="865" height="419" alt="image" src="https://github.com/user-attachments/assets/d43b3e64-afbd-4257-a3aa-00d1a47bb07f" />

>底下是四個資料庫盡量Status都要是current，不要出現old不然就不是最新的資料了
>
---

## 📦 部署架構（Docker Compose 管理）

容器服務模組包括：

* **gvmd**（管理核心）
* **openvas / ospd-openvas**（掃描引擎）
* **scap-data / cert-bund-data / dfn-cert-data**（資安資料庫）
* **gsa**（Web GUI）
* **pg-gvm**（PostgreSQL 資料庫）
* **redis-server**（快取與任務排程）
* **vulnerability-tests / report-formats / gpg-data**（其他 Feed 資料）

---

## 🔐 安全性與信任來源

* 所有映像皆來自 **Greenbone 官方 Docker Registry**：
  `registry.community.greenbone.net/...`
* 資料來源包含：

  * **CVE**（MITRE、NIST）
  * **CPE、OVAL 標準格式**
  * **DFN-CERT、CERT-Bund 安全通報**

---

## 📌 建議與後續

* 建議在 **內部網段** 測試掃描，避免外洩敏感資訊
* 每日監控 **Feed 更新狀況**（檢查資料庫是否為 `current` 狀態）
* 確保所有模組與漏洞資料庫保持最新

---

