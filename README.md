# Twitch 小羊打王 GitHub Pages 版

這個資料夾是純靜態網頁版本，適合直接放到 GitHub Pages。

## 頁面

- `settings.html`：設定頁，填活動標題、ROUND、掉寶、自動扣血、WebSocket URL、測試資料。
- `battle.html`：演出頁，會讀取設定並直接連外部 WebSocket。
- `index.html`：入口頁。
- `config.json`：預設設定檔。
- `sheeps/`：演出圖片素材。

## 資料來源

演出頁會連：

```text
wss://tsukilin.greentool.cc/ws/off
```

支援目前後端已使用的外部格式：

- `OFF_DAMAGE` 或包含 `amount + name/user/displayName` 的資料，會轉成一次攻擊。
- `OFF_METADATA` 或包含 `currentSub / targetSub / rank / reachTarget` 的資料，會更新目前訂閱數、目標訂閱數、排行榜與勝利判定。
- 排行榜會從 `rank` 裡的 `name` 和 `count` 讀取；如果沒有 `count`，才會 fallback 到 `amount / damage / total / score / sub / subs`。

## 重要限制

GitHub Pages 是靜態空間，`settings.html` 不能直接把設定寫回 GitHub 上的 `config.json`。

目前設定頁會把設定存在同一個瀏覽器的 `localStorage`。如果需要「一台電腦改設定，另一台電腦的演出頁也同步」，需要再接一個可寫入的雲端資料來源，例如 Firebase、Supabase、Google Apps Script，或自架 API。
