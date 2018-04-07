khác với stream thì buffer là global object, có thể tự allocate được

có 3 cách để tạo buffer là

* Buffer.from\(\)
* Buffer.alloc\(\)
* Buffer.allocUnsafe\(\)

```
var buffer =  new ArrayBuffer(8)
var view = new Int32Array(buffer)
```



