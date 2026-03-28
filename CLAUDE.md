# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 專案概述

2026 沖繩家族旅遊規劃專案（9人，含2位輪椅使用者，5天4夜，3/31-4/4）

## 主要文件

### 規劃文件
| 文件 | 用途 |
|------|------|
| `沖繩旅遊規劃.md` | 主文件：行程、航班、住宿 |
| `餐廳清單.md` | 5天所有餐廳選項（早午晚） |
| `待辦事項.md` | 出發前待辦清單（🔴🟡🔵優先級） |
| `CoCoR_預約訊息.md` | 福祉計程車預約訊息（英/日） |
| `駕照日文譯本申請SOP.md` | 日文譯本申請流程 |
| `Laguna_Fuchaku_住客資料.md` | Airbnb 住客資料（⚠️ .gitignore） |

### 網站文件（GitHub Pages）
| 文件 | 用途 |
|------|------|
| `index.html` | 首頁：行程總覽、checklist、緊急聯絡 |
| `day1.html` ~ `day5.html` | 每日詳細行程頁面 |
| `sw.js` | Service Worker（network-first, v3） |
| `manifest.json` | PWA manifest |

### 封存
| 文件 | 用途 |
|------|------|
| `archive/那霸住宿比較.md` | 住宿比較（已決定，封存） |
| `archive/Booking查詢結果-2026-02-07.md` | Booking 查詢記錄 |

## 工作流程

### 查詢即時價格/庫存
使用 **Task agent + Playwright MCP**（減少主對話 token 消耗）：
```
Task agent prompt 範例：
「請用 mcp__playwright__browser_navigate 打開 [Booking URL]，
用 mcp__playwright__browser_snapshot 截取快照，
找出價格和剩餘房數，最後用 mcp__playwright__browser_close 關閉」
```

### 查詢一般資訊（評價、交通等）
使用 **Task agent + WebSearch**

## 重要考量

- **無障礙需求**：部分成員需要無障礙設施，每間飯店都要確認無障礙房資訊
- **停車需求**：9人分租車，需確認停車場資訊
- **價格來源**：標註查詢日期和來源（Booking.com / Google Maps）

## 開發規則

### CLAUDE.md 維護
- 新增/刪除/重新命名檔案 → 更新「主要文件」表格
- 人數、日期、住宿等核心事實變更 → 更新「專案概述」
- 每次對話結束前，確認 CLAUDE.md 是否需要同步

### 全站 UI 變更
- 影響所有頁面的功能（深色模式、導覽列、字型）→ 先確認再動手
- 改一頁的 CSS/JS → 檢查其他頁面是否有同樣元素需要一致更新
- 部署前在手機視窗（375px）目視確認關鍵按鈕可見性

### 網站部署
- 改版後 bump `sw.js` 的 `CACHE_NAME` 版本號
- push 後確認 GitHub Pages 部署成功

## MCP 工具

已啟用：
- `playwright`：網頁自動化查詢（價格、庫存）
- `google-maps`：地點、距離、評分查詢
