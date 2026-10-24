# 磐达体系 · 品牌锚点权威发布件（panda-brand-anchors）

本仓库是磐达体系品牌指纹的**权威发布源**，仅供 `brand_gate.py` 云锚关联网比对使用。

## 发布形态（分片清单）

- 锚表按 118 条/片切分为 4 片：`anchors/part0.json` ~ `anchors/part3.json`
- 入口清单：`anchors/manifest.json`（列出 parts 顺序，`file_count` 为总条数）
- 每片 schema：`panda-anchors-v1`，files 仅含 `sha256`（跨体系同名文件靠内容区分）

## 客户侧校验（云锚关）

```
python brand_gate.py check <目标文件> --root <本地锚表目录> --online <manifest URL>
```

- `--online` 指向本仓库 Pages 发布的 `anchors/manifest.json` 固定 URL
- 脚本自动下载 manifest → 合并 4 片 → 集合比对目标文件实际 sha256
- 网络不可达或文件不在权威表 → 报错不静默放行

## 启用 GitHub Pages（一次性）

1. 仓库 Settings → Pages
2. Source 选 `main` 分支 / root
3. 固定 URL 形如：`https://<owner>.github.io/panda-brand-anchors/anchors/manifest.json`

## 更新发布件

1. 本地 `brand_gate.py publish` 重生成 `published_anchors.json`
2. 按 118 条/片重新分片并推送 `anchors/part*.json`
3. 更新并推送 `anchors/manifest.json`（version/file_count/parts 同步）