# 學術酒吧 Lectures by the Glass 官網

純靜態網站（HTML＋CSS＋少量 JS），不需要 build。部署目標：GitHub → Vercel。

## 檔案結構

| 檔案 | 網址（Vercel） | 內容 |
| --- | --- | --- |
| `index.html` | `/` | 首頁；近期場次由檔案底部的 `EVENTS` 陣列產生 |
| `jinpingmei.html` | `/jinpingmei` | 12/12「酒色財氣：從《金瓶梅》學會職場降妖術」場次頁 |
| `adhd.html` | `/adhd` | 成人 ADHD 場次頁，**日期待公布、目前隱藏**：首頁與金瓶梅頁都不連過來，`<head>` 設 `noindex`（11/14 決定延到 2027 年 1 月） |
| `assets/` | | logo、胡衍南講者照、favicon、首頁 hero 底圖 `venue.jpg`（Drizzle 空場照，模糊後當底） |
| `vercel.json` | | `cleanUrls`（去掉 .html），以及 `/vol3`、`/vol4`、舊檔名的轉址 |

## 視覺

三頁都套用〈學術酒吧 Brand Visual Guideline〉（2026.11，`PDF export/` 內）：漸層底（首頁 G1、金瓶梅 G2、ADHD G4）、模糊實拍、一個主光、顆粒、Paper 膠囊按鈕。共用樣式在每頁 `<style>` 最後的「品牌視覺」區塊，三頁內容相同，改一頁要同步另外兩頁。場次一律寫「下一杯／NEXT GLASS」，不用 Vol. 編號。頁尾酒類警語帶保留（官網是廣告落地頁）。

## join1 報名連結

12/12《金瓶梅》場：`https://join1.app/event/NEG0TB`，已填在 `jinpingmei.html` 的 `SIGNUP_URL` 與 `index.html` 的 `EVENTS`。

成人 ADHD 場日期定案後：

1. `adhd.html`：填 `var SIGNUP_URL`，改 hero 的日期、票種區，拿掉 `<meta name="robots" content="noindex, nofollow">`
2. `index.html`：在 `EVENTS` 加回這一場，並更新「一場怎麼進行」的場次卡
3. `jinpingmei.html`：視需要在頁底「之後的場次」加回連結

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

- [ ] 成人 ADHD 場：日期、標題「為什麼我明明很努力，看起來卻像不夠努力？」、量表環節、招牌互動與酒單：待和陳瑜慧心理師確認（見〈IG 上線貼文盤點與發展原則（1114）〉第 5 節）
- [ ] 金瓶梅 Part 1–4 的講綱（特別是「小人的職場生存學」）：待透過 Chris 和胡教授確認
- [x] 退費規則改為新規（11/14，以 join1 為準）：票券售出後不退換、不延用，可轉讓給親友（活動前私訊 IG 或官方 Line 更名）；首頁、金瓶梅、ADHD 三頁 FAQ 與票種區已同步
- [x] 金瓶梅票種：早鳥 999 元（12/5 前）、原價 1,199 元（12/6 起），含兩杯葡萄酒（每杯 60ml）或一杯無酒精特調；不推雙場聯票
- [ ] 12/12 的開始時間（目前沿用 14:00–15:30）
- [ ] 分享預覽圖（`og:image`，1200×630）：三頁都還沒有，做好後放進 `assets/`，在各頁 `<head>` 加 `<meta property="og:image" content="https://<網域>/assets/xxx.png">`
- [ ] 分析工具（GA4 或 Plausible）、Meta Pixel
