# package 相关


## npm 查找

1. 层层查找 `node_modules` 目录，直到项目根目录，找不到则报错。（`npm root` 查看根
2. 查找 `package.json` 文件，获取 `main` 字段值，没有默认为 `./index.js`，解析该值。

```json
{
  "files": ["/lib", "esm"], /* what files to publish */
  "scripts": {
    "build": "npm run build:esm && npm run build:cjs",
    "build:esm": "babel --delete-dir-on-start -d esm/ src/",
    "build:cjs": "babel --delete-dir-on-start --env-name cjs -d lib/ src/",
  },
  /* Package peer dependencies. The consumer chooses exact versions. */
  "peerDependencies": {
    "lodash": ">= 3.5.0 < 4.0.0",
    "react": ">= 0.14.0 < 17.0.0"
  },
  "license": "MIT",
}
```

借助第三方包，可以支持运行多个 `namespace:*`，比如 `npm-run-all build:*`。

废弃: `npm deprecate foo@"< 0.40" "Use bar package instead"`
取消发布: `npm unpublish foo`
