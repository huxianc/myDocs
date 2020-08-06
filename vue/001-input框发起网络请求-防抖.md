#### watch 监听 input 变化并防抖实现网络请求

- 在`created`内新建一个函数，使用防抖包裹起来

```js
this.debouncedSearch = debounce(this.handleInputDamageCode, 300);
```

- 这里包裹的`this.handleInputDamageCode`就是处理网络请求的函数

```js
async handleInputDamageCode(newVal = this.damageForm.code) {
		if (newVal === '') return;
        // 网络请求
		}
```

- `watch` 中监听`created`的函数

```js
	watch: {
		'damageForm.code': {
			handler() {
				this.debouncedSearch();
			},
		}
	}
```
