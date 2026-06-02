# 部署到 Cloudflare Pages · 三步走

git 已經初始化好了，所有 19 個檔案已經 commit。接下來只需要：

## 步驟 1 · 建立 GitHub repo（30 秒）

1. 開瀏覽器到 [https://github.com/new](https://github.com/new)
2. **Repository name** 填：`rerum-novarum`
3. 設為 **Public**（Cloudflare Pages 免費方案需要）
4. **不要**勾選 "Add a README" / .gitignore / license
5. 按 **Create repository**
6. 建好後您會看到一個畫面，複製那個畫面上的 HTTPS 網址（長這樣 `https://github.com/bigtaffy/rerum-novarum.git`）

## 步驟 2 · 推送到 GitHub（一行指令）

打開 Mac 的 **Terminal**（Spotlight 搜「Terminal」），貼上以下指令，**把 `https://github.com/XXX/rerum-novarum.git` 換成您剛複製的網址**：

```bash
cd ~/Downloads/通諭專題網用圖 && \
git remote add origin https://github.com/XXX/rerum-novarum.git && \
git branch -M main && \
git push -u origin main
```

第一次推送時 Terminal 會問您 GitHub 帳密——輸入 GitHub username 與 **Personal Access Token**（不是 GitHub 密碼，是 token）。

如果還沒有 token：
- 開 [https://github.com/settings/tokens/new](https://github.com/settings/tokens/new)
- Note 填 `cloudflare-deploy`
- Expiration 選 90 days
- 勾選 `repo` 權限
- 按 Generate token，複製那一長串字元（只會出現一次！）
- 回到 Terminal 把它貼上當密碼

## 步驟 3 · 連到 Cloudflare Pages（1 分鐘）

1. 開 [https://dash.cloudflare.com](https://dash.cloudflare.com)
2. 左側 **Workers & Pages** → 右上角 **Create**
3. 選 **Pages** 分頁 → **Connect to Git**
4. 第一次的話會要您授權 GitHub，按照畫面同意即可
5. 選剛建好的 `rerum-novarum` repo
6. 按 **Begin setup**
7. 在「Set up builds and deployments」畫面：
   - **Project name**：`rerum-novarum`（或您喜歡的名字，這會成為網址）
   - **Production branch**：`main`
   - **Build command**：**留空**
   - **Build output directory**：**留空**（或填 `/`）
8. 按 **Save and Deploy**

約一分鐘後，網站就會出現在 `https://rerum-novarum.pages.dev`

---

## 關於 URL · `events.mai-li.app/encyclical/rerum-novarum/`

上面這套流程會把網站部署在 `https://rerum-novarum.pages.dev`，跟《偉大的人類》的 `events.mai-li.app/encyclical/magnifica-humanitas/` 路徑不一致。

要做到一致的 URL 有兩個做法：

### 做法 A · 加入既有 Pages 專案的 repo
找到「magnifica-humanitas 那個網站」對應的 GitHub repo，把這份內容放在 `encyclical/rerum-novarum/` 子資料夾下，推進去即可。需要那個 repo 的網址。

### 做法 B · 自訂網域映射
保留現在的部署，在 Cloudflare Pages 的 **Custom domains** 把它接到 `rerum-novarum.mai-li.app`。需要您有 `mai-li.app` 的 DNS 管理權。

### 做法 C · 暫時就用 `rerum-novarum.pages.dev`
之後想搬家再搬。
