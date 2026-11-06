# 糯糯 — 沉浸式搗麻糬

使用 Next.js、React 和 Three.js 製作的響應式 3D 搗麻糬小玩具。

**線上體驗：[糯糯 Mochi Moment](https://mochi-moment.hitmochi.workers.dev/)**

- 單人模式：點按或空白鍵敲擊，長按連續敲擊，自動模式
- 雙人同屏：A / L 鍵分工敲擊與翻面，可交換左右手
- 原味、抹茶、草莓配色，局部拉扯與回彈動畫
- 可旋轉、縮放的 3D 視角及重設功能
- 繁體中文、日本語、한국어
- 響應式介面與可關閉的合成音效

## 本機執行

```sh
npm ci
npm run dev
```

開啟 http://localhost:3000 。

## 正式部署

目前部署於 Cloudflare Workers，以 Next.js 靜態匯出方式提供網站，不需要資料庫或應用程式環境變數。

- `next.config.mjs` 設定 `output: 'export'`，建置產物在 `out/`。
- `wrangler.jsonc` 設定建置命令 `npm run build` 與靜態資源目錄 `./out`。
- Cloudflare 已連接本倉庫；推送至 `main` 後自動建置部署。
- Cloudflare 建置設定：根目錄 `/`，獨立 Build command 留空，Deploy command 為 `npx wrangler deploy`（由 Wrangler 執行建置）。

手動部署時，先完成 Cloudflare CLI 登入，再執行：

```sh
npm ci
npx wrangler deploy
```

只檢查正式建置可執行 `npm run build`。靜態匯出不使用 `npm start` 啟動正式服務。

## 模型

public/models 包含三份壓縮後的 GLB，合計約 16 MB。貼圖採用 WebP，最高 1024px；木臼與木槌經減面，麻糬保留頂點以支援程式變形。需支援 WebGL 的現代瀏覽器。

雙人模式為同屏操作，並非遠端連線。計數在重新載入後重設；語言偏好保存在本機瀏覽器。

## 後續計畫

- 優化模型載入速度：木槌與木臼進一步減面、幾何壓縮及載入體驗改善。目前三份模型合計約 16 MB，首次載入較依賴網路速度。
- 增加木槌樣式及更多麻糬配色。
- 購買自訂網域後綁定現有 Cloudflare Worker。
