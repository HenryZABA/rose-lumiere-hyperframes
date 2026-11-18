# Rose Lumière · HyperFrames 案例视频模板

用一段项目录屏制作 16:9 的案例展示视频。左侧以模拟构建对话逐字输出制作过程，文件完成时出现图标。右上播放完整成品，右下随镜头切换辅助内容。本例为 1920 × 1080、22 秒、无声，带可直接播放的示例素材。

## 本地预览

准备 Node.js 22+、npm 和 FFmpeg。首次运行需要联网下载固定版本的 HyperFrames CLI。

```sh
git clone https://github.com/HenryZABA/rose-lumiere-hyperframes.git
cd rose-lumiere-hyperframes
npm run dev
```

打开终端打印的本地预览地址，按播放或拖动时间线。修改文件后预览会自动更新。

## 换成自己的项目

1. **成品录屏。** 将新录屏放入 `assets/project/`。在 `index.html` 里更新 `video` 变量的默认路径和 `#result` 的 `src`，同时更新 `projectName` 与左栏标题。当前主视频设为静音。
2. **左侧构建对话。** 打开 `compositions/layout.html`，修改 `.bubble` 中的用户需求，以及各 `.entry` 内 `template.copy` 的英文台词，可直接改成中文。`data-from` 和 `data-until` 是逐字输出的起止秒数。时间段首尾相接即可连续输出。每条末尾的 `.filechip` 包含文件名和 SVG 图标，可以换成项目对应的图片或代码文件。台词为演示编写，界面已标注模拟构建过程。
3. **右下随镜头变化。** 在同一文件的 `#support-slot` 内编辑展示内容。每个 `.study` 都是独立的 HTML 区域，可用一幅素材、多图对照、流程步骤或 SVG 音频波形。音乐案例可以把该段的图片和文字替换为横向音轨，并用布局时间线 `tl` 同步播放指示线。实际声音需要在主工程中另加音频轨。本例 0 秒显示建筑底图，4 秒切到彩窗构图，8.5 秒切中心花纹，19 秒切地面投光。切换点在文件末尾的时间表中。增删段落时同时更新对应的选择器、初始透明度和时间表。
4. **片长。** 若录屏不是 22 秒，在 `index.html` 中同步调整根画布、布局和视频的 `data-duration`。在 `layout.html` 里更新输出时钟的 `time`、`duration` 及滚动测量循环的帧数（片长 × 30），再按镜头调整对话与辅助区时间点。

## 检查与导出 MP4

```sh
npm run check
mkdir -p renders
npm run render -- --fps 30 --quality delivery --output renders/case-study.mp4
```

主视频、图片、字体与动画依赖随仓库提供。示例界面使用 Enter 品牌素材，复用到其他品牌时可替换 `assets/brand/enter-logo.png`。
