## #Switch

```go
switch [условие] {
case num > 1:
	...
case num < 11:
	...	
default:
	...
}
```


____
```go
number := 10
switch {
case num > 1:
	...
	falltrough //не прерывает после выполнения
case num < 11:
	...	
	break //прерывает (стоит по умолчанию)
}
```