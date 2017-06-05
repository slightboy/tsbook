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

用于检查实例是否继承于某个类

> 官方注解：instanceof 运算符用来检测 constructor.prototype 是否存在于参数 object 的原型链上。


``` ts
'string' instanceof String
```

# 类型保护与区分类型 Type Guards and Differentiating Types

以上讲解的三种方式判断范围内视类型已转换

``` ts
interface Bird {
    fly();
    layEggs();
}

interface Fish {
    swim();
    layEggs();
}

function getSmallPet(): Fish | Bird {
    // ...
}
```

``` ts
let pet = getSmallPet();

// 每一个成员访问都会报错
if (pet.swim) {
    pet.swim();
}
else if (pet.fly) {
    pet.fly();
}
```
一般写法：
``` ts
let pet = getSmallPet();

if ((<Fish>pet).swim) {
    (<Fish>pet).swim();
}
else {
    (<Bird>pet).fly();
}
```

## 用户自定义的类型保护

``` ts
function isFish (pet: Fish | Bird): pet is Fish {
    return (<Fish>pet).swim !== undefined;
}

let pet = getSmallPet();

if (isFish(pet)) {
    pet.swim();
}
else {
    pet.fly();
}

```

## typeof 类型保护

``` ts
function padLeft(value: string, padding: string | number) {
    if (typeof padding === "number") return Array(padding + 1).join(" ") + value
    if (typeof padding === "string") return padding + value
    throw new Error(`Expected string or number, got '${padding}'.`)
}

```

## instanceof 类型保护

``` ts
let pet = getSmallPet();

if (pet instanceof Fish) {
    pet.swim();
}
else {
    pet.fly();
}

```