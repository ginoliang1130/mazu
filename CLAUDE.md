# CLAUDE.md — mazu 專案指引

## 專案簡介

2026 白沙屯媽祖進香任務地圖，純靜態網站（HTML + CSS + JS），部署在 GitHub Pages。

## 檔案結構

```
index.html   — 頁面結構，無 build 步驟，直接開瀏覽器可用
styles.css   — 所有樣式
app.js       — 所有邏輯與資料（APP_DATA、render 函式、state）
```

## 部署

推到 `main` branch 自動觸發 GitHub Actions（`.github/workflows/deploy-pages.yml`）：

1. `sed` 將 `app.js` 裡的 `__GOOGLE_MAPS_EMBED_API_KEY__` 替換成 GitHub Secret
2. 產出的 `dist/` 部署到 GitHub Pages

**不要把 API key 直接寫進 source code。** key 只存在 GitHub Secret，由 CI 注入。

## Google Maps Embed

- 使用正式 Embed API：`https://www.google.com/maps/embed/v1/search?key=...`
- API key 需在 GCP Console 的 HTTP referrers 白名單加入 `https://ginoliang1130.github.io/*`
- 本地開發時 key 是 placeholder，地圖 iframe 會被隱藏，屬正常行為

## 開發習慣

- 每次修正完直接 `commit` 並 `push`，不需要等確認
- 版本號在 `index.html` 的 CSS/JS query string（`?v=YYYYMMDD-N`），有改動時一起更新
