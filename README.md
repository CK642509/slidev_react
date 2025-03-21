# Slidev 簡報

這是[《React 思維進化》讀書會](https://github.com/Tech-Book-Community/Zet-React-Book)的簡報，於 2025.03.18 進行分享，內容包含 2-7 ~ 2-9。

- 使用 [Slidev](https://sli.dev/) 製作
- 部屬於 Vercel，可以線上查看簡報 ([連結](https://slidev-react-20250318.vercel.app))

## 如何使用
### 1. 安裝
```
npm install
```
### 2. 啟用
```
npm run dev
```
### 3. 查看簡報
進入 `http://localhost:3030` 查看簡報

## 專案架構說明
- 簡報在 `slides.md`
- 官方範例在 `example.md` (備用)
- 所有簡報的統一設定 (e.g. 頁碼) 在 `global-top.vue`
- 簡報中的圖片在 `public` 資料夾，圖片是使用 [draw.io](https://www.drawio.com/) 繪製的

## Vercel 部屬注意事項
之前曾遇過一個狀況，在 local 執行 `slidev build` 沒問題，部屬上 Vercel 卻 build 失敗。最後參考這個[回答](https://github.com/slidevjs/slidev/issues/322#issuecomment-1233058507)，將 Framework Preset 改成 Vite 就沒問題了。