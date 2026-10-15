# sK1 2.0rc5 繁體中文語系（zh_TW）

sK1 2.0rc5 向量繪圖軟體的繁體中文（台灣用語）介面翻譯。官方版本沒有中文，這份翻譯補上全部介面字串。

| 項目 | 內容 |
|---|---|
| 適用版本 | sK1 2.0rc5（翻譯範本 `sk1.pot`，建立日期 2020-02-23） |
| 翻譯字串 | 890 條，全部完成 |
| 語言 | 繁體中文（台灣用語），語言代碼 `zh_TW` |
| 授權 | 依 sK1 專案授權（GPL v3）發布 |

## 檔案說明

| 檔案 | 用途 | 一般使用者需要嗎 |
|---|---|---|
| `sk1.mo` | 編譯好的語系檔，sK1 直接讀取 | **需要**，放進 sK1 就能用 |
| `zh_TW.po` | 翻譯原始檔，可用 Poedit 或文字編輯器修改 | 不需要；想修改翻譯或回報錯誤時使用 |
| `README.md` | 本說明 | — |

簡單說：`.po` 是給人看、給人改的；`.mo` 是給程式讀的。

## 安裝方式

### 1. 找到 sK1 的語系資料夾

sK1 會讀取安裝目錄裡的 `sk1/share/locales/` 資料夾，裡面已經有 `ru`、`fr_FR` 等其他語言的子資料夾。

- **Windows**：在 sK1 安裝資料夾裡搜尋名為 `locales` 的資料夾。
- **Linux**：通常在 `/usr/lib/python2.7/dist-packages/sk1/share/locales/`，或執行下面指令尋找：

```bash
find / -path "*sk1/share/locales" -type d 2>/dev/null
```

### 2. 放入語系檔

照著其他語言的結構，建立 `zh_TW/LC_MESSAGES/` 資料夾，把 `sk1.mo` 放進去：

```
sk1/share/locales/
├── fr_FR/
│   └── LC_MESSAGES/
│       └── sk1.mo
├── ru/
│   └── ...
└── zh_TW/              ← 新建
    └── LC_MESSAGES/    ← 新建
        └── sk1.mo      ← 放這裡
```

Windows 若裝在 `C:\Program Files` 底下，建立資料夾時可能需要系統管理員權限。Linux 請用 `sudo`。

### 3. 切換語言

1. 開啟 sK1，到選單 **Edit → Preferences**（編輯 → 偏好設定）。
2. 選擇 **UI**（介面）頁面。
3. 在 **Language (\*)**（語言）選擇 `zh_TW`。
4. 關閉 sK1 再重新開啟。標示 (\*) 的選項都需要重新啟動才會生效。

語言選單的項目就是 `locales` 底下的資料夾名稱，所以資料夾一定要叫 `zh_TW`，才會出現在選單裡。

## 修改翻譯

1. 用 [Poedit](https://poedit.net/) 開啟 `zh_TW.po`，修改譯文後儲存。Poedit 會在同一個資料夾自動產生 `.mo` 檔。
2. 把產生的 `.mo` 檔改名為 `sk1.mo`，覆蓋到 `zh_TW/LC_MESSAGES/`。
3. 重新啟動 sK1。

不用 Poedit 也可以用指令編譯，下列方法擇一：

```bash
msgfmt -c zh_TW.po -o sk1.mo                                                  # GNU gettext（-c 會檢查格式錯誤）
python -c "import polib; polib.pofile('zh_TW.po').save_as_mofile('sk1.mo')"   # Python（需先 pip install polib）
pybabel compile -i zh_TW.po -o sk1.mo                                          # Babel（需先 pip install babel）
```

翻譯注意事項：

- `%s`、`%i`、`%d` 是程式要填入的數值，數量和順序必須和英文原文相同，否則 sK1 可能出錯。
- 選單裡的 `&` 是快捷鍵標記，例如 `&File` 譯為 `檔案(&F)`，請保留這種寫法。

## 已知限制

- **少數字串仍為英文**：部分字串直接寫在程式碼裡，沒有放進翻譯範本，無法透過語系檔翻譯。
- **介面字型**：系統沒有中文字型時，介面的中文會顯示成方框。Linux 可安裝 `fonts-noto-cjk`。
- **字型清單的問題（sK1 本身的程式問題，與翻譯無關）**：依原始碼分析，sK1 的字型清單按位元組排序，中文名稱的字型會排在清單**最後面**；部分字型的名稱可能顯示成空白，但選取後仍能正常套用。
- 這份翻譯只對應 2.0rc5。如果之後的版本新增或修改了字串，需要用新的 `sk1.pot` 合併更新：

```bash
msgmerge -U zh_TW.po sk1.pot
```

## 回饋與貢獻

- 發現翻譯錯誤或用語不妥，歡迎直接修改 `zh_TW.po`，或回報給發布者。
- 想讓更多人用到，可以把 `zh_TW.po` 以 Pull Request 提交到 sK1 官方專案的 `po-sk1/` 資料夾（[sk1-project/sk1-wx](https://github.com/sk1-project/sk1-wx)）。開源專案只收 `.po` 原始檔，`.mo` 會在建置時自動產生。
