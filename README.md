# 學術酒吧 Lecture by the Glass 官網

純靜態網站（HTML＋CSS＋少量 JS），不需要 build。部署目標：GitHub → Vercel。

## 檔案結構

| 檔案 | 網址（Vercel） | 內容 |
| --- | --- | --- |
| `index.html` | `/` | 首頁；近期場次由檔案底部的 `EVENTS` 陣列產生 |
| `jinpingmei.html` | `/jinpingmei` | Vol.03《金瓶梅》12/12 場次頁（廣告素材 A 落地頁） |
| `adhd.html` | `/adhd` | Vol.04 成人 ADHD 12/19 場次頁（廣告素材 B 落地頁） |
| `assets/` | | logo、胡衍南講者照、favicon |
| `vercel.json` | | `cleanUrls`（去掉 .html），以及 `/vol3`、`/vol4`、舊檔名的轉址 |

## 開賣當天要改的地方（join1 報名連結）

兩場共用同一張 join1 報名表，網址要貼在 4 個地方：

1. `adhd.html`：`var SIGNUP_URL = "";`
2. `jinpingmei.html`：`var SIGNUP_URL = "";`
3. `index.html`：`EVENTS` 裡 Vol.03 的 `url: null`
4. `index.html`：`EVENTS` 裡 Vol.04 的 `url: null`

廣告或合作團體的連結請帶 UTM，例如：

```
https://<你的網域>/adhd?utm_source=meta&utm_medium=paid&utm_campaign=dec2026&utm_content=b_adhd
```

## Repo 與 vault 的關係

這個資料夾是**獨立的 git repo**，remote 是 [danielthhsieh/Lectures_bytheGlass](https://github.com/danielthhsieh/Lectures_bytheGlass)。它實體上放在 Obsidian vault 裡，但 vault 根目錄的 `.gitignore` 已經排除 `lbtg-site/`，所以 vault repo 不會追蹤這裡的檔案，兩個 repo 各自 commit、各自 push。

## 推送到 GitHub（danielthhsieh 帳號）

remote URL 已帶上帳號名稱（`https://danielthhsieh@github.com/...`），git 會用 danielthhsieh 去 macOS 鑰匙圈找憑證，不會誤用公司的 GitHub 帳號。

```bash
git push -u origin main
```

第一次推送會要求密碼：請貼 **Personal Access Token**，不是 GitHub 登入密碼。取得方式：用 danielthhsieh 登入 GitHub → Settings → Developer settings → Personal access tokens → Fine-grained tokens → Generate new token，Repository access 只選 `Lectures_bytheGlass`，Permissions 的 Contents 設 **Read and write**。輸入一次後鑰匙圈會記住。

不想用終端機的話，也可以用 GitHub Desktop（以 danielthhsieh 登入）→ File → Add Local Repository → 選這個資料夾 → Push origin。

## 第一次部署到 Vercel

1. 用 danielthhsieh 的 GitHub 帳號登入 Vercel → **Add New… → Project** → Import `Lectures_bytheGlass`。
2. Framework Preset 選 **Other**；Build Command、Output Directory 都留空 → **Deploy**。
3. 部署完成後，在 Vercel 專案的 **Settings → Domains** 綁定網域（若有）。

## 之後更新

```bash
git add -A
git commit -m "說明這次改了什麼"
git push
```

Vercel 會在每次 push 到 `main` 後自動重新部署，約 1 分鐘生效。

## 上線前待確認

- [ ] Vol.04 標題「為什麼他（或我）很努力，看起來卻像不夠努力？」、量表環節、90 分鐘流程：待陳瑜慧心理師確認（〈Vol.4 活動整體樣態規劃〉doc 第 8.1、9 節）
- [ ] 首頁 FAQ「票買了可以退嗎」寫「售出後不接受退換」，但兩個場次頁寫「活動開始前皆可申請取消與退費」，需依 join1 實際設定統一
- [ ] 票價與票種（作戰總覽 4.2 節仍標「待主辦方拍板」）
- [ ] 12/12、12/19 的開始時間（目前沿用 14:00–15:30）
- [ ] 分享預覽圖（`og:image`，1200×630）：三頁都還沒有，做好後放進 `assets/`，在各頁 `<head>` 加 `<meta property="og:image" content="https://<網域>/assets/xxx.png">`
- [ ] 分析工具（GA4 或 Plausible）、Meta Pixel
