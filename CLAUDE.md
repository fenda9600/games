# 游戏大厅仓库规范（给 AI 助手 / 协作者）

本仓库通过 GitHub Pages 发布到 https://game.guatama5400.xyz/ （`main` 分支根目录，推送后约 1 分钟生效）。

## 上架一款新游戏的步骤
1. **选 id**：小写英文 + 连字符，例如 `snake-3d`。不得与现有目录重名。
2. **建目录** `/<id>/`，游戏入口为 `/<id>/index.html`。游戏的所有资源放在这个目录内。
3. **路径**：游戏内部引用自身资源一律用相对路径（`./img/a.png`），不要用 `/img/a.png`，否则会指向站点根目录。
4. **返回大厅**：在游戏主菜单/标题界面放一个返回按钮，链接 `href="/"`，文案「🏠 大厅」。
5. **存档隔离**：所有游戏共享同一个域名，localStorage / IndexedDB 的 key 必须以游戏 id 为前缀（例如 `snake-3d-save-v1`）。严禁调用 `localStorage.clear()`，它会清空其他游戏的存档。
6. **封面** `/<id>/cover.jpg`：16:9，建议 960×540，JPEG，小于 200KB，最好是真实游戏画面截图。
7. **登记到 `/games.json`** 的 `games` 数组末尾追加一项：
   ```json
   {
     "id": "snake-3d",
     "title": "中文名",
     "subtitle": "English Name",
     "description": "一两句话的玩法介绍（40~60 字）",
     "path": "/snake-3d/",
     "cover": "/snake-3d/cover.jpg",
     "icon": "🐍",
     "accent": "#7CFF6B",
     "tags": ["休闲", "单机"],
     "controls": "键盘 / 触屏",
     "added": "YYYY-MM-DD"
   }
   ```
   - `path` 必须以 `/` 开头和结尾；`accent` 是 6 位十六进制颜色，用作卡片高亮色；`added` 填上架当天日期（14 天内卡片会显示 NEW）。
   - 修改后确认 JSON 合法：`python3 -m json.tool games.json`。
8. **更新 README.md** 的「已上架」表格。
9. **本地验证**：在仓库根目录 `python3 -m http.server 8000`，打开 `http://localhost:8000/` 确认大厅出现新卡片、封面正常、点击能进入游戏、游戏内「大厅」按钮能返回。
10. **提交推送**到 `main`，等待 Pages 构建完成（`gh api repos/<owner>/<repo>/pages/builds/latest --jq .status` 为 `built`），再访问线上地址确认。

## 禁止事项
- 不要修改或删除 `CNAME`，不要修改 GitHub Pages 设置。
- 除非明确要求，不要修改大厅 `/index.html` 和其他游戏目录。
- 不要引入需要构建步骤的框架产物以外的东西到根目录；如游戏需要构建，只提交构建后的静态文件到 `/<id>/`。
- 不要提交大于 20MB 的单个文件。
