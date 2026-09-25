# 游戏大厅 · game.guatama5400.xyz

浏览器小游戏合集，托管在 GitHub Pages，推送到 `main` 分支即自动上线。

在线地址：https://game.guatama5400.xyz/

## 目录结构
```
/index.html          大厅首页（读取 games.json 自动生成游戏卡片，一般不需要改）
/games.json          游戏清单，上架新游戏就在这里加一条
/CNAME               自定义域名，不要删除或修改
/<game-id>/          每个游戏一个独立目录
    index.html       游戏入口
    cover.jpg        封面（16:9，建议 960×540，< 200KB）
```

## 已上架
| 游戏 | 路径 |
|---|---|
| 星际战车-UU共创版 Planet Tanks | `/planet-tanks/` |
| 飞车 3D Cyber Drift 3D | `/feiche-3d/` |
| 鹈鹕骑单车 Pelican on a Bike | `/pelican-bike/` |
| 穿越火线·运输船 Transport Ship | `/cf-transport-ship/` |

## 上架新游戏
见 [CLAUDE.md](CLAUDE.md) 中的规范。
