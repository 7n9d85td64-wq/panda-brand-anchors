# 磐达品牌指纹权威发布件（panda-brand-anchors）

本仓库是「磐达体系」品牌防篡改机制的权威指纹源（Git Pages 固定 URL 用）。

## 仓库内容

- `published_anchors.json` — 全部体系文件的品牌指纹发布件（sha256 + brand + watermark_id，V1.6，472 文件）

## 客户侧校验方法

```bash
# 1. 下载权威发布件到本机（或用 --online 直接比对）
# 2. 校验任意体系核心文件三关：品牌关 / 完整性关 / 授权关
python brand_gate.py check <目标文件> --root <指纹表目录> --online <本仓库 Pages URL>/published_anchors.json
```

- 品牌关：文件 frontmatter 带 brand 标识
- 完整性关：文件 sha256 与发布件一致（被篡改立即报错）
- 授权关：本机授权码哈希在服务方台账中

## 更新

发布件由服务方 `publish_anchors.py` 生成（版本号递增），推送到本仓库后即生效。

© 磐达体系 2026