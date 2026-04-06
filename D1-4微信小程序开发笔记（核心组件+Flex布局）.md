# 微信小程序开发笔记（核心组件+Flex布局）

# 一、小程序全局配置

1.  全局配置文件：所有全局配置均写在最外层的 `app.json` 中，后续用到其他配置再补充添加。

2.  配置优先级：页面自身也有对应配置，但现阶段暂不使用，全部统一采用全局配置。

3.  配置后续：完成全局配置后，即可开始逐个编写具体页面。

# 二、微信小程序核心组件（重点掌握3个）

说明：小程序中“标签”称为「组件」，以下3个核心组件可实现80%-90%的小程序页面功能，其余组件（地图、媒体、表单等）可在官方文档中按需查询，无需逐一记忆，以实际功能需求为导向即可。

## 2.1 text组件（3.2.1）

作用：用于编写文本信息。

类比：类似于传统HTML中的 `span` 标签，默认不独占一整行（行内元素特性）。

## 2.2 view组件（3.2.2）

作用：用于页面布局，充当容器（盒子模型），承载其他组件。

类比：类似于传统HTML中的 `div` 标签（块级元素特性）。

## 2.3 image组件（3.2.3）

作用：用于展示图片。

使用要点：通过 `src` 属性指定图片路径，例如 `src="static/海狗.jpg"`（路径需准确）。

## 补充说明

1.  组件默认自带基础样式，可通过自定义样式修改。

2.  其他组件（如表单input、视频等），因有HTML基础，后续按需学习即可，无需现阶段掌握。

# 三、Flex布局（重点，页面布局核心）

说明：Flex布局并非微信小程序特有，是HTML、CSS通用的布局方式，掌握后可快速完成各类页面布局。

## 3.1 核心概念（必记）

1.  主轴：由 `flex-direction` 规定，决定子元素的排列方向（水平/垂直）。

2.  副轴（纵轴）：与主轴垂直，决定子元素在垂直于主轴方向的对齐方式。

3.  适用对象：给「容器」添加Flex样式，容器的子元素会按照Flex规则排列。

## 3.2 核心样式属性（4个必记，搞定大部分布局）

### 3.2.1 display: flex

作用：给容器添加该样式，使容器变为Flex容器，其内部子元素按Flex规则排列。

### 3.2.2 flex-direction（规定主轴方向）

- `row`（默认）：主轴为水平方向，子元素从左到右排列（最常用）。

- `row-reverse`：主轴为水平方向，子元素从右到左排列（较少用）。

- `column`：主轴为垂直方向，子元素从上到下排列。

### 3.2.3 justify-content（规定子元素在主轴方向的排列方式）

- `flex-start`（默认）：子元素靠主轴起始端排列（水平方向即居左）。

- `center`：子元素在主轴方向居中排列。

- `space-around`：子元素平均分布在主轴上，两端留有相等空白（常用，适合菜单布局）。

- `space-between`：子元素两端对齐，中间空白平均分配（两端贴边，中间均分）。

### 3.2.4 align-items（规定子元素在副轴方向的对齐方式）

- `flex-start`（默认）：子元素靠副轴起始端排列。

- `center`：子元素在副轴方向居中排列（常用，使内部元素垂直居中）。

- `flex-end`：子元素靠副轴末端排列。

## 3.3 补充样式（实用）

1.  图片尺寸：使用 `rpx` 单位（小程序适配不同屏幕的专用单位，区别于HTML的 `px`），例如 `width: 100rpx`。

2.  图片圆角：使用 `border-radius: 50rpx`，可将图片设置为圆形（常用於菜单图标）。

3.  边框：使用 `border: 1rpx solid #ddd`，可给容器添加边框，便于调试布局。

## 3.4 实操示例（2个核心案例，贴合开发场景）

### 示例一：基础菜单布局（水平排列，内部上下对齐）

需求：4个菜单，每个菜单包含图片+文本，整体水平平均分布，每个菜单内部图片+文本上下排列、居中对齐。

核心代码逻辑（简化）：

```html
<!-- 外层容器：flex布局，水平平均分布 -->
&lt;view class="menu"&gt;
  <!-- 每个菜单项：flex布局，垂直排列，内部居中 -->
  <view class="item">
    <image src="static/xxx.jpg"></image>
    <text>精品视频</text>
  </view>
  <view class="item"&gt;...&lt;/view&gt; <!-- 重复3个，共4个菜单 -->
</view&gt;

<!-- 样式 -->
.menu {
  display: flex;          /* 容器变为flex */
  flex-direction: row;    /* 主轴水平 */
  justify-content: space-around; /* 水平平均分布 */
}
.item {
  display: flex;          /* 子容器也为flex */
  flex-direction: column; /* 主轴垂直（内部上下排列） */
  align-items: center;    /* 副轴居中（内部元素垂直居中） */
}
image {
  width: 100rpx;          /* 图片尺寸适配 */
  border-radius: 50rpx;   /* 图片圆形 */
}
    
```

### 示例二：纯图片菜单布局（水平排列）

需求：仅展示图片菜单，水平平均分布，无需文本。

核心代码逻辑（简化）：

```html

<view class="menu1">
  <image src="static/xxx.jpg"></image>
  <image src="static/xxx.jpg"></image>
  <image src="static/xxx.jpg"></image>
</view&gt;

<!-- 样式 -->
.menu1 {
  display: flex;
  flex-direction: row;
  justify-content: space-around;
}
image {
  width: 100rpx;
  border-radius: 50rpx;
}
    
```

# 四、Flex布局总结（必背）

- 1.  布局核心：给容器添加 `display: flex`，通过2个方向属性（flex-direction、justify-content、align-items）控制子元素排列。

- 2.  重点属性：记准 `flex-direction`（主轴方向）、`justify-content`（主轴排列）、`align-items`（副轴对齐），即可搞定大部分页面布局。

- 3.  实用技巧：图片适配用 `rpx`，圆形图标用 `border-radius: 50rpx`；复杂布局可嵌套Flex（外层容器+内层子容器均设为flex）。

- 4.  组件配合：view（容器）+ text（文本）+ image（图片）+ Flex布局，可实现绝大多数小程序基础页面。

# 五、复习提示

1.  开发时遇到布局问题，优先查看Flex布局的3个核心属性（flex-direction、justify-content、align-items），确认主轴/副轴方向及排列方式。

2.  组件使用疑问，可直接查询微信小程序官方文档的“组件”板块，按需查找即可，无需死记所有组件。

3.  路径问题：image组件的src路径需准确（如示例中的static文件夹），避免图片无法显示。
> （注：文档部分内容可能由 AI 生成）