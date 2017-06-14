# 命名

1. 类型 PascalCase
1. 类 PascalCase
1. 枚举及枚举项 PascalCase
1. 接口 PascalCase，并且不要使用 I 做前缀
1. 函数 camelCase
1. 属性或本地变量 camelCase
1. 不要使用 m_ 当私有属性前缀，少用 _ 前缀
1. 尽量保证命名有意义
1. 单个返回值 result
1. for，foreach 及其他单项值 item
1. for 及其他单项计数器 i
1. 索引 index
1. 箭头函数 e

# 模块及组件

1. 一个文件对应一个逻辑组件
1. 相似功能组件放在一个模块中
1. 模块组织可以目录形式也可以以 namespace 形式

# 类型

1. 类型定义应放在文件顶部
1. 不要在全局命名空间里定义类型或值
1. 公共类型定义可以放在 /types.ts

# null 和 undefined

1. 使用 undefined，不要使用 null

# flags

1. 当一个类型中有超过2个 bool 属性时，应该使用 flag

# 注释

1. JSDoc 风格注释

# 字符串

1. 使用单引号

# 注意事项

1. 尽量不使用 for...in for...of
1. 用 for 替代 foreach，也可使用 Array.prototype.forEach | Array.prototype.map | Array.prototype.filter



## 风格

1. 使用箭头函数替代匿名函数表达式
1. 只有在需要的时候才把箭头函数的参数括起来

	坏：
	``` ts
	(e) => e > 10
	```
	好：
	``` ts
	e => e > 10
	(x, y) => x + y
	<T>(e: T) => [T]
	```
1. 能用一行解决的，不要使用多行

	坏：
	``` ts
	e => {
		return {
			id: {
				e
			}
		}
	}
	```
	好：
	``` ts
	e => ({id: {e}})
	```

1. 单条判断或循环省略 花括号
1. { 与语句在同一行

	``` ts
	function () {

	}

	if  (something) {

	}
	for (something) {
		
	}
	swtich (something) {

	}
	```
1. 小括号开始不要有空格，逗号，冒号，分号后要有一空格。

``` ts
for (let i = 0, n = str.length; i < 10; i++) { }
if (x < 10) { }
function f(x: number, y: string) : void { }
```

# 技巧

## 箭头函数

### 返回对象：

``` ts
e => ({id: e})
```

### Rest 参数：

``` ts
(param1, param2, ...rest) => { statements }
```

### [Rest 参数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/rest_parameters)：
``` ts
(param1, param2, ...rest) => { statements }
```

### [默认参数](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Functions/Default_parameters)：
``` ts
(param1 = defaultValue1, param2, …, paramN = defaultValueN) => { statements }
```

### [Destructuring](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/Destructuring_assignment)：
``` ts
let f = ([a, b] = [1, 2], {x: c} = {x: a + b}) => a + b + c;
f();  
// 6
```

### [this](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Operators/this)：
箭头函数之前

方法一：
``` ts
let self = this, callback = function () { self.id++ }
```

方法二：
``` ts
let callback = (function () { this.id++ }).bind(this)
```

使用箭头函数:
``` ts
let callback = () => this.id++
```

## 判断

### 严格判断

在类型或判断数值确定的情况下使用严格判断




### 避免嵌套
之前：
``` ts
for (let x = 1, y = 2; x < y; ++x, --y) {
	if (x === 1)
		break
	else if (y === 2)
		y = 5
	else
		return
}
```
改进：
``` ts
for (let x = 1, y = 2; x < y; ++x, --y) {
	if (x === 1) break
	if (y !== 2) return
	y = 5
}
```