# Chinese Land Deeds · 契紙流年

*AI-assisted reading and household reconstruction of the University of Pittsburgh "Chinese Land Records" collection (EAL.2011.01; 234 documents, 1584–1978, mostly Fujian). How did title documents change across regimes, and how did property pass down the generations?*

匹茲堡大學「中國土地文書」館藏的識讀與歸戶：產權憑證如何隨政權更替而變化？一個家戶的產業如何一代代轉移？

數據源：<https://digital.library.pitt.edu/collection/chinese-land-records>

## 主要發現

1. **國家越管越深**：有官印的文書，清代佔 63%，民國 81%，1949 年後 96%。契稅從清代契尾的 3% 升到 1947 年官印賣契的 6%。
2. **官府文書看不到傳承**：永泰黃氏 57 頁完糧收據上，同一筆稅在兄弟名下換來換去；1947 年的管業執照只登記當下業主，沒有「來歷」欄。
3. **傳承寫在民間契約裡**：建陽劉氏的契約寫明「本族」「堂孫」；閩侯林萬開 1891 年的分家鬮書寫明「承父遺物業」「長子長孫份」。
4. **一條跨組的代際鏈（推測）**：林萬開鬮書「長子長孫份」裡的馬路下 1 畝 2 分，對上 1947 年林修枝執照上的馬路下 1.20 畝，坑裡、馬坑等土名也重合。由此可接出一條 1875–1947 年的鏈。原文沒有寫兩人的關係。

## 目錄

| 路徑 | 內容 |
|---|---|
| `PLAN.md` | 項目計劃，參考了 GitHub 和 Hugging Face 上的 OCR 與古文項目 |
| `PROGRESS.md` | 階段進展匯報 |
| `app/` | **本地演示網頁**：館藏概覽、憑證譜系、家戶歸戶、林修枝的九坵地、分析與結論、原件對讀 |
| `data/fetch_pitt_land_records.py` | 元數據抓取（Drupal `?_format=json` 和 IIIF manifest） |
| `data/pitt_land_records*.csv` | 235 條記錄；`_linked` 另加本地圖像路徑；`_pages` 每頁圖像一行（407 行） |
| `data/pitt_finding_aid_items.csv` | 檔案目錄 240 條，含中文年號原文日期和盒號、夾號 |
| `data/households/` | 識讀規範 `READING_GUIDE.md`；四組家戶的轉錄、要素和分析（A 永泰黃氏、B 林森林修枝、C 閩侯林萬開、F 建陽劉氏）；合併表 `all_*.csv` |
| `pipeline/` | 本地圖像對應（00）和 IIIF 下載（01） |
| `analysis/` | 各組合併、林修枝組輸出、演示網頁數據導出 |

## 運行演示網頁

1. 把課程提供的圖像包放到 `students_documents_export/images/`，文件名格式為 `<條碼>_<三位頁碼>.jpg`。
2. 在倉庫根目錄運行：

```bash
python -m http.server 8765
```

3. 打開 <http://localhost:8765/app/>。

家戶識讀結果更新後，運行下面兩條命令重新生成頁面數據：

```bash
python analysis/merge_households.py
```

```bash
python analysis/export_app_data.py
```

## 關於圖像和識讀

- **倉庫裡不放任何圖像**。館方標註圖像版權為 Copyright Undetermined，體積也在 200MB 以上。
- 可以通過每條記錄的 `url` 字段到館方網站查看原圖。該網站對腳本的大量請求會彈出人機驗證，請勿繞過。
- 轉錄保留繁體和異體字。〔〕為手寫或戳記填寫的內容，□ 為無法識讀，[?] 為沒有把握。
- 識讀由 AI 完成，關鍵讀數和兩部分之間的分歧都經人工對照原件裁定。引用前請再核對原件。
- 家戶分析嚴格區分「原文寫明」和「推測」，每個結論都註明依據的文書編號（pid）。

## 背景

哈佛大學數字人文課程黑客松項目（2026）。
