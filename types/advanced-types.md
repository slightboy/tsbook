# 交叉类型 Intersection Types

交叉类型是多个类型合并为一个类型。用符号（&）进行合并。

``` ts
type ID {
	id: string
}

type Name {
	name: string
}

type UserInfo = ID & Name


function test (val: ID & Name) {

}


```

# 联合类型 Union Types

联合类型可以表示该类型是几个类型之一。用符合（|）表示间隔。

``` ts
type ID = string | number

function test (val: string | number) {

}
```
