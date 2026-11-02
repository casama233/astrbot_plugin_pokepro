# astrbot_plugin_pokepro — 專業戳一戳

[简体中文](README.md) · **繁體中文** · [English](README.en.md)

這是 AstrBot 的戳一戳互動插件。有人戳 Bot 時，可按權重隨機執行反戳、LLM 回覆、QQ 表情、圖片表情、禁言或觸發指令；也提供主動戳、關鍵字及定時戳，且可自訂機率與內容。

**需要 AstrBot v4.13.0+**，否則可能無法載入插件。於 AstrBot 插件市場搜尋 `astrbot_plugin_pokepro` 安裝。

## 基本設定

| 設定 | 用途 | 預設 |
| --- | --- | --- |
| `on_poke` | 戳一戳監聽總開關 | `true` |
| `poke_cd` | 使用者戳 Bot 的冷卻秒數 | `10` |
| `group_poke_cd` | 群聊戳 Bot 的冷卻秒數，`0` 關閉 | `0` |
| `follow_prob` | 他人被戳時跟著戳的機率 | `0.1` |

每個回覆動作都有 `weight`；實際選中機率 = **該動作權重／全部動作權重總和**。

| 動作 | 主要欄位 | 預設 |
| --- | --- | --- |
| `antipoke`（反戳） | `weight`、`max_times`（隨機 1–N 次） | `10`、`5` |
| `llm`（模型回覆） | `weight`、`template`（可用 `{username}`） | `10`、`"{username} 戳了你一下..."` |
| `face`（QQ 表情） | `weight`、`pool` 表情 ID 列表、`max_copy_count` | `10`、`[1,11,14...]`、`3` |
| `meme`（表情包） | `weight`、`pool` 本地圖片池 | `10`、`[]` |
| `ban`（禁言） | `weight`、`duration`、`delta`、`ban_template`、`ban_fail_template` | `10`、`60` 秒、`30` 秒、無預設提示 |
| `command`（指令） | `weight`、`pool` 指令池 | `10`、依配置 |

## 主動戳與排程

| 設定 | 用途 | 預設 |
| --- | --- | --- |
| `poke_max_times` | `戳 @某人 次數` 的一般使用者上限（管理員不受限） | `5` |
| `poke_interval` | 發戳間隔秒數 | `0.5` |
| `poke_keywords` | 訊息出現時觸發主動戳的關鍵字 | `[笨蛋, 人机, 机器人, bot]` |
| `scheduler.enabled` | 啟用定時戳 | `true` |
| `scheduler.cron` | 分、時、日、月、週 | `"30 22 * * *"` |
| `scheduler.target` | `群號:QQ號` 列表 | `["-199:-101"]` |
| `scheduler.times` | 每次戳的次數 | `1` |

## 指令（保留實際中文寫法）

| 指令 | 功能 |
| --- | --- |
| 被戳 | 依權重執行反戳、模型、表情、圖片、禁言或指令 |
| `戳 @XXX` | 戳指定人，可指定次數，例如 `戳 3@张三` |
| `戳我` | 戳自己 |
| `戳全体成员` | 戳全員；超過 200 人的群組隨機選取 200 人 |

翻譯 README **不會更改插件實際支援的中文指令或配置鍵**。

## 貢獻與授權限制

歡迎 Star、Issue、功能提案及 PR。原 README 列出的插件反饋 QQ 群為 `-199`。

**重要上游授權警告：** 此倉庫是 [Zhalslar/astrbot_plugin_pokepro](https://github.com/Zhalslar/astrbot_plugin_pokepro) 的 fork。已查核上游**沒有 LICENSE 文件**（`UNLICENSED_UPSTREAM`）。本 fork 內的 GPL-3.0 文件**不能替原作者授權**，亦不能自行把上游程式碼改授 GPL。取得作者許可，或確認相關內容為獨立創作以前，不得另外發布、打包或合併上游衍生部分。保留原作者署名與素材來源，不能把本倉庫的授權視為覆蓋第三方資產的許可。
