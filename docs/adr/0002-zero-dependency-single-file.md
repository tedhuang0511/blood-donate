# 維持零依賴的單一 HTML 檔

整個網站是一個 `index.html`：HTML、CSS、JavaScript 全部內嵌，沒有 build step、沒有 npm、沒有任何外部函式庫（唯一的外部 script 是 GoatCounter 統計）。這是刻意的：這個站的更新是人工比對 PTT 貼文後直接改檔案（見 `.github/prompts/update.prompt.md`），維護者要能打開一個檔案就看懂全部、改完直接 commit 就上線。引入打包工具會讓「改一行贈品說明」變成要先跑安裝與建置。

因此在做 UI 功能時，優先手刻而非引入套件——例如 lightbox 的縮放與左右切換是用 `transform` 與 pointer events 自己寫的，而不是裝 PhotoSwipe；深色模式用 CSS 變數與 `prefers-color-scheme`，而不是裝主題框架。

代價：手刻的元件在邊角案例（手勢慣性、觸控裝置差異）上不會有成熟套件那麼完善，而且 `index.html` 會持續變長。當這個檔案長到一個人讀不動時，正確的下一步是**把活動資料抽成 `activities.json` 由前端渲染**（縮小手寫的部分），而不是引入建置流程。
