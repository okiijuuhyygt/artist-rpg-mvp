# Artist RPG MVP · 專案狀態

> 最後更新:2026-04-25 凌晨 **05:10**
> Build: **index v1.3 / code v1.27** · content 已被耗耗 admin 編輯

## 網址
- 公開站 · https://okiijuuhyygt.github.io/artist-rpg-mvp/
- 關主後台 · https://okiijuuhyygt.github.io/artist-rpg-mvp/admin.html
- GitHub · https://github.com/okiijuuhyygt/artist-rpg-mvp

## 功能狀態

| 功能 | 狀態 | 備註 |
|---|---|---|
| 三 scene(intro / map / level) | ✅ | hash routing + 滑動轉場 |
| 五關任務制(L0-L4 真動作) | ✅ | v1.0 起。L0 按鈕 / L1 聽 15s / L2 投票 / L3 寫歌詞 / L4 召喚陣 |
| 試聽 8-bit tone generator | ✅ | iOS 靜音也聽得到(WAV via `<audio>`) |
| BGM 雙軌(intro + map) | ✅ | C major + A minor 兩段 8-bit loop |
| 訪客計數 90s 風 | ✅ | abacus.jasoncameron.dev |
| 像素大頭(GIF) | ✅ | 120x120,crop 620x620 at (110,420) |
| Kit email 名單(真收) | ✅ | form 9365865「陳則皞の村莊」 |
| Admin token-only 偽裝密碼登入 | ✅ | 密碼 = 耗耗的 GitHub PAT |
| Admin CMS(content.json) | ✅ | 耗耗已自己改過內容 |
| Admin 音檔上傳(5 關 + 2 BGM) | ✅ | mp3/wav/m4a,20MB cap |
| 關主金色徽章(登入識別) | ✅ | 暖棕皮革風 |
| Clear 後「繼續 →」CTA | ✅ | v1.21,不再 auto-return |
| 完成後自動回 map | ❌ 改 CTA | v1.21 revert 為玩家點擊 |
| Cache-buster(iOS 頑固) | ✅ | meta version + localStorage mismatch force reload |
| site name 可編輯 | ✅ | admin 世界設定 → SITE NAME,當前設為 `haohao.unzip` |

## 還沒做(pending)

- **付費解鎖** — 討論到一半,等耗耗醒來回 3 個 Y/N(見下)
- **照片上傳(Cloudinary)** — L1/L3 填空資產需要,他還沒註冊 cloudinary
- **L2 投票 / L3 寫歌詞 data 送出** — 目前只存玩家 localStorage,耗耗看不到
- **OG image / Favicon** — 分享預覽目前空白
- **Kit confirmation email** 改他語氣 — 還是 Kit 預設英文

## 付費解鎖 · 等耗耗 Y/N

| Q | 我的建議 |
|---|---|
| **Q1. 付費玩家角色名** | 「**製作委員會**」(中性,避性別,有日本動畫味) |
| **Q2. MVP 定價 & 內容** | **199 / 299 TWD digital-only**:demo mp3 + 歌詞 PDF + podcast 連結 + MV credit |
| **Q3. 付費流程** | 點 CTA → 跳綠界 → 付完綠界寄通知耗耗 → 耗耗手動 email delivery。遊戲內不分 tier、不做解鎖機制 |

## 付費解鎖 · 最終 spec(2026-04-25)

**✅ 確認的決策:**
- 角色名:**製作委員會**
- 價格:**150 TWD**(single tier)
- 付費流程:綠界 hosted payment → 通知耗耗 → 耗耗手動 email 寄 demo/PDF/podcast
- CTA 位置:每關 action-block 底下常駐「✦ 加入製作委員會」按鈕

**Phase 1(v1.22 已做完):**
- 付費 modal 有每關不同 teaser(peak-end rule)+ 統一 bundle 介紹 + 前往結帳
- 綠界 URL 空時顯示「結帳系統建置中」+ 引導填 email

**Phase 2(下一輪要做的 tier 差異):**
付費玩家在遊戲內**看到更多**,不只是線下收 email:
- L1 填空資產:真的可以**上傳照片**到 MV 0:47 空白牆(需 Cloudinary)
- L2 分岔路:看到**完整投票結果 + 誰投了什麼**(需 Kit API 或 server)
- L3 歌詞:看到**其他付費玩家寫的歌詞精選**
- L4 召喚陣:看到**進度 + 誰已經 join 了**

Phase 2 需要:
1. Tier identification — 綠界付款後 Kit 打 `paid-ep1` tag → 前端查(需要 Worker 繞 CORS + 藏 API key)
2. Cloudinary 帳號 + upload preset
3. Kit API proxy(Cloudflare Worker 免費)

**理由:** peak-end rule — 玩家看到**這一關**特有的 value 才掏錢,不是 generic 「解鎖全部」。

| 關 | 該關的解鎖預告角度(全指向同一個 EP bundle) |
|---|---|
| L1 | 🎧 完整 demo · 把你手寫的字放進 MV 0:47 |
| L2 | 🗺 看到這條路最終我錄了哪首 · 投票名單 |
| L3 | 💌 你寫的歌詞印成**實體明信片**寄給你 |
| L4 | 🔥 召喚名單 · 翻唱歌手 credit |

實作順序:
1. 每關 action-block 下方加「✦ 解鎖支線」secondary button(跟「繼續 →」並排)
2. 點了開 modal / 切 sub-scene,顯示**這關 angle 的預告** + 商品條列
3. Modal 底部「▶ 前往結帳」→ 跳綠界 hosted payment
4. 綠界付完寄 notification 到耗耗 Kit / email → 耗耗手動 email delivery

## 重要技術 gotchas

- **Token 只在耗耗瀏覽器 localStorage**。他存 Apple 備忘錄(iCloud 多裝置同步)
- **Kit 需要 ck.js + data-sv-form attrs 才 count subscriber**(沒帶 tracker 會被當 bot drop,但 302 still 回 success 造成錯判)
- **iOS Chrome 和 Safari 都吃同一個 WebKit cache**,靠 build-version meta 變動 + localStorage mismatch 強制 reload
- **綠界 callback 要 server**(GitHub Pages 沒 server)— 所以 MVP 走「email 寄通知耗耗 → 耗耗手動 delivery」避開整個問題
- **GitHub API PUT 大檔會 error**(> 50MB),所以音檔限 20MB

## 主要檔案

- `index.html` — 公開站,single-page hash router
- `admin.html` — 關主後台
- `content.json` — 所有文字 + 關卡設定 + 上傳音檔 path(耗耗用 admin 改)
- `avatar.gif` — 像素大頭
- `fonts/` — (已刪)Cubic 11 試過被 revert

## 3/23 RPG 原設計 ↔ MVP 實作對照

| 3/23 設計 | MVP 實作 |
|---|---|
| 填空式資產(MV 空白牆、章節封面) | L1/L3 的 `???` 框 + `hasMissingPiece` flag(UI 提示,未真上傳) |
| 分支決策權(付費玩家投票) | L2 兩條路 + `state.picks`(要 email 才能投,但未真回傳給耗耗) |
| NPC 階級(遊客/村民/商人/金主媽媽) | 簡化為 訪客/村民;商人/金主媽媽 保留在付費階段討論 |
| 傭兵召喚陣(30 村民解鎖) | L4 隱藏關,`unlockedBy: __village__`(填 email 即解);真 30 人門檻未做 |

## 下一輪優先順序(我建議)

1. 耗耗 confirm 付費 3 Q → 寫成 spec
2. 實作付費 CTA button + 綠界跳轉 link
3. L2/L3 的 data 用 Kit tag / Formspree 送出(讓耗耗看得到)
4. Cloudinary 照片上傳(耗耗註冊後接)
5. OG image + Favicon(polish)
