# babel-plugin-inject-polyfills

> 在项目的入口文件中插入指定的 polyfills（受 `VUE CLI 3` 启发）。<br/>
Add polyfill imports to the entry file ( Inspired by `VUE CLI 3` ).


### Installation

```
npm i babel-plugin-inject-polyfills -D
# or
yarn add babel-plugin-inject-polyfills --dev
```

### Usage

一个配和 `@babel/plugin-syntax-dynamic-import` 解决 `webpack` 中 `babel-loader` 无法处理动态 `import()` 语法的示例。[参考链接](https://babeljs.io/docs/en/babel-plugin-syntax-dynamic-import)。它使得你无需显式的在 `webpack` 的 `entry` 中指定需要的 `polyfills` 或者 在入口文件中 `import` 它们。

An example with `@babel/plugin-syntax-dynamic-import` which solves the problem that `babel-loader` cannot handle the `import()` syntax in `webpack`. [Reference Link](https://babeljs.io/docs/en/babel-plugin-syntax-dynamic-import). It eliminates the need to explicitly specify the `polyfills` in the `entry` of `webpack` or `import` them in the entry file.

```js
const presets = [
  [
    "@babel/env",
    {
      "targets": [
        "> 1%",
        "last 2 versions",
        "IE >=9",
      ],
      "useBuiltIns": "usage",
      // https://babeljs.io/docs/en/babel-preset-env#exclude
      "exclude": [
        "es6.array.iterator",
        "es6.promise"
      ]
    }
  ]
];
const plugins = [
  "@babel/plugin-syntax-dynamic-import",
  [
    "babel-plugin-inject-polyfills",
    // 指定你需要添加的 polyfills （specify the polyfills that you want to import）
    {
      "polyfills": [
        "es6.array.iterator",
        "es6.promise"
      ]
    }
  ]
]

module.exports = { presets, plugins };
```
