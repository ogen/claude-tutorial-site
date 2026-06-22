# Claude Tutorial Site — MkDocs 建置說明

## 專案說明

這個專案將 `/Users/ogen/Documents/claude-tutorial/` 的 Markdown 教學文件，透過 MkDocs + Material theme 轉換成 HTML 靜態網站。

兩個專案完全獨立，原始 Markdown 檔案一字不動。

## 目錄結構

```
claude-tutorial-site/          ← 本專案（MkDocs 網站）
├── CLAUDE.md                  ← 本說明文件
├── mkdocs.yml                 ← 網站設定（導覽、主題、外掛）
├── docs/                      ← MkDocs 讀取的文件根目錄
│   ├── index.md               ← 首頁（00_learning-roadmap.md 的複本）
│   ├── 00_windows-differences.md  ← 符號連結 → 原專案
│   ├── 00_learning-roadmap.md     ← 符號連結 → 原專案（供內部連結解析用）
│   ├── module1-overview/      ← 符號連結 → 原專案
│   ├── module2-claudeai/      ← 符號連結 → 原專案
│   ├── module3-desktop-mcp/   ← 符號連結 → 原專案
│   ├── module4-claude-code/   ← 符號連結 → 原專案
│   ├── module5-skills/        ← 符號連結 → 原專案
│   ├── module6-api/           ← 符號連結 → 原專案
│   ├── module7-automation/    ← 符號連結 → 原專案
│   ├── module8-enterprise/    ← 符號連結 → 原專案
│   ├── module9-ai-ecosystem/  ← 符號連結 → 原專案
│   └── module10-capstone/     ← 符號連結 → 原專案
└── site/                      ← 產生的 HTML 靜態檔（不進 git）
```

### 符號連結設計原則

docs/ 下的模組資料夾全部是符號連結，指向原專案。好處是：
- 原專案更新 Markdown，重新 build 網站就能同步，不需要手動複製
- `index.md` 是例外，用複製而非連結，因為首頁需要獨立存在

`00_windows-differences.md` 和 `00_learning-roadmap.md` 放在 docs 根目錄（而非子目錄），原因是原始 Markdown 檔案內的相對連結（如 `../00_windows-differences.md`）需要能從模組資料夾回到 docs 根目錄才能解析。

## 環境需求

```bash
pip install mkdocs mkdocs-material
```

## 常用指令

```bash
# 本地預覽（即時重新整理）
mkdocs serve
# → 瀏覽器開 http://localhost:8000

# 建置靜態 HTML
mkdocs build
# → 輸出到 site/ 目錄

# 部署到 GitHub Pages
mkdocs gh-deploy
# → 需先在 GitHub 建立 repo 並設定 remote
```

## 初始建置步驟（記錄用）

第一次從零建起這個專案的完整步驟：

**1. 安裝套件**
```bash
pip install mkdocs mkdocs-material
```

**2. 建立 MkDocs 專案**
```bash
cd /Users/ogen/Documents
mkdocs new claude-tutorial-site
```

**3. 建立 docs/ 結構**
```bash
SRC=/Users/ogen/Documents/claude-tutorial
DOCS=/Users/ogen/Documents/claude-tutorial-site/docs

# 首頁：複製學習路徑總覽
cp "$SRC/00_learning-roadmap.md" "$DOCS/index.md"

# 根目錄連結（供內部連結路徑解析）
ln -s "$SRC/00_windows-differences.md" "$DOCS/00_windows-differences.md"
ln -s "$SRC/00_learning-roadmap.md"    "$DOCS/00_learning-roadmap.md"

# 各模組目錄符號連結
for dir in module1-overview module2-claudeai module3-desktop-mcp \
            module4-claude-code module5-skills module6-api \
            module7-automation module8-enterprise \
            module9-ai-ecosystem module10-capstone; do
  ln -s "$SRC/$dir" "$DOCS/$dir"
done
```

**4. 設定 mkdocs.yml**

參見本目錄的 `mkdocs.yml`，主要設定：
- `theme.name: material`、`language: zh-TW`
- 深色 / 淺色主題切換
- 程式碼複製按鈕、全文搜尋、頁籤導覽
- 完整的 30 章 `nav` 導覽結構

**5. 驗證建置**
```bash
mkdocs build
```

預期只剩 MkDocs 2.0 的版本聲明警告（無連結錯誤）。

## 連結警告處理記錄

build 過程遇到的連結問題與解法：

| 警告 | 原因 | 解法 |
|------|------|------|
| `index.md` → `00_windows-differences.md` 找不到 | 原本放在 `appendix/` | 移到 docs 根目錄 |
| `appendix/windows-differences.md` 內部連結跑掉 | 從子目錄出發路徑錯位 | 移除 appendix/，改放根目錄 |
| `30_taiwan-stock-agent.md` → `../00_learning-roadmap.md` | 首頁已改名為 index.md | 在根目錄補符號連結 |
| `18_api-setup.md`、`22_automation-workflows.md` → `../00_windows-differences.md` | 原路徑指向根目錄，但檔案在 appendix/ | 移到根目錄後路徑自動對上 |

## 新增模組時的更新清單

原專案新增章節後，同步到網站的步驟：

1. 若新增了模組資料夾：在 `docs/` 補符號連結
   ```bash
   ln -s /Users/ogen/Documents/claude-tutorial/module11-xxx \
         /Users/ogen/Documents/claude-tutorial-site/docs/module11-xxx
   ```
2. 在 `mkdocs.yml` 的 `nav:` 區塊加入新章節路徑
3. 執行 `mkdocs build` 確認無警告
4. 執行 `mkdocs serve` 預覽確認

## 部署

### GitHub Pages（已完成）

網站網址：https://ogen.github.io/claude-tutorial-site/

更新網站只需一個指令：

```bash
cd /Users/ogen/Documents/claude-tutorial-site && mkdocs gh-deploy
```

執行後會自動 build 並推送到 `gh-pages` branch，約 1-2 分鐘生效。

### 其他選項（備用）
- **Netlify / Vercel**：連結 GitHub repo，push 自動觸發 build
