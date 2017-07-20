# 判断

## 短线判断

之前：
``` js
if (something2) {
	// do
} else {
	// do
}
```
之后：
``` js
if (something2) {
	// do
	return
}
// do
```

之前：
``` js
if (something1) {
	if (something2) {
		// do1
	} else {
		// do2
	}
} else {
	// do3
}
```
之后：
``` js
if (something1) {
	if (something2) {
		// do1
	}
	// do2
	return
}
// do3
```



TypeScript:
1. 基础类型
1. 高级类型
1. 类型混合
1. 泛型

Vue：
1. Vue 实例组成
1. 模板结构
1. 指令
1. 计算属性、方法、事件
1. 组件及组件之间通讯

Vuex：
1. namespace 应用、State 及绑定、Getters 及绑定、Mutations、Actions 及绑定

JavaScript & TypeScript
1. 变量、条件、循环相关命名，语法，规则及技巧
