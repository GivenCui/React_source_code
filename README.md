# React v16.6.0 源码解析<!-- omit in toc -->

## 目录<!-- omit in toc -->
- [相关](#%e7%9b%b8%e5%85%b3)
- [目录结构说明](#%e7%9b%ae%e5%bd%95%e7%bb%93%e6%9e%84%e8%af%b4%e6%98%8e)
- [overview](#overview)
- [babel 在线 JSX 转`React.createElement`测试](#babel-%e5%9c%a8%e7%ba%bf-jsx-%e8%bd%acreactcreateelement%e6%b5%8b%e8%af%95)


## 相关

- [gitBook-React 源码阅读](https://mubu.com/doczGCeD9IYY0)

## 目录结构说明

根目录结构

```shell

.
├── README.md
├── 01-demos       # 测试demo
├── flowChart      # 关键功能流程图
├── react          # react github的代码
├── react-hooks    # react新增hooks的代码
└── update-scheduler-demo    # scheduler demo

```

react/packages

```shell
.
├── create-subscription
├── events             # 合成事件
├── jest-react
├── react              # react core代码
├── react-art
├── react-cache
├── react-dom          # react-dom  (依赖react-reconciler)
├── react-is
├── react-native-renderer
├── react-noop-renderer
├── react-reconciler   # 重要 (RN中复用)
├── react-test-renderer
├── scheduler          # 调度, 实现async module
└── shared             # 公用代码

```

## overview

1. `react` 源码不多, 如何在不同平台渲染, 拆分出 react-dom 和 react-native-renderer 等
2. 使用了[flow](https://flow.org/en/docs/getting-started/)做静态类型检测

   ```js
   // @flow
   function square(n: number): number {
     return n * n
   }

   square('2') // Error!
   ```

## babel 在线 JSX 转`React.createElement`测试

> ☞ [babel.io/repl](https://babeljs.io/repl), 注意: 自定义组件大小写决定了转换为原生元素还是自定义元素


例子 1:

```js
// jsx
<div><div/>     // 元素名小写

// es5
"use strict";

React.createElement("div", null)
```

例子 2:

```js
// jsx
<Button        // 元素名大写, 自定义标签
  className="btn"
  onClick={this.clickHandle}
  type="primary"
>
  <span>1</span>
  自定义按钮
</Button>;

// es5
"use strict";

// React.createElement(元素, 属性对象, 子元素1, 子元素2)
React.createElement(
  Button,
  {
    className: "btn",
    onClick: (void 0).clickHandle,
    type: "primary"
  },
  React.createElement("span", null, "1"),
  "\u81EA\u5B9A\u4E49\u6309\u94AE"
);
```
