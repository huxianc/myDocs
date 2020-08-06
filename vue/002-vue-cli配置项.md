> [参考链接](https://github.com/staven630/vue-cli4-config/)

### 下面列出我使用过的

- proxy
- alias
- 压缩图片
  > npm i -D image-webpack-loader

```js
// 生产模式使用
config.module
  .rule("images")
  .use("image-webpack-loader")
  .loader("image-webpack-loader")
  .options({
    mozjpeg: { progressive: true, quality: 65 },
    optipng: { enabled: false },
    pngquant: { quality: [0.65, 0.9], speed: 4 },
    gifsicle: { interlaced: false },
    // webp: { quality: 75 }
  });
```

- 打包分析
  > npm i -D webpack-bundle-analyzer

```js
config
  .plugin("webpack-bundle-analyzer")
  .use(require("webpack-bundle-analyzer").BundleAnalyzerPlugin, [
    {
      analyzerMode: "static", // 静态生成 不占用端口
    },
  ]);
```

- 去掉 console.log
  > npm i -D babel-plugin-transform-remove-console

`babel.config.js`文件中

```js
const IS_PRODUCTION = process.env.NODE_ENV === "production";
const plugins = [];
if (IS_PRODUCTION) {
  plugins.push([
    "transform-remove-console",
    {
      exclude: ["error", "warn"],
    },
  ]);
}

module.exports = {
  presets: [["@vue/app", { useBuiltIns: "entry" }]],
  plugins,
};
```

- splitChunks
- ie 兼容
