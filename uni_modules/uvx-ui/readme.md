# uvx-ui

`uvx-ui` 是一个面向 [uni-app x](https://doc.dcloud.net.cn/uni-app-x/) 的跨平台 UI 组件库，使用 UTS 和 UVUE 编写，提供布局、表单、导航、数据展示和操作反馈等常用组件。

- 官方文档：<https://www.uvxui.cn/>
- 源码仓库：<https://gitee.com/toothdy/uvx-ui>

## 环境要求

- HBuilderX 3.9.0 及以上版本
- uni-app x 5.21 及以上版本
- Vue 3

建议使用最新稳定版 HBuilderX。各组件的属性、事件和平台兼容性请查看[uvx-ui 官方文档](https://www.uvxui.cn/)。

## 安装

访问 [uvx-ui 插件市场](https://ext.dcloud.net.cn/plugin?name=uvx-ui)，点击“使用 HBuilderX 导入插件”，选择目标 uni-app x 项目完成安装。如有依赖安装提示，请按照 HBuilderX 的提示一并安装。

当前版本会读取项目根目录中的业务语言包，请同时准备：

```text
locales/
├── en.json
├── zh-cn.json
└── zh-tw.json
```

## 快速上手

### 1. 配置 easycom

在项目根目录的 `pages.json` 中添加组件映射：

```json
{
  "easycom": {
    "autoscan": true,
    "custom": {
      "^uvx-(.*)": "@uni_modules/uvx-ui/components/uvx-$1/uvx-$1.uvue"
    }
  }
}
```

### 2. 注册 uvx-ui

在 `main.uts` 中安装插件：

```ts
import App from "./App.uvue";
import { createSSRApp } from "vue";
import uvxui from "@/uni_modules/uvx-ui/index.uts";

export function createApp() {
  const app = createSSRApp(App);
  app.use(uvxui);

  return {
    app,
  };
}
```

### 3. 引入样式

在 `App.uvue` 中引入组件库全局样式：

```vue
<style lang="scss">
@import "@/uni_modules/uvx-ui/index.scss";
</style>
```

如需在业务样式中使用 uvx-ui 的 SCSS 主题变量，请在 `uni.scss` 中引入：

```scss
@import "@/uni_modules/uvx-ui/theme.scss";
```

### 4. 使用组件

easycom 配置完成后，无需在页面中手动导入组件：

```vue
<template>
  <uvx-page>
    <uvx-button text="主要按钮" type="primary" @click="handleClick" />
  </uvx-page>
</template>

<script setup lang="uts">
const handleClick = () => {
  uni.showToast({
    title: "点击成功",
  });
};
</script>
```

## 更多用法

请访问 [uvx-ui 官方文档](https://www.uvxui.cn/) 查看组件列表、API、示例和兼容性说明。
