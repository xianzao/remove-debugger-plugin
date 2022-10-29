<br />
<h1 align="center">remove-debugger-plugin</h1>
<p align="center">
<a href="https://github.com/xianzao/remove-debugger-plugin/stargazers"><img alt="GitHub stars" src="https://img.shields.io/github/stars/xianzao/remove-debugger-plugin"></a>
<a href="https://github.com/xianzao/remove-debugger-plugin/network"><img alt="GitHub forks" src="https://img.shields.io/github/forks/xianzao/remove-debugger-plugin"></a>
</p>

## 目标

移除上线前 debug 代码的 plugins

## 使用方式

局部安装

```BASH
# 1. 项目中执行
npm install -D remove-debugger-plugin

# 2. babelrc中添加
{
  plugins: ["no-debugging"]
}

这个插件默认会移除 debugger; 和 console 调用。

这个插件可以移除 debugger 、 console 、 alert 和 自定义的调试函数调用和定义。

为保证在开发阶段不转换代码，记得将这个插件只配置在发布阶段：

# babelrc
{
 {
  "env": {
    "publish": {
      "presets": [
        "@babel/preset-env"
      ],
      "plugins": ["no-debugging"]
    }
  }
}

# package.json script
{
  "scripts": {
    "build": "cross-env BABEL_ENV=publish webpack", # 类似
  },
}
```

### options

| Property | Type    | Default | Description                                        |
| -------- | ------- | ------- | -------------------------------------------------- |
| debugger | Boolean | true    | 移除断点调试 debugger 代码                         |
| console  | Boolean | true    | 函数调用                                           |
| alert    | Boolean | null    | 函数调用                                           |
| debugFn  | String  | null    | 指定的自定义调试代码函数（包括调试函数声明和调用） |

## 使用

### 例子

1. 使用默认配置

```js
.babelrc

{
  plugins: [
    [
      "no-debugging"
    ]
  ]
}
```

转换前：

```js
const a = 12
const b = 13

function add(m, n) {
  debugger
  return m + n
}

const result = add(a, b)

console.log(result)
```

转换后：

```js
const a = 12
const b = 13

function add(m, n) {
  return m + n
}

const result = add(a, b)
```

2. 自定义配置
   移除 alert

```js
.babelrc

{
  plugins: [
    [
      "no-debugging",
      {
        alert: true,
        console: false
      }
    ]
  ]
}
```

转换前：

```js
const a = 12
const b = 13

function add(m, n) {
  debugger
  return m + n
}

alert(result)

const result = add(a, b)

console.log(result)
```

转换后：

```js
const a = 12
const b = 13

function add(m, n) {
  return m + n
}

const result = add(a, b)

console.log(result)
```

## NPM

项目已自动更新至 NPM，请移步至[remove-debugger-plugin](https://www.npmjs.com/package/remove-debugger-plugin)

```

```
