# 微信小程序Flex布局及特殊样式课堂笔记

# 一、前期回顾：通用Flex布局

此前讲解的Flex布局相关知识均为通用内容（适用于HTML/CSS，同样可迁移到小程序），已通过2个基础示例完成讲解，后续重点聚焦小程序特有的样式及实战案例。

# 二、小程序特有样式：rpx与px的区别（重点）

## 2.1 核心差异

- **px（像素）**：固定像素值，适用于普通HTML/CSS，但在小程序中不推荐使用。原因：不同设备（手机、iPad等）屏幕尺寸不同，使用px会导致元素大小固定，无法自适应，比如在手机上显示合适的元素，在iPad上会显得很小，周围出现大量空白，无法自动拉伸适配。

- **rpx（响应式像素）**：小程序推荐使用的单位，会根据设备屏幕尺寸自动调节像素长宽，实现自适应。

## 2.2 rpx核心规则

小程序规定：**整个页面的宽度固定为750rpx**（无论设备是iPad、iPhone5/6/7等，页面宽度均为750rpx）。

注意：单个rpx的实际宽度会随设备变化，设备屏幕越大，单个rpx对应的实际像素越宽，从而实现元素自适应拉伸。

## 2.3 示例

图片标签设置为120rpx × 120rpx，在不同设备上会自动适配大小（iPad上会比手机上更大）；结合CSS3的border-radius: 50%，可实现圆形图片效果。

# 三、实战案例3：购物菜单（拍卖专场）布局（结合Flex）

## 3.1 案例需求

实现一个拍卖专场菜单布局，包含：标题、提示信息（时间+浏览次数）、大图、小缩略图，整体采用Flex布局实现元素排列。

## 3.2 结构划分（view标签=HTML中的div标签）

- 最外层view（class="action"）：包裹所有拍卖专场

- 单个拍卖专场view（class="item"）：每个item对应一个拍卖专场，可重复多个

- 专场标题view（class="title"）：显示专场标题（如“公民羊吃的东西拍卖”）

- 提示信息view（class="tips"）：包含2个元素（左侧时间、右侧浏览次数）

- 大图容器view（class="big"）：包裹专场大图

- 小缩略图容器view（class="small"）：包裹多个小缩略图

## 3.3 具体代码与样式设置

### 3.3.1 结构代码（简化）

```html
<view class="action">
  <!-- 单个拍卖专场 -->
  <view class="item">
    <!-- 标题 -->
    <view class="title">第一场 公民羊吃的东西拍卖</view>
    <!-- 提示信息（时间+浏览次数） -->
    <view class="tips">
      <view class="states">2020-0101 11:14为关</view>
      <view class="count">浏览次数</view>
    </view>
    <!-- 大图 -->
    <view class="big">
      <image src="图片路径"></image>
    </view>
    <!-- 小缩略图 -->
    <view class="small">
      <image src="图片路径"></image>
      <image src="图片路径"></image>
      <image src="图片路径"></image>
      <image src="图片路径"></image>
    </view>
  </view>
  <!-- 可添加多个item（多个拍卖专场） -->
</view>
```

### 3.3.2 样式设置（重点Flex+自适应）

- **标题样式（.title）**：字体大小40-50rpx（适配屏幕），字体加粗（font-weight: 600），突出标题。

- **提示信息样式（.tips）**：
        

    - display: flex; flex-direction: row;（横向排列）

    - justify-content: space-between;（两个元素分别靠左右两侧）

    - 字体大小30rpx，颜色#8c8c8c（灰色，区分标题）

- **大图样式（.big + .big image）**：
        

    - .big：设置高度400rpx（固定容器高度），overflow: hidden;（图片超出容器部分隐藏）

    - .big image：width: 100%; height: 100%;（图片占满容器，自动压缩/拉伸，不变形）

- **小缩略图样式（.small + .small image）**：
       

    - .small：display: flex; flex-direction: row; justify-content: flex-start;（横向排列，从左到右依次摆放）

    - .small image：width: 100rpx; height: 100rpx;（固定小图尺寸，适配屏幕）

    - 可选：给图片添加margin-right: 20rpx;（图片之间留间距，更美观）

- **多个专场间距（.item）**：可给item添加margin/padding（单位用rpx），避免多个专场紧挨着。

# 四、关键注意事项

1. 小程序开发中，样式单位优先使用rpx，避免使用px，确保自适应各种设备。

2. 案例布局核心是Flex布局，重点掌握flex-direction、justify-content的用法（横向排列、元素对齐方式）。

3. 图片适配：通过设置容器尺寸+overflow: hidden; 配合图片width: 100%; height: 100%; 实现图片自适应且不溢出。

4. 当前阶段开发，只需关注HTML（小程序view、image等标签）和CSS（样式），无需查看JS文件。

5. Flex布局可灵活调整元素排列，如小缩略图也可通过计算页面宽度（750rpx），分配每个图片的占比，实现均匀排列。
> （注：文档部分内容可能由 AI 生成）