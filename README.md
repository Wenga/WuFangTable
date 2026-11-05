# 五方入味 · 寻味五城

独立的静态网页，面向活动现场 iPad Pro 横屏。点击地图或底部城市按钮，自由浏览五城；切换菜品与茶饮，模型默认以每秒 15° 水平循环旋转（24 秒一圈）；拖拽时手动旋转，松开后约 1.5 秒恢复自动旋转。不提供缩放或复位按钮。保留简体中文、繁体中文、English，语言选择只保存在当前浏览器。

## 发布到 GitHub Pages

此目录无需 npm 安装、构建或后端服务。

- 使用当前仓库：提交完整 `docs/` 目录，在仓库 **Settings → Pages → Deploy from a branch** 中选择你的发布分支与 **`/docs`**，保存。
- 使用新的独立仓库：把此目录**里面的所有文件**（包括 `.nojekyll` 和 `assets/`）放到新仓库根目录，Pages 选择发布分支与 **`/(root)`**。

站内资源全部使用相对路径，可部署到 `https://用户名.github.io/仓库名/`。不要只上传 HTML；模型和本地查看器也必须一起上传。网页总量约 45 MB，无超过 GitHub 普通文件限制的文件。

## 本地预览

在 `WuFang` 项目目录运行：

```sh
python3 -m http.server 4173
```

打开 `http://localhost:4173/docs/`。请通过 HTTP 打开，不要直接双击 HTML。

## 内容与模型

- 城市、界面翻译和模型切换：`app.js`。
- 菜茶三语介绍及资料链接：`culture-data.js`，沿用原互动网页。
- 样式：`style.css`，沿用米白纸底、水墨背景、楷宋字体、灰绿与印章色。
- 模型：`assets/models/*.glb`；每次只展示一个，按需加载。
- 来源版本：`assets/models/sources.json`，路径相对于原 `wufang_3d/output`。
- 本地查看器：Google `<model-viewer>` 4.1.0；说明及许可证见 `THIRD_PARTY.md`。

模型沿用原有 Blender 几何，烘焙程序化基础颜色、保留青花等纹理，并为移动端调整玻璃和茶汤透明度。它们是原项目的程序化重建模型；网页实时材质与 Blender 离线渲染不完全一致。源 `.blend` 文件未修改。重新导出工具位于项目的 `scripts/export-web-models.py` 和 `scripts/prepare-web-materials.py`。

## 验证与现场使用

已在浏览器检查十个模型、三语切换、地图选城、菜茶切换、自动旋转、鼠标拖拽旋转与禁止缩放，以及 1366×1024 和 1194×834 横屏布局。还需在实际 iPad Safari 上验证拖拽手势和现场网络表现。

核心资源均随站点提供，无运行时 CDN 依赖；资料出处链接需要互联网。没有实现完整离线缓存，不能保证断网后刷新或打开未访问的模型。首次打开较大的模型需要下载几 MB。

## 柔光材质版本

十个模型统一使用本地 `assets/soft-studio.hdr` 柔光环境，减淡接触阴影，并按瓷器、玻璃、茶汤、食物设置不同粗糙度。盐水鸭移除了误导出的照片法线贴图。重导出后依次运行 `scripts/prepare-web-materials.py`、`scripts/refine-duck.py`、`scripts/refine-soft-materials.py`；最后一个脚本使用 `output/atlas/material-backups/` 中的原始导出备份，若重建了源模型，应先另行归档旧备份再重建新备份。模型提示在查看器下方独立排版。

玻璃杯专项调整：执行上述材质步骤后运行 `scripts/refine-glass.py`，调整广州、沈阳玻璃杯的灰青色轮廓、清漆反射与茶汤透明度。
