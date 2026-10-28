# 永續善農獎 IPM Award 報名小幫手

給有意報名「永續善農獎 IPM Award」的農友使用的網頁工具。回答幾個問題找到適合的組別，再一題一題填完，產生可以列印、投件用的報名表。

網址：https://clhuangtarm-lab.github.io/ipm-award/

> 本工具依第五屆永續善農獎評選辦法（公告版）整理。正式投件請以主辦單位公告的官方附件表格為準。最新公告與報名方式請看活動網站：https://ipm-award.mystrikingly.com/

## 這個網站是什麼

- 整個網站只有一個檔案：`index.html`。畫面、樣式、程式都在裡面。
- 沒有後端，沒有資料庫。使用者填的內容只存在自己瀏覽器的 localStorage，不會上傳。
- 用 GitHub Pages 發布。推上 `main` 分支，網站就會自動更新。

## 更新網站的流程

1. **先取最新版**。任何機器都一樣：`git clone` 或 `git pull`，或在倉庫頁面按鍵盤 `.` 用線上編輯器改，不用裝任何東西。
2. **改 `index.html`**，只改要改的地方。
3. **推上 `main`**。
4. **用瀏覽器打開上面的網址確認**。Pages 通常 1 分鐘內更新。

## 改之前一定要檢查

1. **先看 `git log`**，有沒有不是自己做的新提交。有的話，以倉庫現在的 `index.html` 為基底。
2. **不要拿本機的舊檔整份覆蓋 `index.html`**。曾經發生過一次，把別人已經推上去的更新整個蓋掉，後來靠 `git revert` 救回。
3. **推之前執行 `git diff --stat`**，變動量要和預期相符。改一個日期只會有幾行，如果出現上百行，代表基底拿錯了。
4. **推完比對線上內容**，不要只看部署成功的燈號。

## 匿名使用量統計

用 [GoatCounter](https://www.goatcounter.com/) 統計匿名的使用情形：瀏覽與按鈕次數，以及彙整後的大致國家、瀏覽器、作業系統與螢幕大小，用來了解推廣成效與農友卡在哪一步。依官方說明，它不會把 IP 和瀏覽器資訊存進資料庫，只存統計後的數值。官方文件沒有明確說明 cookie 的使用，所以本網站不對外宣稱「不使用 cookie」。

- **不收集個人資料。** 只送「事件名稱」，不送使用者填的任何內容。
- **開關在 `index.html` 的 `ANALYTICS_CODE`。** 留空代表完全不啟用，不載入任何外部程式；填入 GoatCounter 的網站代碼才會啟用，同時頁尾會顯示「只統計匿名次數」的說明。
- **統計失敗不影響填寫。** 服務被廣告攔截或當機時，網站照常能用。

統計的事件（在 `index.html` 搜尋 `track(`）：

| 事件 | 意思 |
|---|---|
| `quiz_start` | 開始分組測驗 |
| `quiz_result_field` / `_tech` / `_promo` | 看到測驗結果（建議的組別） |
| `form_open_field` / `_tech` / `_promo` | 開始填報名表（選的組別） |
| `form_generated_field` / `_tech` / `_promo` | 按下「產生報名表」 |
| `print` / `copy` | 列印、複製報名表 |
| `backup_export` / `backup_import` | 匯出、匯入備份 |

要追蹤不同管道的來源（例如 LINE、臉書、說明會海報），在網址後面加 `?ref=管道名稱`，例如 `https://clhuangtarm-lab.github.io/ipm-award/?ref=line`，GoatCounter 會把它列在「來源」裡。

訪客數不等於報名人數：家人或農會人員可能代填多位農友，同一個人也可能用手機和電腦各開一次。統計只能當流程指標。

## 常見的改動位置

在 `index.html` 裡搜尋這些名稱：

| 要改什麼 | 搜尋 |
|---|---|
| 報名截止日（倒數計時） | `deadlineText` |
| 投件方式頁的截止日 | `收件截止日` |
| 各組報名表欄位 | `var FORMS` |
| 佐證資料與預估頁數 | `var DOC_ITEMS` |

截止日在倒數計時和投件方式頁各有幾處，要一起改。改完用搜尋確認舊日期已經沒有殘留。

## 注意事項

- **這個倉庫是公開的。** 不要放個資、報名者資料或內部文件。
- **不要把 git 工作資料夾放在 OneDrive 之類的同步資料夾裡**，`.git` 容易被同步搞壞。
- **Windows 上本機檔案會比線上大。** git 的 `autocrlf` 會把換行轉成 CRLF，所以本機的 `index.html` 大小和線上不同是正常的。要比對請用 `git show HEAD:index.html`，那才是倉庫裡真正的內容。
- **偶爾 Pages 部署會失敗**（Actions 裡 deploy 紅燈）。重新觸發一次建置就好：

  ```bash
  gh api --method POST repos/clhuangtarm-lab/ipm-award/pages/builds
  ```
