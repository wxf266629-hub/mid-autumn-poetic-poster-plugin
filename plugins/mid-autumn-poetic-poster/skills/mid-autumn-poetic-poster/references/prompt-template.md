# Prompt 组装模板

将方括号内容替换后再发送给图像生成或设计工具。用户要准确的中文时，默认先生成无字背景，随后添加可编辑文字层。只有工具明确支持可靠排版或用户明确要“一次生成带字图”，才把中文标题和诗句放进图像 Prompt。

## 中文模板

```text
[画幅：1242×2208 手机竖版 / 50×150mm 书签]，中秋古风诗意画面，主题为「[主题]」，情绪为「[情绪]」。
主视觉是「[主视觉]」，必须成为唯一视觉焦点；前景「[前景]」，中景「[中景]」，远景「[远景]」。
中国水墨与水彩结合，轻宣纸纤维，柔和边缘，低饱和「[色彩]」，电影感月光与薄雾，局部留白，画面像一幅可以进入其中的东方长卷。
金箔只作为光感，限制在「[金箔位置]」，少量碎金颗粒或水面反光，不做装饰贴纸。
在「[文字位置]」预留平静、可读的题字区，不在背景中绘制任何汉字、印章或标点。后期排版层：标题「[标题]」使用可辨识的毛笔书法；已核实诗词「[诗句无标点]」竖排或窄列；出处「[朝代 作者 作品名]」小号排列。默认不加红色刻章。
负面约束：元素堆砌，平均分布，缺乏留白，现代扁平插画，过度摄影写实，塑料质感，粗颗粒脏纸，满屏金箔，大红大金，粗金描边，月光直线，错误汉字，错误诗句，错误作者，逗号句号和其他标点，自动红色印章。
```

## 英文辅助模板

```text
Vertical Chinese Mid-Autumn poetic poster, [size], theme “[theme]”, [mood].
One dominant focal subject: [subject]. Foreground [foreground], middle ground [middle ground], distant background [background].
Elegant Chinese ink wash and watercolor on subtly textured warm rice paper, soft edges, restrained low-saturation [palette], atmospheric moonlight and mist, generous negative space, cinematic oriental scroll-like depth.
Subtle gold leaf only as light accents on [locations], sparse and irregular, never decorative glitter.
Reserve a calm, readable area for later editable typography. Render no Chinese characters or seal in the background. Later text layers: legible brush calligraphy title “[title]”, verified poem “[poem without punctuation]”, small source “[source]”; no red seal by default.
Avoid clutter, equal visual weight, flat modern illustration, glossy photorealism, plastic flowers or food, dirty paper, excessive gold, bright red-and-gold festival style, straight moon reflection, malformed Chinese characters, incorrect poem, punctuation, automatic red stamp.
```

## 组装顺序

1. 用主题库确定主视觉和月亮尺度。
2. 只补一个中景和一个远景，避免自动堆元素。
3. 用情绪决定冷暖，不让金箔替代光影。
4. 默认为文字预留干净区域，把标题、诗句、出处作为后期可编辑层；若用户明确要求图片直接带字，做逐字校对。
5. 把主题专属负面约束放在通用负面约束之后，例如归雁追加“birds remain dominant, moon stays small and pale”。

## 交付包的最小内容

- 成图请求：实际图像或明确说明无法生成；另附主题、尺寸、已核实诗句与出处，以及可编辑文字层说明。
- Prompt 请求：正向 Prompt、负面约束、文字层内容、尺寸；用户可以直接复制。
- 系列请求：先给系列基准，再列每张的主视觉、色调、诗句和差异。
- 印刷请求：交付成品尺寸、文件像素、出血与安全区说明；若印厂规范未给出，标记为待确认值。
