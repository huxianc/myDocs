1. 使用:export{}导出为一个对象

```scss
:export {
  menuText: $menuText;
  menuActiveText: $menuActiveText;
  subMenuActiveText: $subMenuActiveText;
  menuBg: $menuBg;
  menuHover: $menuHover;
  subMenuBg: $subMenuBg;
  subMenuHover: $subMenuHover;
  sideBarWidth: $sideBarWidth;
}
```

2. 在 vue 文件中引入该文件

```js
import variables from "@/styles/variables.scss";
```

3. 然后利用 computed 属性进行转换(不然会报错-不能直接使用)

```js
variables() {
  return variables;
}
```

然后就可以在 vue 文件中使用了
