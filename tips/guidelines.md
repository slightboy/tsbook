# 变量

## 命名

所有命名应该简单，并保证一定语义

> 赋值 等号 前后加 空格

### 常量

全大写，并确保有完整语义

例：
``` ts
const MAX_PARAMETER_COUNT = 100
```

> 建议把所有常量归置到一个对象中（此处命名可用常规类型和变量命名）

例：
``` ts
const AppSetting = Object.freeze({MaxParameter: 100})
```
### 变量

camelCase

例：
``` ts
let options: object

```

#### 常用命名

1. 计数器 i
1. 单项值 item
1. 索引 index
1. 结果或返回值 result

## 判断

等于或不等于运算时，如果明显判断类型 应使用 === 和 !== 作严格判断

属性判断（适用属性值 非零判断）

``` ts
let count = something.length || 10

if (something.length) {
	// todo
} else {
	// todo
}

```

### 运算符

&& 逻辑与：
``` ts
expr1 && expr2
```

|| 逻辑或：
``` ts
expr1 || expr2
```
! 逻辑非

``` ts
!expr
```

三目：
``` ts
condition ? expr1 : expr2 
```

### if

例：
``` ts
if (condition1 === condition2) {
	// todo
} else if (condition3 === condition4) {
	// todo
} else {
	// todo
}
```

如果 代码只有一行，省略 { }
例：
``` ts
if (condition1 === condition2)
	// todo
else if (condition3 === condition4)
	// todo
else 
	// todo
```

避免嵌套

例：
``` ts
function test () {
	if (condition) {
		// todo1
	} else {
		// todo2
	}
}

function test () {
	if (condition) {
		// todo1
		return
	}
	// todo2
}
```

控制反转

例：
``` ts
function test () {
	if (condition) {
		// todo1
	} else {
		// todo2
	}
}

function test () {
	if (!condition) {
		// todo2
		return
	}

	// todo1
}

```
实例：
``` ts
async function 'm.add' (data) {
  debug(this.protocol, data)
  if (data && data.group && data.group.id && ((data.group.members && data.group.members.length) || (data.group.managers && data.group.managers.length))) {
    let [result, err] = await this.service('member').upsert(data.group)
    if (!err) {
      if ((result.managers && result.managers.length) || (result.members && result.members.length)) {
        if (result.members) {
          result.members = result.members.map(e => e.id)
        }
        this.socket.user.reply(this.protocol, {id:data.id, group:result, ret:0})
        if (result.members)  {
          if (result.members.length === 0) {
            return this.socket.group.to(result.id).broadcast(this.protocol, {id:data.id, group:result, operator:this.socket.user.id})
          }
          this.socket.group.join(result.id, result.members)
          await this.service('user').upsert({id:result.members, group:result.id})
        }
        setTimeout(() => this.socket.group.to(result.id).broadcast(this.protocol, {id:data.id, group:result, operator:this.socket.user.id}), this.config.socket.delay)
      } else {
        this.socket.user.reply(this.protocol, {id:data.id, ret:400})
      }
    } else {
      this.socket.user.reply(this.protocol, {id:data.id, ret:err })
    }

  } else {
    this.socket.user.reply(this.protocol, {id: data.id, ret:400})
  }
}

async function 'm.add' (data) {
  debug(this.protocol, data)
  if (!data || !data.group || !data.group.id || (data.group.members && data.group.members.length === 0) && (data.group.managers && data.group.managers.length === 0) ) return this.socket.user.reply(this.protocol, {id: data.id, ret:400})

  let [result, err] = await this.service('member').upsert(data.group)

  if (err) return this.socket.user.reply(this.protocol, {id:data.id, ret:err })

  if ((result.managers && result.managers.length === 0) && (result.members && result.members.length === 0)) return this.socket.user.reply(this.protocol, {id:data.id, ret:400})

  if (result.members)
    result.members = result.members.map(e => e.id)

  this.socket.user.reply(this.protocol, {id:data.id, group:result, ret:0})

  if (result.members)  {
    if (result.members.length === 0)
      return this.socket.group.to(result.id).broadcast(this.protocol, {id:data.id, group:result, operator:this.socket.user.id})
    this.socket.group.join(result.id, result.members)

    await this.service('user').upsert({id:result.members, group:result.id})
  }

  setTimeout(() => this.socket.group.to(result.id).broadcast(this.protocol, {id:data.id, group:result, operator:this.socket.user.id}), this.config.socket.delay)
}

```

### swtich

``` ts
swtich (condition) {
	case '1':
		break
	case '2':
	case '3':
		break
	default:
}
```
备注：
1. return 中断并跳出函数

## 循环

### for 及 foreach
例：
> 单行省略 {}
``` ts
for (let i = 0; i < count; i++) {
	// todo
}
```

``` ts
for each (let key in obj) {

}
```

备注：
1. continue 忽略其后代码，直接进入下一循环
1. break 中断当前循环
1. return 中断循环并跳出函数



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