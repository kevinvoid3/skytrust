# 光遇工具站 Sky Tools

[English](./README_en.md) | 繁體中文

給 **Sky: Children of the Light（光·遇）** 玩家用的小工具合集：季節先祖解鎖計算、好友樹規劃、身高計算。全部是靜態網頁，進度只存在你自己的瀏覽器裡。

[網站連結](https://kevinvoid3.github.io/skytrust)｜[GitHub 專案](https://github.com/kevinvoid3/skytrust)

## ✨ 功能特性

### 🕯️ 季節先祖計算器（`spirit.html`）

- **完整兌換樹**：涵蓋季節先祖、嚮導、常駐先祖與長老，依季節與地圖分組，版面依照遊戲內的實際排列
- **進度追蹤**：點選項目即標記解鎖，自動計算需要的季蠟、已花費的季蠟，以及目前好感度與等級
- **好感度門檻**：每一層標出升級需要的好感度，左側用分段進度條顯示目前所在的層級
- **還需天數估算**：依照每日蠟燭獲取量與初始蠟燭推算
- **季卡標示**：季卡限定的項目在圖示左上角掛季節項鍊徽章
- **隱藏畢業禮與季節項鍊**：開關各季分開記住，隱藏的項目不計入統計
- **跨分組搜尋**：輸入項目、先祖或季節名稱，直接跳到該格並閃爍標示
- **分享連結**：把當前分組的進度壓成一條網址，對方開啟時是唯讀檢視，可以選擇套用
- **單檔離線版**（💾 離線版）：資料內嵌進一個 HTML 檔，雙擊就能開，不需要網路
- **多方案**：可以為不同角色分開記錄進度，並支援匯出／匯入備份
- **緊湊模式**：手機預設開啟，單格高度減少約三成

### 🤝 好友樹規劃器（`friend.html`）

- 可記錄多位好友，各自的解鎖紀錄分開保存
- 設定目標等級，試算需要的蠟燭與好感度門檻，並和你的蠟燭庫存比對
- 全解鎖預覽、重置、匯出／匯入

### 👤 身高計算器（`height.html`）

- 上傳、拖曳或貼上造型 QR Code 截圖，也可以直接貼 Base64 字串或分享連結
- 算出目前身高，以及這個帳號可能的最高與最矮身高
- QR Code 在瀏覽器裡解碼，圖片不會上傳到任何地方

### 共通

- **三語介面**：繁體中文／简体中文／English，各頁共用同一個語言設定
- **深色／淺色主題**：各頁共用同一個主題設定
- **純靜態**：沒有後端，部署在 GitHub Pages 這類靜態託管服務上就能運作

## 📁 專案結構

```
.
├── index.html          # 首頁：各工具的入口
├── spirit.html         # 季節先祖計算器
├── friend.html         # 好友樹規劃器
├── height.html         # 身高計算器
├── about.html          # 關於此站
├── index.old.html      # 舊版（v1）計算器，保留備查
├── data/
│   ├── spirits.data.json    # 兌換樹資料（由建置腳本產生）
│   ├── spirits.i18n.json    # 三語顯示字串
│   ├── spirits.images.json  # 圖示網址對照表
│   └── friend_tree.json     # 好友樹資料（好友樹規劃器用）
├── LICENSE
├── README.md
└── README_EN.md
```

## 📄 資料檔說明

`spirits.*.json` 三份檔案是由另一個私有 repo 的建置腳本，從遊戲資料整理出來的，**不要在這裡手動修改**，下次更新會被整份覆蓋。翻譯或圖片有錯，請開 Issue 回報。

**spirits.data.json**：依分組存放每隻先祖的兌換樹

```json
{
  "_meta": { "build": "2026-11-17a", "generated": "2026-11-19T11:09:06+08:00" },
  "season_32": {
    "spirits": {
      "questap32": {
        "kind": "guide",
        "tier": 4,
        "tiers": { "2": 400, "3": 800, "4": 1200 },
        "items": [
          { "k": "quest", "cst": 0, "ctyp": "season_candle", "exp": 200,
            "level": 1, "pass": false, "src": "quest_ap32_fetch_01" }
        ]
      }
    }
  }
}
```

| 欄位 | 說明 |
|------|------|
| 頂層的鍵 | 分組：`season_N`（季節）、`elders`（長老）、`realm_*`（各地圖的常駐先祖） |
| `kind` | `guide`＝嚮導（二維格線版面），`tree`＝一般兌換樹 |
| `tier` / `tiers` | 可達到的最高等級／各等級需要的累計好感度 |
| `k` | 項目類別，顯示名稱到 `spirits.i18n.json` 查 |
| `cst` / `ctyp` | 價格與貨幣種類（季蠟、愛心、季節之心……） |
| `exp` | 解鎖後給的好感度 |
| `level` | 所在等級 |
| `pass` | 是否為季卡限定 |
| `src` | 遊戲內的項目代碼，同時是圖片與進度紀錄的識別鍵 |

**spirits.i18n.json**：`{ "zh-hant": {…}, "zh": {…}, "en": {…} }`，鍵是分組、先祖代碼與項目類別。

**spirits.images.json**：`{ 項目代碼: 圖片網址 }`。圖片來自 [skyinfoweb](https://skyinfoweb.pages.dev)。

**friend_tree.json**：好友樹規劃器（`friend.html`）的資料來源，定義好友樹上每一個友誼動作的每一級：在第幾層、要花多少蠟燭、圖示是什麼。三種語言各存一份，結構相同，只有 `nm`（顯示名稱）不同。

```json
{
  "zh-hant": {
    "FriendTree": {
      "items": [
        { "actionId": "duetbow", "nm": "雙人鞠躬", "level": 2, "tier": 3,
          "order": 8, "cst": 5, "exp": "10", "image": "https://skyinfoweb.pages.dev/image/…" }
      ]
    }
  },
  "zh": { "FriendTree": { "items": [ … ] } },
  "en": { "FriendTree": { "items": [ … ] } }
}
```

| 欄位 | 說明 |
|------|------|
| `actionId` | 友誼動作代碼。同一個動作的各級共用同一個代碼 |
| `nm` | 顯示名稱（依語言不同） |
| `level` | 這個動作的第幾級（1～4）。必須先解鎖前一級 |
| `tier` | 位在好友樹的第幾層（1～7），決定要多少好感度才能解鎖。各層門檻寫在 `friend.html` 的 `TIER_REQ_EXP` |
| `order` | 同一層內由左到右的順序 |
| `cst` | 解鎖需要的蠟燭數 |
| `exp` | 好感度數值，頁面目前沒有用到 |
| `image` | 圖示網址，一律使用 [skyinfoweb](https://skyinfoweb.pages.dev) 的圖片 |

> 進度是用 `actionId` ＋ `level` 識別的。改動這兩個欄位會讓玩家已經勾選的紀錄對不上，新增或調整項目時請保持不變。

## 🚀 部署方式

1. 把整個資料夾部署到靜態網頁託管服務（GitHub Pages、Cloudflare Pages 等）
2. 頁面用 `fetch` 讀取 `data/` 底下的檔案，所以**不能直接雙擊 HTML 檔開啟**。本機預覽請在資料夾裡執行：
   ```bash
   python -m http.server 8000
   ```
   然後打開 `http://localhost:8000/`
3. 只想在本機離線使用的話，在計算器裡按「💾 離線版」產生單一 HTML 檔即可

## 🔒 隱私

- 所有進度、方案與設定都只存在瀏覽器的 `localStorage`，不會上傳
- 分享連結的進度寫在網址 `#` 後面，這一段不會被送到伺服器
- 清除瀏覽器資料會連進度一起清掉，換裝置或重灌前請先「匯出」備份

## ⚠️ 免責聲明

- 本站與 thatgamecompany（TGC）及網易官方無任何關聯，是玩家自製的第三方工具
- 遊戲名稱、圖片與相關素材的權利屬於原權利人
- 資料可能因遊戲改版而與實際情況有出入，請以遊戲內為準

## 🐛 問題回報

有問題、建議或錯誤回報，歡迎到 [GitHub Issues](https://github.com/kevinvoid3/skytrust/issues) 提出，或寄信到 [adam810027@gmail.com](mailto:adam810027@gmail.com)。

## 📜 License

程式碼以 [MIT License](./LICENSE) 釋出。遊戲素材不在此授權範圍內。