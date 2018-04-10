# Buffer

Buffer liên quan nhiều tới Stream nhưng khác với stream thì buffer là global object, có thể tự allocate được. Xử lý như một mảng bình thường nhưng giá trị thể hiện bằng hex.

Bình thường hay đổi giá trị nhị  phân thành kí tự để đọc bằng toString\(\)

```text
var fs = require('fs')

fs.readFile('./text.txt', (err, buf) => {
    console.log(buf);            // <Buffer 31 32 33 34 35 36 37 38 39>
    console.log(buf.toString()); // 123456789    
})
```

Có thể làm việc trực tiếp với buffer mà không cần chuyển mã

```text
fs.readFile('./test.txt', (err, buf) => {
    for (var i = 0; i < buf.length; i++) {
        buf[i] = buf[i] + (65 - 49)
    }
    console.log(buf.toString()); // ABCDEFGHI
})

```



có 3 cách để tạo buffer là

* Buffer.from\(\)
* Buffer.alloc\(\)
* Buffer.allocUnsafe\(\)

```text
var buffer =  new ArrayBuffer(8)
var view = new Int32Array(buffer)
```

