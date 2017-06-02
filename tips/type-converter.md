# 类型转换

## “尖括号”语法

``` ts
let someValue: any = "this is a string"
let strLength: number = (<string>someValue).length
```

## as 运算符

``` ts
let someValue: any = "this is a string"
let strLength: number = (someValue as string).length
```

# 类型判断

## is 返回值类型谓词

is 运算符是 typescript 独有，即表示它不参与实际编译后的运算。

> is 只能做返回值修饰

``` ts

function isPromise(val: any): val is Promise {
    return (<Promise>val).then !== undefined;
}

```

## typeof 判断

typeof 只能用于判断基本类型，不能用于判断特定类型。
即以下类型：
``` ts
'string' | 'number' | 'boolean' | 'symbol' | 'undefined' | 'object' | 'function'
```



## instanceof 运算符

