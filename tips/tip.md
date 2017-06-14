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