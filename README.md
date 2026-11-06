# 時之笛 譜架

《薩爾達傳說 時之笛》Switch 2 版的陶笛自動演奏網頁。點一下歌曲 icon，手機就把旋律吹出來，靠近 Switch 2 的麥克風，遊戲就會讓林克照著演奏。不用自己哼，也不用按按鈕。

## 怎麼用

1. 在遊戲的「選項」打開 **Ocarina Mic Input**
2. 在遊戲裡拿出陶笛
3. 手機靠近 Switch 2，點網頁上的歌曲 icon

遊戲辨識不到的話，到網頁的「演奏設定」換音高（低／中／高）或改用純音。iPhone 沒聲音時，先關掉側邊的靜音開關。

任天堂官網寫的兩個注意事項：

- 遊戲只認得已經在遊戲裡學會的歌，還沒學的歌播了也不會有反應
- Switch 2 接著外接麥克風，或 Pro 控制器接著有麥克風的耳機時，可能辨識不到

## 功能

- 14 首歌依功能分類：開啟機關、傳送、召喚與溝通、時間與天氣、自訂（稻草人之歌）、小遊戲（索拉河青蛙）
- 分類和歌曲的預設順序依遊戲裡的常用程度排，常用的在前面
- 點 icon 直接播放，同一時間只播一首；點三角力量展開樂譜，樂譜用 Switch 2 按鍵顯示
- 播放時徽章外圈的進度環跟著填滿，每個音一圈漣漪，每首歌的圖案有自己的動畫
- 點卡片右上角的劍可以釘選，釘選的歌會多一份放在最上面，原本分類裡的位置不變；可以同時釘選多首，也能拖曳排序（手機長按約 0.3 秒）
- 稻草人之歌讓玩家自己輸入 8 個音，會檢查遊戲規則：不能 8 個音全部一樣，也不能包含其他歌的旋律
- 釘選、順序、演奏設定和稻草人旋律存在瀏覽器的 localStorage

## 技術

- 單一 HTML 檔：`public/index.html`，不用 build
- 聲音用 Web Audio 即時合成，不載入任何音檔
- 拖曳排序用 [SortableJS](https://github.com/SortableJS/Sortable) 1.15.2（cdnjs）

## 部署

網站部署在 Cloudflare Workers 的靜態網站（`wrangler.jsonc` 指定上傳 `public/`）：https://ocarina-player.a84012807.workers.dev

```sh
npx wrangler deploy
```

## 分享預覽圖

`public/og.png`（1200×630）由 `og/card.html` 產生，修改後用 Chrome 重新截圖：

```sh
"/Applications/Google Chrome.app/Contents/MacOS/Google Chrome" --headless=new --hide-scrollbars \
  --force-device-scale-factor=1 --window-size=1200,630 --virtual-time-budget=10000 \
  --screenshot="$PWD/public/og.png" "file://$PWD/og/card.html"
```

## 按鍵資料來源

五個音由低到高對應 Switch 2 預設配置的 L、R、A、Y、X，這組對應用任天堂官方截圖裡薩爾達的搖籃曲和時之歌核對過（兩首合起來用到全部五個音）。

12 首歌的旋律都對照過[任天堂日本官網的樂譜](https://www.nintendo.com/jp/games/switch2/aa9ja/melody/index.html)，官網標的是唱名和實體陶笛指法，換算成按鍵後 12 首都和網站資料一致。青蛙之歌和稻草人之歌官網沒有列。

---

非官方玩家工具，與任天堂無關。圖示、動畫和聲音都是原創，沒有使用遊戲的美術或音檔。
