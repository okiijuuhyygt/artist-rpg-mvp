# 付費流程 mock 測試 — 訊息 templates

> 目的:在切 paid mode 之前,先讓**一個信任的朋友**真的跑一次「玩 → 付 → 收到東西」全流程,確認 ops 順,再對外開。
> 預估時間:朋友 5 分鐘玩 + 你 10 分鐘 delivery。
> 操作:把下面 template 複製貼到 LINE / IG DM / Threads / 任何你跟那位朋友常用的管道。

---

## 1. 約朋友來測 — 開場 DM(複製這段)

```
欸我在做一個東西,需要你幫我跑一次測試 5 分鐘 🙏

我做了一個小遊戲讓聽眾參與我寫歌的過程,有付費版(150)。
我要在公開之前確認「玩家付了能順利收到東西」,所以想請你假裝是真客戶跑一次。

你只要做兩件事:
1. 點這個連結玩到任何一關,看到「✦ 加入製作委員會」按鈕點下去 → 跳綠界 → 付 150
2. 付完跟我說「付好了」就好

我會在 24 小時內把該寄的東西寄到你 email,你幫我看寄出來的東西順不順、有沒有奇怪的地方就好。

測完我把 150 還你 + 請你喝飲料當謝禮。要嗎?

🔗 https://okiijuuhyygt.github.io/artist-rpg-mvp/
```

---

## 2. 切 paid mode 的步驟(朋友 OK 之後再做)

1. 進 admin: https://okiijuuhyygt.github.io/artist-rpg-mvp/admin.html
2. 用 GitHub PAT 登入(Apple 備忘錄那個)
3. 「付費設定(製作委員會)」section → MODE 改成 `💳 paid`
4. 確認 CHECKOUT URL 是 `https://p.ecpay.com.tw/6963529`(綠界 hosted link)
5. 「儲存到網站」

---

## 3. 朋友付完 → 你的 delivery email(複製到 Gmail / Apple Mail)

**收件人:** 朋友的 email
**主旨:** 製作委員會 EP1 · 收到了你的支持 🎵
**正文:**

```
嗨 [朋友名字],

收到你 150 的支持了 — 謝謝你陪我跑這個測試 🙏

這封信是 EP1「製作委員會」目前可以給你的東西。實體交付的部分(明信片、MV credit)我會在 EP1 上線時一起寄。

—

🎧 demo mp3
[這裡放 1-3 個 demo 的 mp3 連結 — Google Drive / Dropbox / 任何雲端連結都可以,設成「有連結的人可看」]

💌 歌詞手稿 PDF
[一個 PDF 連結 — 用 Notion export 或 Pages 印 PDF 都可以]

🎙 幕後 podcast 連結
https://open.firstory.me/user/haohao-zip/platforms

🎬 你的名字會進 MV credit
我會把你寫的名字加進 EP1 MV 結尾的「製作委員會」名單。
請告訴我希望顯示什麼名字(本名/暱稱/匿名都可以)?

—

實際上線之後會做的事:
- MV 上 YouTube 那天會通知你
- EP2 開始寫的時候你會先收到 demo
- 11 月低成本演出排上的話,你會有 priority 報名

如果你發現這封信有任何 typo / 連結壞 / 流程不順,直接回信告訴我 — 你是第一個跑這個的人,任何回饋都超有用。

—
HAO · 陳則皞
haohao.unzip
```

---

## 4. 測完之後做的事

- [ ] 確認朋友收到 email + 連結都能開
- [ ] 把 150 還朋友(轉帳 / 請吃飯都可)
- [ ] 在 admin 把 MODE 切回 `🆓 free`(or 留 paid 如果朋友 feedback OK)
- [ ] 把朋友的 email 留在你的 Kit 「付費玩家」標籤(手動加 tag)
- [ ] 在 SESSION-HANDOFF 記下:「paid flow mock 跑過,順 / 卡在 X / 改了 Y」

---

## 5. 朋友會踩到的常見坑(預防性 list)

| 朋友可能說的 | 你該檢查 |
|---|---|
| 「綠界網頁卡白白的」 | 跨瀏覽器 cache 問題 → 請朋友開無痕 |
| 「付完看不到任何 confirmation」 | 對的,綠界沒 callback,他付完只會看到綠界的「付款成功」頁 → 這是已知設計,你會手動確認 |
| 「mp3 連結點不開」 | Google Drive 權限沒設「有連結的人可看」 |
| 「你怎麼知道我付了?」 | ECPay 商家後台會通知你(後台 → 收款記錄 → email 通知) |
| 「我的名字怎麼進 credit?」 | 這封信問清楚名字 → 你存 Notion 或 Apple 備忘錄「EP1 製作委員會名單」 |

---

## 6. 朋友建議名單(挑一個容易講話的)

[ 這格自己填:寫 3-5 個你覺得會願意花 5 分鐘幫忙的名字 ]
1.
2.
3.

選擇標準:
- 願意誠實給回饋(不是無腦稱讚)
- 用 iPhone(因為 iOS Safari 是大宗,要驗證跨瀏覽器)
- 不是 musician(他會以「客戶」視角玩,不是同行)
