# uvx-ui

面向 [uni-app x](https://doc.dcloud.net.cn/uni-app-x/) 的 UTS UI 组件库，提供基础、表单、数据展示、反馈、布局和导航等常用组件，并附带可直接运行的示例工程。

- 使用 UTS 与 `.uvue` 编写，遵循 uni-app x 强类型约束
- 通过 easycom 自动发现 `uvx-*` 组件，无需逐个导入
- 内置主题变量、暗色模式和中英繁三种语言资源
- 提供 Android、iOS、HarmonyOS、Web 和微信小程序相关的条件编译实现
- 示例工程启用 uni-app x 蒸汽模式（Vapor）与字节码渲染

> 各组件的平台实现程度不同，正式使用前请在目标平台运行对应示例验证。当前模块元数据尚未发布完整的平台兼容性矩阵。

## 相关链接

- [Gitee 仓库](https://gitee.com/toothdy/uvx-ui)
- [uni-app x 文档](https://doc.dcloud.net.cn/uni-app-x/)

## 环境要求

本仓库没有 Node.js 工程配置，使用 HBuilderX 打开和运行。

| 环境 | 最低版本 | 说明 |
| --- | --- | --- |
| HBuilderX | 4.14 | 取依赖模块声明的最高要求 |
| uni-app x | 4.74 | `lime-dayuts` 的最低要求 |
| Vue | 3 | 项目使用 Vue 3 与组合式 API |

建议使用最新稳定版 HBuilderX。不同发行目标还需要安装相应的模拟器、SDK 或开发者工具。

## 快速体验

```bash
git clone https://gitee.com/toothdy/uvx-ui.git
```

1. 使用 HBuilderX 打开仓库根目录。
2. 选择“运行”菜单，并选择 Android、iOS、Web、HarmonyOS 或微信开发者工具等目标。
3. 编译完成后，从首页进入各组件示例。

## 集成到项目

### 1. 复制模块

将下列目录复制到 uni-app x 项目的 `uni_modules` 目录：

```text
uni_modules/
├── lime-dayuts/
├── uvx-tools/
└── uvx-ui/
```

当前入口还会加载项目根目录下的业务语言包，需同时复制：

```text
locales/
├── en.json
├── zh-cn.json
└── zh-tw.json
```

### 2. 配置 easycom

在 `pages.json` 中配置组件映射：

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

### 3. 注册插件

在 `main.uts` 中安装 uvx-ui：

```ts
import App from "./App.uvue";
import { createSSRApp } from "vue";
import uvxui from "@/uni_modules/uvx-ui";

export function createApp() {
  const app = createSSRApp(App);
  app.use(uvxui);

  return {
    app,
  };
}
```

### 4. 引入样式

在 `App.uvue` 中引入全局样式：

```vue
<style lang="scss">
@import "@/uni_modules/uvx-ui/index.scss";
</style>
```

如需在业务 SCSS 中使用主题变量，可在项目的 `uni.scss` 中引入：

```scss
@import "@/uni_modules/uvx-ui/theme.scss";
```

### 5. 使用组件

完成 easycom 配置后，可在页面中直接使用 `uvx-*` 组件：

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

## 目录结构

```text
.
├── common/                     # 示例工程公共样式
├── locales/                    # 业务侧语言包
├── pages/                      # 组件示例页面
├── static/                     # 图片与字体等静态资源
├── uni_modules/
│   ├── lime-dayuts/            # 日期处理依赖
│   ├── uvx-tools/              # 原生动画与系统能力
│   └── uvx-ui/                 # 组件库源码
├── App.uvue                    # 应用入口与全局样式
├── main.uts                    # Vue 应用及插件注册
├── manifest.json               # 应用与平台配置
└── pages.json                  # 页面路由与 easycom 配置
```

## 开发说明

- 页面使用 `.uvue`，脚本使用 UTS，并保持显式、严格的类型声明。
- 跨平台差异使用 uni-app x 条件编译隔离。
- 可滚动页面使用 `scroll-view`、`list-view` 或其他受支持的滚动容器。
- 新组件按 easycom 目录规范放在 `uni_modules/uvx-ui/components/uvx-<name>/`。
- 新增演示页面后，需要在 `pages.json` 注册，并在 `pages/index/data.uts` 添加入口。
- 提交前至少在受影响的目标平台运行对应示例。

## 许可证

[MIT](./LICENSE)
