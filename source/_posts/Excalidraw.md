---
title: excalidraw添加中文手写体
categories: 实用技巧
tags: 
    - Excalidraw
    - Nodejs
    - Yarn
    - Git
date: 2023-08-19 15:00:00
description: 实用画图工具excalidraw
cover: https://tttuuuchuang.oss-cn-wulanchabu.aliyuncs.com/uploads/2023/08/19/4-2023-08-19-1530.png
top_img: rgba(0,0,0,0)
---
## Excalidraw

之前一直用mermaid画图，苦于格式限定的太死板，所以找到一款好用的画板[Excalidraw ](https://excalidraw.com/)辅助画图

使用过程中发现了一些问题

excalidraw的手写体不支持中文，看起来十分违和

![](https://tttuuuchuang.oss-cn-wulanchabu.aliyuncs.com/uploads/2023/08/19/2023-08-19-1120.png)

所以通过本地部署，导入中文手写字体的方法解决问题

采用了[沐瑶软笔手写体](https://www.fonts.net.cn/font-35068393713.html)，效果如下

![](https://tttuuuchuang.oss-cn-wulanchabu.aliyuncs.com/uploads/2023/08/19/1-2023-08-19-1120.png)

## 本地部署

### 环境

- Git
- yarn
- Nodejs

### 克隆代码

```bash
git clone https://github.com/excalidraw/excalidraw.git
```

### 安装依赖

```bash
yarn
```

### 启动

```bash
yarn start
```

可以在https://localhost:3000运行使用了



## 添加中文手写字体

### 添加字体

- 在``public``目录中加入字体文件 ``example.ttf``
- 在``public/fonts.css``添加对应字体引入

```css
@font-face {
    font-family: "example";
    src: url("example.ttf");
    font-display: swap;
}
```

- 在``src/index-node.ts``注册字体

```ts
registerFont("./public/example.ttf", { family: "example"});
```



### 添加常量

- 在``src/constant.ts``中的``FONT-FAMILY``常量中添加font

```ts	
export const FONT_FAMILY = {
    Virgil: 1,
    Helvetica: 2,
    Cascadia: 3,
    example: 4,  //该行为新增内容， example对应添加字体时的font-family
};
```



### 添加按钮

- 在``/src/actions/actionProperties.tsx``中``actionChangeFontFamily``添加

```tsx
export const actionChangeFontFamily = register({
    ...
    PanelComponent: 
    	...
    	//以下内容为新增
    	{
            value: FONT_FAMILY.example,
            text: "中文手写",
            icon:  FreedrawIcon,
        }
})
```



### 预加载字体资源

- ``index.html``

```html
<link
	rel="preload"
	href="example.ttf"
	as="font"
	type="font/ttf"
	crossorigin="anonymous"
	/>
```



## 部署gitpage

```b
yarn build
```

将``build``文件夹内文件push到 ``username.github.io``的项目仓库中即可

网站[在此](https://xiaopangwa99.github.io/)

