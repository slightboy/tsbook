# 接口 interfaces

接口是对象行为的抽象


## 字段

``` ts
interface IGroup {
	id: string
}
```

## 方法

``` ts
interface IGroup {
	addMember (val: IMember) : void
}
```
或
``` ts
interface IGroup {
	addMember: (val: IMember) => void
}
```

## 函数 Function Types
``` ts
interface AddMemberFunc {
	(val: IMember) : void
}
```
重载 overloads

``` ts
interface AddMemberFunc {
	(val: IMember) : void
	(id: string) : void
}
```

## 构造函数 constructor

``` ts
interface IGroupConstructor {
	new (id: string) : IGroup
}
```
重载 overloads
``` ts
interface IGroupConstructor {
	new (id: string) : IGroup
	new (id: string, name: string) : IGroup
}
```

## 可索引的类型 Indexable Types

> 可索引的类型必须是 number | string | symbol

``` ts
interface IGroupMap {
	[id: string]: IGroup
}
```

## 只读
``` ts
interface IGroup {
	readonly id: string
}
```

## 可选
``` ts
interface IGroupMap {
	name?: string
}
```


## 继承

``` ts
interface IHaveID {
	id: string
}

interface IHaveName {
	name: string
}

interface IGroup extends IHaveID, IHaveName {
	addMembers (val: IMember) : void
}

```


## 实现

``` ts
interface IGroup {
	id: string
	name: string
	addMember (val: IMember)
}

class Group implements IGroup {
	id: string
	name: string
	addMember (val: IMember) {

	}
}
```