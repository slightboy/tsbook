# 函数

## 声明

函数声明（Function Declaration）：
``` ts
function resolve (value?: any) : void {

}
```

函数表达式（Function Expression）：
``` ts
let reject = function (reason?: any) : void {

}
```
> 不注明函数返回值 默认 any

## 约束
对函数的参数或返回值进行约束有两种方式

类型约束：

``` ts
// 定义 type
type resolveSign = (value?: any) => void

// 不定义
function toPromise (resolve: rejectSign, reject: ((reason?: any) => void) {

}
```

接口约束：

``` ts
interface rejectSign {
	(value?: any) : void
}

function toPromise (resolve: rejectSign, reject: ((reason?: any) => void) {

}
```

## 箭头函数

``` ts
let calc = (x: number, y: number) => { }

```

## 可选参数

``` ts
function calc (x: number, y?: number) {

}
```

## 默认值

``` ts
function calc (x: number, y: number = 1) {

}
```
## 重载 overloads

``` ts
function calc (x: number, y: number)
function calc (args: number[])
function calc (val: number | number[], y?: number) {

}
```

``` ts
function calc (x: number, y: number)
function calc (args: number[])
function calc (...args: any[]) {

}
```


## 参考

- [Functions](http://www.typescriptlang.org/docs/handbook/functions.html) （[中文版](https://zhongsp.gitbooks.io/typescript-handbook/content/doc/handbook/Functions.html)）