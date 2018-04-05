# Event Emitter

1. Tự viết event-emiiter
2. Kế thừa
3. Socket.IO

Viết 1 class Emitter sẽ bắt các sự kiện, mỗi sự kiện tương ứng với 1 hàm listener\(event handler\)

Sau khi tạo class sẽ tạo hàm lằng nghe sự kiện hàm **on\(type, listener\). **  
Để phát ra sự kiện dùng hàm emit

```javascript
function Emitter() {
    this.event = {}
}


Emitter.prototype.on = function (type, listener) {
    this.event[type] = this.event[type] || []
    this.event[type].push(listener)
}

Emitter.prototype.emit = function (type) {
    if (this.event[type]) {
        this.event[type].forEach(function (listener) {
            listener()
        });
    }
}

var emitter = new Emitter()

emitter.on("event1", function () {
    console.log('very good');
})


emitter.on("event1", function () {
    console.log('bad 1');
})

emitter.on("event2", function () {
    console.log('bad 2');
})


var events= [1, 2]

for (var event of events) {
    if (event == "1") {
        emitter.emit('1')
    }
}
```

### 

### 2. Kế thừa từ module event

```javascript
// DÙNG CLASS
'use strict'
var EventEmitter = require('events')

class Dialog extends EventEmitter {
    constructor() {
        super()
        this.msg = 'hello'
    }

    sayHello(data) {
        // console.log(`${this.msg} ${data}`);
        this.emit('hello', data)
    }
}

var dialog = new Dialog()
dialog.on('hello', function (data) {
    console.log(`${this.msg} ${data}`);
})

dialog.sayHello('nhat')
```



