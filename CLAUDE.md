# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## 專案概述

2026 沖繩家族旅遊規劃專案（11人，5天4夜）

## 主要文件

| 文件 | 用途 |
|------|------|
| `沖繩旅遊規劃.md` | 主文件：行程、航班、住宿、LINE 群組文案 |
| `那霸住宿比較.md` | 住宿詳細比較：價格、設施、無障礙、交通 |

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
- **停車需求**：11人可能租車，需確認停車場資訊
- **價格來源**：標註查詢日期和來源（Booking.com / Google Maps）

## MCP 工具

已啟用：
- `playwright`：網頁自動化查詢（價格、庫存）
- `google-maps`：地點、距離、評分查詢
