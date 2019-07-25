# React v16.6.0 源码解析

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
