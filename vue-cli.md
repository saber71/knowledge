# Vue-Cli 项目打包保留类名

```javascript
// 包括Vue.js组件
module.exports = {
  chainWebpack: (config) => {
    config.optimization.minimizer("terser").tap((args) => {
      const { terserOptions } = args[0];
      terserOptions.keep_classnames = true;
      terserOptions.keep_fnames = true;
      return args;
    });
  },
};
```
