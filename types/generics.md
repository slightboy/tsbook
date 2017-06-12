# 泛型 Generics

泛型用占位符的形式提供了可复用组件。可用于 type、interface、function 、class 等定义。

以下为将元素转换为元素数组的示例。

不使用泛型：
``` ts
function toArray (val: any) : any[] {
	return [val]
}
```
此处如果我们传一个 string，想得到一个 string[]，得到的却是 any[]，这显然不是我们想要的。
解决办法只有每个类型写一个方法，但是这又明显不现实。


使用泛型：
``` ts
function toArray<T> (val: T) : T[] {
	return [val]
}
```


## 泛型 type

function：
``` ts
let toArray: <T>(val: T) => T[]
```

interface：
``` ts
let toArray: { <T>(val: T) : T }
```

## 泛型 interface

``` ts
interface toArray {
	<T>(val: T) : T[]
}

interface toArray<T> {
	(val: T) : T[]
}

```
## 泛型 class

``` ts
class Dictionary<T, K> {

}

```


## 泛型约束

``` ts
type ObjectID = {id: string}

function doThing <T extends ObjectID>(val: T[]) : string[] {
	return val.map(e => e.id)
}
```
