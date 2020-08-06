webpack 中原始写法

```js
 import(/* webpackChunkName: "basic" */`@/views/basic.vue`
```

但是我懒 就写了一个函数来引入

```js
const load = component => () => import(`@/views/basic/${component}/index`);
```

遇到问题 动态加载出错 Cannot find module '@/views/xxx'

知乎上看到的解答：[参考链接](https://zhuanlan.zhihu.com/p/139232427)

原来写法

```js
export const loadView = view => {
  return () => import(`@/views/${view}`);
};
```

改为

```js
export const loadView = view => {
  return resolve => require([`@/views/${view}`], resolve);
};
```

webpack 版本问题，webpack4 中动态 import 不支持变量方式，
该修改对于生产环境无影响，只在开发环境有问题
