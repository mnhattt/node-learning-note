Đầu tiên là tạo 1 file txt khá lớn để trả về cho client. Chạy xong sẽ có 1 file big-text cỡ 350mb  


```
var fs = require('fs')

var file = fs.createWriteStream('./big-text.txt')

for (var i = 0; i < 5 * 1e5; i++)
    file.write('Lorem ipsum dolor sit amet, consectetur adipiscing elit. Cras convallis ex at nisi egestas scelerisque. Etiam metus mi, sodales varius lectus nec, fermentum feugiat nisi. Class aptent taciti sociosqu ad litora torquent per conubia nostra, per inceptos himenaeos. Donec libero erat, interdum id bibendum eu, eleifend sit amet ex. Donec eleifend varius justo eget ornare. Cras vitae eros eu massa dapibus imperdiet. Donec euismod, augue ac volutpat luctus, mi massa volutpat urna, ut sodales justo elit sed est. Nulla a dignissim nulla. Nunc vulputate dui in vulputate condimentum. Fusce non placerat nulla. Nulla diam velit, rhoncus sit amet sem eget, pharetra consectetur erat. Nunc vitae odio ut risus pulvinar laoreet a eget erat.')

```



Tạo 1 http server đọc file và trả lại cho client theo cách bình thường

Ở cách này server phải đệm file text trong ram nên bật process manager sẽ thấy process này dùng lượng ram hơm 300MB.

```js
var server = require('http').createServer

server((req, res) => {
    res.writeHead(200, {
        'Content-Type': 'text/platin'
    })
    var text = fs.readFileSync(__dirname + '/big-text.txt')
    res.end(text)
}).listen(4000)
```



Cải thiện bằng cách dùng stream đọc từng chuỗi thông tin\(chunk data\) rồi nối\(pipe\) nó vào res. Cách này chỉ tiêu tốn vài chục MB

```js
var server = require('http').createServer


server((req, res) => {
    res.writeHead(200, {
        'Content-Type': 'text/platin'
    })
    var text = fs.createReadStream('./big-text.txt')
    text.pipe(res)
}).listen(4000)
```







VD của Samer Buna về hiệu quả của stream so với các làm truyền thống khi muốn truyền tải 1 file rất lớn

[https://medium.freecodecamp.org/node-js-streams-everything-you-need-to-know-c9141306be93](https://medium.freecodecamp.org/node-js-streams-everything-you-need-to-know-c9141306be93)

